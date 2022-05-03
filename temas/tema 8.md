<style>
o { color: Orange }
</style>
<o>* Destacar tipos o composión</o>

# [Tema 8](tema8_Interfaz_Usuario_III.pdf)

## Spinner

Es una listas desplegables que muestras los elementos una vez pulsada la flecha de despliegue, el usuario puede seleccionarlos.

```xml
 <Spinner
        android:id="@+id/spinner"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />
```

Es necesario crear una estructura de elementos que podamos asociar a éste como un Array de Strings para luego asignarlo al spinner:

```kt
var colores = arrayOf("Rojo","Verde","Azul")
```

A continuación debemos definir el adaptador, en nuestro caso un objeto. ArrayAdapter, que será el objeto que lanzaremos con nuestro Spinner.

```kt
 val adaptador =ArrayAdapter(this,            
 android.R.layout.simple_list_item_1, colores) 
```

Parámetros:

1. **this:** El contexto, referencia a la actividad donde se crea el adaptador.
2. **android.R.layout.simple_list_item_1 :** El ID del layout sobre el que se mostrarán los datos del control.En este caso le pasamos el ID de un layout predefinido en Android (android.R.layout.simple_spinner_item), formado únicamente por un control textView, pero podríamos pasar el ID de cualquier layout de nuestro proyecto con cualquier estructura y conjunto de controles.
3. **colores:** El elemento que contiene los datos a mostrar.

Con estas simples líneas tendremos un control similar al de la siguiente imagen:

![image1](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image1.png?raw=true)

![image2](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image2.png?raw=true)

> 🎓 Vamos a crea un proyecto de ejemplo llamado Spinner al que
> añadiremos el siguiente código en la **MainActivity.kt**, y no olvides añadir un spinner con *id=spinner* en el layout **activity_main.xml**:

```kt {highlight=[8,11,12]}

class MainActivity : AppCompatActivity(), 
                     AdapterView.OnItemSelectedListener
                      {
    var colores = arrayOf("Rojo", "Verde", "Azul") 
    lateinit var listaColores: Spinner 
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState) setContentView (R.layout.activity_main)
        val adaptador = ArrayAdapter(this,android.R.layout.
                                        simple_list_item_1,colores)
        listaColores = findViewById(R.id.spinner)
        listaColores.adapter = adaptador
        listaColores.setOnItemSelectedListener(this)
    }

```

> 📌**Línea 8** creamos el adaptador, como hemos explicado anteriormente,
para asignarlo al Spinner en la **Línea 11**.
>En cuanto a los eventos lanzados por el control Spinner, el más utilizado será el generado al seleccionarse una opción de la lista desplegable, onItemSelected.
> Para capturar este evento se procederá de forma similar a lo ya visto para otros controles anteriormente, asignándole su controlador mediante el método **setOnItemSelectedListener()** , en este caso lo hacemos mediante el método de derivar de la interfaz, **Línea 12**. 
> En el código inferior vemos implementado el método, que muestra un Toast con el color elegido.

```kt
        override fun onItemSelected(adapterView: AdapterView<*>?,
                                    view: View?, i: Int, l: Long){
            val x = Toast.makeText(this, "El color elegido es: " +
                    colores[i], Toast.LENGTH_LONG)
            x.show()
        }
```

### Pagina 3



```xml

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="colores">
        <item>ROJO</item>
        <item>VERDE</item>
        <item>AZUL</item>
    </string-array>
</resources>

```






 ![image10](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image10.png?raw=true)

> ![image11](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image11.png?raw=true)

> ![image12](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image12.png?raw=true)

> ![image17](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image17.png?raw=true)


![image19](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image19.png?raw=true)


![image21](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/T8/image21.png?raw=true)