<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>

- [Tema 2](#tema-2)
  - [Recursos Android](#recursos-android)
    - [<o>Subdirectorios</o>](#osubdirectorioso)
    - [<o>Carpetas Mipmap y Drawable</o>](#ocarpetas-mipmap-y-drawableo)
    - [<o>Carpeta values</o>](#ocarpeta-valueso)
    - [Acceder a los Recursos en Android](#acceder-a-los-recursos-en-android)
  - [Android Manifest](#android-manifest)


# [Tema 2](tema2_estructura_de_un_proyecto_Android_Studio.pdf)



## Recursos Android

### <o>Subdirectorios</o>
![recursos](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/recursosCarpetas.jpg?raw=true)

- **drawable**: <r>Recursos gráficos</r> que vamos a utilizar como .png, .jpg, .gif...
- **mipmap**: Unicamente guardaremos <r>iconos de la aplicación</r> en las diferentes densidades de pantalla.
- **layout**: Archivos XML que contienen <r>definiciones de la interfaz de usuario(vistas)</r>.
- **menu**:Archivos XML que establecen las <r>características para los menús</r> usados en la interfaz.
- **values**: Archivos XML que contienen datos simples como <r>enteros, strings, booleanos, colores</r>.
  
### <o>Carpetas Mipmap y Drawable</o>

<b> Densidades:</b>

- **Mediun Dots per Inch(mdpi):** 160pulgadas
- **High Dots per Inch(hdpi):** 240pulgadas
- **Extra high dots per inch(xhdpi):** 340pulgadas
- **Extra Extra high dots per inch(xxhdpi):** 480pulgadas

### <o>Carpeta values</o>

Se crean por defecto 3 carpetas  <r>colors, strings, theme</r>.

<b>Strings:</b>  almacena todas las cadenas que se muestran

![String](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/stringXML.png?raw=true)

<b>Color:</b>  a cada estiqueta \<color\> se le asigna un <r>nombre</r> y una referencia <r>\#hexadecimal</r> que es la que representa el color
![Colors](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/colorsXML.png?raw=true)

Al crear un recurso se le pueden dar propiedades adicionales como por ejemplo la nacionalidad y lengua en el caso de un strings
![CrearString](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/CrearRecurso.gif?raw=true)


### Acceder a los Recursos en Android

**Desde Kotlin:**

Cada identificador se ubica en una clase llamada R a través de una constante entera **R.tipoRecurso.nombreRcurso**. 
![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/AccederRecurso.png?raw=true)

**Desde XML:**

Para ello usamos la sintaxis @[Paquete:]tipoRecurso/nombreRecurso
![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/AccederRecursoXML.png?raw=true)


## Android Manifest

**<b>Manifest:</b>** Es el archivo más esencial de nuestra aplicación que contiene nodos descriptivos sobre las características de la App como la versión de SDK,permisos necesarios, servicios, activitys.

**<b>Etiqueta aplicacion:</b>**

- <o>allowBackup(true/false):</o> Indica si la aplicacion sera persistente al cerrar nuestro AVD.
- <o>icon:</o> Indica donde esta ubicado el icono de la aplicación.
- <o> label:</o> Nombre de la aplicación que vera el usuario en su telefono
- <o>theme:</o> Apunta al archivo styles.xml donde se define el estilo visual de la aplicación
- <o>supportsRtl:</o> Declara si la aplicacion esta dispuesta a admitir diseños de derecha a izquierda

**<b>Etiqueta activity:</b>**

Representa actividades de la aplicaón

- <o> label:</o> Texto que se mostrara en la cabecera de la actividad
- <o> android:name:</o> Especifica el nombre de la actividad
- <o> android:screenOrientation:</o> Define la orientación de la aplicación vertical o apaisada
- <o>android:configChanges:</o> se definen los diferentes eventos que manejar con el fin de evitar que se destruya la actividad (al cambiar de orientacion o cuando aparece un teclado) se separan por \| ejemplo <r>keyboard\|keyboardHydden\|orientation</r>

 Con la etiqueta  \<intent-filter\>  y su elemento  \<action\>  estamos indicando que esta activity va a ser un punto de entrada para nuestra aplicación. Sólo puede haber una activity que reaccione a este
intent. Con elemento  <category>  le decimos a Android que queremos que esta activity sea añadida al lanzador de la aplicación.

![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/ManifestIntentFilter.png?raw=true)




**<b>Etiqueta uses-permissions:</b>**

 Android restringe el uso de los recursos del sistema: tarjeta SD,
 WIFI, HW de audio, etc. Mediante este Tag especificamos los permisos que va a necesitar nuestra aplicación.




 - <o>android.permisssion.RECORD_AUDIO:</o> Acceso al hw de audio y grabación.
 - <o> android.permisssion.INTERNET:</o> Permiso a todas las API’s de red.
 - <o> android.permisssion.WRITE_EXTERNAL_STORAGE:</o>Almacenamiento externo.
 - <o> android.permisssion.WAKE_LOCK:</o>  nos permite antibloqueo 

**<b>Permisos en momento de ejecución:</b>**

[Permisos en el momento de ejecución](https://developer.android.com/training/permissions/requesting)

1. Declara los permisos en el manifest
2. Esperar a que el usuario invoque la accion que requiere
   1. Comprueba que los permisos todavia no han sido otorgados
   2. Muestra justificación (Dialogo) por la que se requieren los permisos, en caso que se vea necesario.**Linea 6 y 10**
   3. Solicita los permisos. **Linea 14**
3. En caso afirmativo accede al recurso, si no es asi se le proporciona un mensaje explicando que no puede acceder

[Tema2 pagina 13](tema2_estructura_de_un_proyecto_Android_Studio.pdf)

```kotlin  

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



