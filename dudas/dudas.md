
# dudas

1. me gustaria saber que extension de markdown usais para imprimir los pdfs o mas bien como lo haceis por que no me funciona bien el hihglight {highlight=[4,8,....]} en el pdf que imprimo
![duda1](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/dudas/duda1.png?raw=true)

//PUES TENEMOS MARKDOWN PREVIEW ENHANCED, Que tu ya tenías creo. Sobre el texto de la Preview, pulsamos con el derecho
//del ratón  menú emergente seleccionamos Chrome (Puppeteer) y le damos a PDF
2. **tema 8 pagina 7**   esto por que lo haceis asi
![duda2](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/dudas/duda2.png?raw=true)
en vez de hacerlo asi
//Con el poco código que veo puedo arriesgarme a contestar que es porque le estamos dando un porcentaje a la vista para que ocupe
//solo el 75 por ciento de su contenedor padre,que por lo visto es un linearLayot con orientación horizontal. Tu le dices que ocupe todo
//el ancho del padre, por lo que no cabria la otra vista al lado
![duda2](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/dudas/duda3.png?raw=true)
3. **tema 8 pagina 15** porque usamos el lateinit var en la declaracion de la interface?
![duda3](https://github.com/MarceloSantonja/AndroidApuntes/blob/main/resources/images/dudas/duda4.png?raw=true)
//El lateinit se utiliza porque no se le está dando un valor desde el principio a la propiedad, pero no se hace solo con interfaces se hace con
//cualquier propiedad.
4. he intentado hacer el ejemplo de la pagina 16 y me da error pasando la interface
//te mando un enlace con la corrección, el problema es que creabas un objeto nuevo holder en el return, ahora verás que puedes hacer click sobre
//toda la línea o sobre el nombre

```kt
2022-05-06 00:10:28.634 15678-15678/com.marcelo.ejemplorecyclerview E/AndroidRuntime: FATAL EXCEPTION: main
    Process: com.marcelo.ejemplorecyclerview, PID: 15678
    kotlin.UninitializedPropertyAccessException: lateinit property pasarCadenaInterface has not been initialized
        at com.marcelo.ejemplorecyclerview.Holder.getPasarCadenaInterface(Holder.kt:10)
        at com.marcelo.ejemplorecyclerview.Holder.onClick(Holder.kt:30)
        at android.view.View.performClick(View.java:7448)
        at android.view.View.performClickInternal(View.java:7425)
        at android.view.View.access$3600(View.java:810)
        at android.view.View$PerformClick.run(View.java:28305)
        at android.os.Handler.handleCallback(Handler.java:938)
        at android.os.Handler.dispatchMessage(Handler.java:99)
        at android.os.Looper.loop(Looper.java:223)
        at android.app.ActivityThread.main(ActivityThread.java:7656)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:592)
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:947)


```

```kt
package com.marcelo.ejemplorecyclerview

import android.content.Context
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.Toast
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        val datos = anadirDatos()
        val recyclerView = findViewById<RecyclerView>(R.id.recyclerList)
        val adaptador = Adaptador(datos,this)
        recyclerView.adapter = adaptador
        recyclerView.layoutManager =
            LinearLayoutManager(this, LinearLayoutManager.VERTICAL, true)
//        adaptador.onClick(View.OnClickListener { v ->
//            Toast.makeText(
//                this@MainActivity,
//                "Has pulsado" + recyclerView.getChildAdapterPosition(v),
//                Toast.LENGTH_SHORT
//            ).show()
//        })
//        adaptador.onLongClick(View.OnLongClickListener { v ->
//
//            val posicion = recyclerView.getChildAdapterPosition(v)
//            adaptador.datos.removeAt(posicion)
//            adaptador.notifyItemRemoved(posicion)
//            true
//        })
        adaptador.pasarCadena(object:PasarCadenaInterface {
            override fun pasarCadena(cadena: String) {
                Toast.makeText(applicationContext, "Has pulsado " + cadena, Toast.LENGTH_SHORT).show()
            }
        })
    }

    private fun anadirDatos(): ArrayList<Usuario> {
        var datos = ArrayList<Usuario>()
        for (i in 0..19)
            datos.add(Usuario("nombre$i", "apellido$i apellido$i"))
        return datos
    }
}
```

```kt
package com.marcelo.ejemplorecyclerview

import android.content.Context
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.recyclerview.widget.RecyclerView

class Adaptador (val datos: ArrayList<Usuario>,var contexto: Context) :
    RecyclerView.Adapter<Holder>(), View.OnClickListener, View.OnLongClickListener {
    lateinit var listenerClick: View.OnClickListener
    lateinit var onLongListenerClick: View.OnLongClickListener
    lateinit var pasarCadenaInterface: PasarCadenaInterface

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): Holder {
        val itemView: View = LayoutInflater.from(parent.context)
            .inflate(R.layout.recycler_layout, parent, false)

        val holder = Holder(itemView)
        holder.pasarCadena( object : PasarCadenaInterface {
            override fun pasarCadena(cadena: String) {
                pasarCadenaInterface.pasarCadena(cadena)
            }
        })

        itemView.setOnClickListener(this)
        itemView.setOnLongClickListener(this)
        return Holder(itemView)
    }
    fun pasarCadena(pasarCadenaInterface: PasarCadenaInterface) {
        this.pasarCadenaInterface = pasarCadenaInterface
    }

    override fun onBindViewHolder(holder: Holder, position: Int) {
        val item: Usuario = datos[position]
        holder.bind(item)
    }

    override fun getItemCount(): Int {
        return datos.size
    }

    fun onClick(listener: View.OnClickListener) {
        this.listenerClick = listener
    }

    fun onLongClick(listener: View.OnLongClickListener) {
        this.onLongListenerClick = listener
    }

    override fun onClick(p0: View?) {
        listenerClick.onClick(p0)
    }

    override fun onLongClick(p0: View?): Boolean {
        onLongListenerClick?.onLongClick(p0)
        return true
    }


}

```

```kt
package com.marcelo.ejemplorecyclerview

import android.view.View
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

class Holder(v: View) :RecyclerView.ViewHolder(v), View.OnClickListener {
    val textNombre: TextView
    val textApellido: TextView
    lateinit var pasarCadenaInterface: PasarCadenaInterface

    fun bind(entity: Usuario){
        textNombre.setText(entity.nombre)
        textApellido.setText(entity.apellidos)
    }
    init {
        textNombre = v.findViewById(R.id.textView)
        textApellido = v.findViewById(R.id.textView2)
        textNombre.setOnClickListener(this)
        textApellido.setOnClickListener(this)
    }
    fun pasarCadena( pasarCadenaInterface: PasarCadenaInterface){
        this.pasarCadenaInterface =pasarCadenaInterface
    }

    override fun onClick(p0: View?) {
        var cadena:String
        if(p0?.id==R.id.textView) cadena=textNombre.text.toString()
        else cadena=textApellido.text.toString()
        pasarCadenaInterface.pasarCadena(cadena)
    }



}

```

```kt
package com.marcelo.ejemplorecyclerview

class Usuario(nombre:String, apellidos:String) {

    var nombre: String = nombre
    var apellidos: String = apellidos

}

```

[Enlace a github del proyecto](https://github.com/MarceloSantonja/EjerciciosAndroidMarcelo/tree/main/B8/EjemploRecyclerView)
