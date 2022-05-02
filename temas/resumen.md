<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>

# TODOs:

- <r>var</r> 
- <o>var</o> 
- <g>var</g> 
- <b>var</b> 


# Android

## [Tema 2](tema2_estructura_de_un_proyecto_Android_Studio.pdf)

### Recursos Android

#### <o>Subdirectorios</o>
![recursos](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/recursosCarpetas.jpg?raw=true)

- **drawable**: <r>Recursos gráficos</r> que vamos a utilizar como .png, .jpg, .gif...
- **mipmap**: Unicamente guardaremos <r>iconos de la aplicación</r> en las diferentes densidades de pantalla.
- **layout**: Archivos XML que contienen <r>definiciones de la interfaz de usuario(vistas)</r>.
- **menu**:Archivos XML que establecen las <r>características para los menús</r> usados en la interfaz.
- **values**: Archivos XML que contienen datos simples como <r>enteros, strings, booleanos, colores</r>.
  
#### <o>Carpetas Mipmap y Drawable</o>

##### Densidades

- **Mediun Dots per Inch(mdpi):** 160pulgadas
- **High Dots per Inch(hdpi):** 240pulgadas
- **Extra high dots per inch(xhdpi):** 340pulgadas
- **Extra Extra high dots per inch(xxhdpi):** 480pulgadas

#### <o>Carpeta values</o>

Se crean por defecto 3 carpetas  <r>colors, strings, theme</r>.

<b>Strings:</b>  almacena todas las cadenas que se muestran

![String](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/stringXML.png?raw=true)

<b>Color:</b>  a cada estiqueta \<color\> se le asigna un <r>nombre</r> y una referencia <r>\#hexadecimal</r> que es la que representa el color
![Colors](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/colorsXML.png?raw=true)

Al crear un recurso se le pueden dar propiedades adicionales como por ejemplo la nacionalidad y lengua en el caso de un strings
![CrearString](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/CrearRecurso.gif?raw=true)


#### Acceder a los Recursos en Android

**Desde Kotlin:**

Cada identificador se ubica en una clase llamada R a través de una constante entera **R.tipoRecurso.nombreRcurso**. 
![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/AccederRecurso.png?raw=true)

**Desde XML:**

Para ello usamos la sintaxis @[Paquete:]tipoRecurso/nombreRecurso
![AccederRecurso](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/temas/imagenes/AccederRecursoXML.png?raw=true)


### Android Manifest

**<b>Manifest:</b>** Es el archivo más esencial de nuestra aplicación que contiene nodos descriptivos sobre las características de la App como la versión de SDK,permisos necesarios, servicios, activitys.

**<b>Etiqueta aplicacion:</b>**
-<o>allowBackup(true/false):</o>indica si la aplicacion sera persistente al cerrar nuestro AVD.
-<o>icon:</o> indica donde esta ubicado el icono de la aplicación.
-<o> label:</o> Nombre de la aplicación que vera el usuario en su telefono
-<o>theme:</o> apunta al archivo styles.xml donde se define el estilo visual de la aplicación
-<o>supportsRtl:</o> Declara si la aplicacion esta dispuesta a admitir diseños de derecha a izquierda

**<b>Etiqueta activity:</b>**

-<o> label:</o> texto que se mostrara en la cabecera de la actividad
-<o> android:name:</o>
-<o></o>
-<o></o>