**PASO 1.** Definir el layout de la activity principal
**activity_main.xml**
````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:layout_gravity="center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Introduce Nombre:"/>
    <EditText
        android:layout_gravity="center"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:id="@+id/datos" />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button"
        android:text="Saludo"/>

</LinearLayout>
````
**PASO 2.** Definir la interfaz gráfica de la segunda ventana
**activity2.xml**
````xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/
xmlns:app="http://schemas.android.com/apk/res-auto"
android:layout_width="match_parent"
android:layout_height="match_parent">

  <TextView
      android:id="@+id/textoActivity2"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_marginStart="132dp"
      android:layout_marginTop="320dp"
      android:text="textoActivity2"
      android:textSize="20dp"
      app:layout_constraintStart_toStartOf="parent"
      app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
````
**PASO 3.** Crear una activity para la pantalla secundaria
**Activity2.kt**
````kotlin
class Activity2 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity2)
        val textView=findViewById<TextView>(R.id.textoActivity2);
        val intento= this.intent
        textView.setText("Hola "+intento.getStringExtra("DATO")+ ", ¿como estas?")
        }
}
````
**PASO 4.** Declarar en el Manifest actividades que usará nuestra app
````xml
<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap ic_launcher_round"
    android:supportsRtl="true"
    android:screenOrientation="landscape"
    android:configChanges="orientation|screenSize"
    android:theme="@style/Theme.EjercicioResuelto2Activitys">

    <activity android:name=".MainActivity">
      <intent-filter>
          <action android:name="android.intent.action.MAIN" />
          <category android:name="android.>intent.category.LAUNCHER" />
      </intent-filter>
    </activity>
    <activity android:name=".Activity2"/>
</application>
````
**PASO 5.** Implementar la lógica de funcionamiento
````kotlin
class MainActivity:AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        findViewById<Button>(R.id.button).setOnClickListener {
            val intento=Intent(applicationContext, Activity2::class.java)
            val datos=findViewById<EditText>(R.id.datos).text.toString()
            intento.putExtra("DATO", datos)
            startActivity(intento)
        }
    }
}
````
