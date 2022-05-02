
**PASO 1.** Preparar la vista de la aplicación
**activity_main.xml**

````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:orientation="vertical"
android:gravity="center"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">

  <Button
      android:id="@+id/navegador"
      android:layout_width="200dp"
      android:layout_height="wrap_content"
      android:text="@string/abrir_navegador"/>
  <Button
      android:id="@+id/abrir"
      android:layout_width="200dp"
      android:layout_height="wrap_content"
      android:text="@string/abrir_aplicaci_n"/>
  <Button
      android:id="@+id/escuchar"
      android:layout_width="200dp"
      android:layout_height="wrap_content"
      android:text="@string/escuchar_canci_n"/>

</LinearLayout>
````

**PASO 2.** Codificar la ejecución del primer botón

**MainActivity.kt**
````kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
    findViewById<Button>(R.id.navegador).setOnClickListener (View.OnClickListener {
        val intent = Intent(Intent.ACTION_WEB_SEARCH).apply {
            putExtra(SearchManager.QUERY, "iesdoctorbalmis")
        }
        if (intent.resolveActivity(packageManager) != null) startActivity(intent)
    })
}
````
**PASO 3.** Abrir aplicación externa
**MainActivity.kt**
````kotlin
findViewById<Button>(R.id.abrir).setOnClickListener {
    val intent= Intent();
    intent.setComponent(ComponentName("com.ejemplos.myapplication",
        "com.ejemplos.myapplication.MainActivity"))
    if (intent.resolveActivity(packageManager) != null) startActivity(intent)
    }
````

**PASO 4.** Acceso a la tarjeta SD
Interfaz gráfica
**PASO 5.** Lógica Botón Escuchar canción
Pedir permisos

````Kotlin
RESPUESTA_PERMISOS = 111
@RequiresApi(Build.VERSION_CODES.Q)
fun solicitarPermisosYEscucharCancion() {
    if (checkSelfPermission(READ_EXTERNAL_STORAGE) ==
    PackageManager.PERMISSION_DENIED) {
        requestPermissions(arrayOf(READ_EXTERNAL_STORAGE),
          RESPUESTA_PERMISOS)
    } else escucharCancion()
}
override fun onRequestPermissionsResult(
        requestCode: Int,
        //codigo de identificación del resultado
        permissions: Array<out String>,
        //array con los nombres de los permisos
        grantResults: IntArray
        //array de 0 y -1 (permitido,no permitido) en orden)

        super.onRequestPermissionsResult(requestCode, permissions,
        grantResults)
          when (requestCode) {
            RESPUESTA_PERMISOS -> {

            if (grantResults[0] == PackageManager.PERMISSION_GRANTED)
                Toast.makeText(
                    applicationContext,
                    permissions[0] + " Permiso concedido",
                    Toast.LENGTH_SHORT
                ).show()
            escucharCancion()
      }
   }
}
````
Declarar el content provider

**1.** Crear una carpeta xml en los recursos, res\xml y dentro un fichero.
  por ejemplo provider_paths . Donde añadiremos el siguiente código para
  referenciar al directorio raíz.

````kotlin
<?xml version="1.0" encoding="utf-8"?>
<paths>
    <external-path name="external_files" path="."/>
</paths>
````  
**2.** Añadir en el Manifest un provider que haga referencia al recurso creado.
Dentro de la etiqueta aplicación y teniendo en cuenta no olvidar los permisos
de READ_EXTERNAL_STORAGE .
**Manifest.xml**
````kotlin
<provider
    android:name="androidx.core.content.FileProvider"
    android:authorities="${applicationId}.provider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/provider_paths" />
</provider>
````
Codificar el intent

**MainActivity.kt**

````kotlin
class MainActivity : AppCompatActivity() {

    @RequiresApi(Build.VERSION_CODES.Q)
    override fun onCreate(savedInstanceState: Bundle?) {
...

      findViewById<Button>(R.id.escuchar).setOnClickListener
      {
          solicitarPermisosYEscucharCancion()
      }
    }
private fun escucharCancion() {
    //Ruta de la carpeta que usa android para guardar recursos
    //de la aplicación, consta del dominio y es privada a esta
    var directorio=getExternalFilesDir(null)?.absolutePath
    //Cogemos el inicio de la ruta, que corresponde con
    //los archivos multimedia 'storage/emulated/0/'
    directorio=directorio?.substring(0,directorio?.indexOf("Android"))
    val data = File(directorio + "music/minions.mp3")
    val uri = FileProvider.getUriForFile(
        this@MainActivity,
        BuildConfig.APPLICATION_ID + ".provider",
        data
    )
    val intent = Intent(Intent.ACTION_VIEW)
    intent.setDataAndType(uri, "audio/.mp3")
    intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
    startActivity(intent)
   }
...
}
````
