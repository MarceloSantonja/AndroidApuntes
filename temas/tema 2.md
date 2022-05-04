<style>
o { color: Orange }
</style>
<o>* Destacar tipos o composión</o>

- [Tema 2](#tema-2)
  - [Recursos Android](#recursos-android)
    - [Subdirectorios](#subdirectorios)
    - [Carpetas Mipmap y Drawable](#carpetas-mipmap-y-drawable)
    - [Carpeta values](#carpeta-values)
    - [Acceder a los Recursos en Android](#acceder-a-los-recursos-en-android)
  - [Android Manifest](#android-manifest)


# [Tema 2](Xusa/tema2_estructura_de_un_proyecto_Android_Studio.pdf)



## Recursos Android

### Subdirectorios
![recursos](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/recursosCarpetas.jpg?raw=true)

- **<o>drawable</o>**: **Recursos gráficos** que vamos a utilizar como .png, .jpg, .gif...
- **<o>mipmap</o>**: Unicamente guardaremos **iconos de la aplicación** en las diferentes densidades de pantalla.
- **<o>layout</o>**: Archivos XML que contienen **definiciones de la interfaz de usuario(vistas)**.
- **<o>menu</o>**:Archivos XML que establecen las **características para los menús** usados en la interfaz.
- **<o>values</o>**: Archivos XML que contienen datos simples como **enteros, strings, booleanos, colores**.
  
### Carpetas Mipmap y Drawable

**<u>Densidades:</u>**

- **<o>Mediun Dots per Inch(mdpi):</o>** 160pulgadas
- **<o>High Dots per Inch(hdpi):</o>** 240pulgadas
- **<o>Extra high dots per inch(xhdpi):</o>** 340pulgadas
- **<o>Extra Extra high dots per inch(xxhdpi):</o>** 480pulgadas

### Carpeta values

Se crean por defecto 3 carpetas  **colors, strings, theme**.

<o>Strings:</o>  almacena todas las cadenas que se muestran

![String](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/stringXML.png?raw=true)

<o>Color:</o>  a cada estiqueta \<color\> se le asigna un **nombre** y una referencia **\#hexadecimal** que es la que representa el color
![Colors](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/colorsXML.png?raw=true)

Al crear un recurso se le pueden dar propiedades adicionales como por ejemplo la nacionalidad y lengua en el caso de un strings
![CrearString](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/CrearRecurso.gif?raw=true)


### Acceder a los Recursos en Android

**<o>Desde Kotlin:</o>**

Cada identificador se ubica en una clase llamada R a través de una constante entera **R.tipoRecurso.nombreRcurso**. 
![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/AccederRecurso.png?raw=true)

**<o>Desde XML:</o>**

Para ello usamos la sintaxis @[Paquete:]tipoRecurso/nombreRecurso
![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/AccederRecursoXML.png?raw=true)


## Android Manifest

**<o>Manifest:</o>** Es el archivo más esencial de nuestra aplicación que contiene nodos descriptivos sobre las características de la App como la versión de SDK,permisos necesarios, servicios, activitys.

**<o>Etiqueta aplicacion:</o>**

- <o>allowBackup(true/false):</o> Indica si la aplicacion sera persistente al cerrar nuestro AVD.
- <o>icon:</o> Indica donde esta ubicado el icono de la aplicación.
- <o> label:</o> Nombre de la aplicación que vera el usuario en su telefono
- <o>theme:</o> Apunta al archivo styles.xml donde se define el estilo visual de la aplicación
- <o>supportsRtl:</o> Declara si la aplicacion esta dispuesta a admitir diseños de derecha a izquierda

**<o>Etiqueta activity:</o>**

Representa actividades de la aplicaón

- <o> label:</o> Texto que se mostrara en la cabecera de la actividad
- <o> android:name:</o> Especifica el nombre de la actividad
- <o> android:screenOrientation:</o> Define la orientación de la aplicación vertical o apaisada
- <o>android:configChanges:</o> se definen los diferentes eventos que manejar con el fin de evitar que se destruya la actividad (al cambiar de orientacion o cuando aparece un teclado) se separan por \| ejemplo **keyboard\|keyboardHydden\|orientation**

 Con la etiqueta  \<intent-filter\>  y su elemento  \<action\>  estamos indicando que esta activity va a ser un punto de entrada para nuestra aplicación. Sólo puede haber una activity que reaccione a este
intent. Con elemento  <category>  le decimos a Android que queremos que esta activity sea añadida al lanzador de la aplicación.

![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T2/ManifestIntentFilter.png?raw=true)

**<o>Etiqueta uses-permissions:</o>**

 Android restringe el uso de los recursos del sistema: tarjeta SD,
 WIFI, HW de audio, etc. Mediante este Tag especificamos los permisos que va a necesitar nuestra aplicación.

 - <o>android.permisssion.RECORD_AUDIO:</o> Acceso al hw de audio y grabación.
 - <o> android.permisssion.INTERNET:</o> Permiso a todas las API’s de red.
 - <o> android.permisssion.WRITE_EXTERNAL_STORAGE:</o>Almacenamiento externo.
 - <o> android.permisssion.WAKE_LOCK:</o>  nos permite antibloqueo 

**<o>Permisos en momento de ejecución:</o>**

[Permisos en el momento de ejecución](https://developer.android.com/training/permissions/requesting)

1. Declara los permisos en el manifest
2. Esperar a que el usuario invoque la accion que requiere
   1. Comprueba que los permisos todavia no han sido otorgados
   2. Muestra justificación (Dialogo) por la que se requieren los permisos, en caso que se vea necesario.**Linea 6 y 10**
   3. Solicita los permisos. **Linea 14**
3. En caso afirmativo accede al recurso, si no es asi se le proporciona un mensaje explicando que no puede acceder

[Tema2 pagina 13](tema2_estructura_de_un_proyecto_Android_Studio.pdf)

``` kt {highlight=[5,7,11,17]}


    val RESPUESTA_PERMISOS = 111

    @RequiresApi(Build.VERSION_CODES.Q)
    fun solicitarPermisos() {
        if (checkSelfPermission(READ_EXTERNAL_STORAGE) == PackageManager.PERMISSION_DENIED
            || checkSelfPermission(READ_CONTACTS) == PackageManager.PERMISSION_DENIED
        ) {
            if (shouldShowRequestPermissionRationale(READ_EXTERNAL_STORAGE)) {
//Si se decide explicar los motivos de los permisos
// con algo similar a un dialogo
            }
            if (shouldShowRequestPermissionRationale(READ_CONTACTS)) {
//Si se decide explicar los motivos de los permisos
// con algo similar a un dialogo
            }
//Con requestPermissions se pide al usuario que permita los permisos,
//en este caso dos
            requestPermissions(
                arrayOf(READ_EXTERNAL_STORAGE, READ_CONTACTS),
                RESPUESTA_PERMISOS
            )
        }
    } 

```

``` kt {highlight=[9,10,11]}

    override fun onRequestPermissionsResult(
        requestCode: Int,//codigo de identificación del resultado
        permissions: Array<out String>,//array con los nombres de los permisos
        grantResults: IntArrayarray //de 0 y -1 (permitido, no permitido) en orden 
    ) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults)
        when {
            RESPUESTA_PERMISOS == requestCode && grantResults.isNotEmpty() -> {
                for (i in 0..permissions.size - 1) {
                    if (grantResults[i] == PackageManager.PERMISSION_GRANTED)

                        Toast.makeText(


                            applicationContext, "Permiso Concedido " +


                                    permissions[i], Toast.LENGTH_SHORT

                        ).show()
                }
            }
        }
    }
```
>📌 Método que se ejecuta cuando el usuario responde a los permisos. Al método le llega el código de la petición, el array con los nombres de los permisos, y el array de enteros indicando si el permiso ha sido denegado o concedido. 
**Línea 9** se comprueba si el código de entrada es el establecido y si hay resultados. 
**Línea 10 y 11** se recorren todos los permisos y se muestra con un toast los permisos concedidos



#**Falta Gradle....**