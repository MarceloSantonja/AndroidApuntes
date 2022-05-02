Una actividad con 2 botones que cada uno lanza una actividad y cuando pinchamos en el texto, nos devuelve un toast de que actividad estabamos.

**MainActivity.kt** - Actividad 1
````kotlin

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)


        val openPostActivity =
            registerForActivityResult(ActivityResultContracts.StartActivityForResult())
            { result ->
                if (result.resultCode == Activity.RESULT_OK) {
                    Toast.makeText(
                        applicationContext,
                        result.data?.getStringExtra("DATORETURN"),
                        Toast.LENGTH_SHORT
                    ).show()
                }
            }
        findViewById<TextView>(R.id.activity2_button).setOnClickListener(
            View.OnClickListener {
                openPostActivity.launch(
                    Intent(applicationContext, Activity2::class.java).apply
                    {
                        putExtra(
                            "DATOS",
                            "Este es el valor que se manda desde Main a la Actividad 2"
                        )
                    })
            })
        findViewById<TextView>(R.id.activity3_button).setOnClickListener(
            View.OnClickListener {
                openPostActivity.launch(
                    Intent(applicationContext, Activity3::class.java).apply
                    {
                        putExtra(
                            "DATOS",
                            "Este es el valor que se manda desde Main a la Actividad 3"
                        )
                    })
            })


    }
}
````

**Actividad2.kt** - Actividad 2
````kotlin
class Activity2 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity2)
        val intento = intent
        Toast.makeText(
            applicationContext, intento.getStringExtra("DATOS"), Toast.LENGTH_SHORT
        ).show()


        findViewById<TextView>(R.id.textoActivity2).setOnClickListener(){
            val intentoResultado = Intent()
            intentoResultado.putExtra("DATORETURN", "Vengo de Actividad 2")
            setResult(Activity.RESULT_OK, intentoResultado)
            finish()
        }
    }
}
````

**Actividad3.kt** - Actividad 3
````Kotlin
class Activity3 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity3)
        Toast.makeText(
            applicationContext, "Este es el valor que se manda desde la actividad 3"
            , Toast.LENGTH_SHORT
        ).show()

        findViewById<TextView>(R.id.textoActivity3).setOnClickListener(){
            val intentoResultado = Intent()
            intentoResultado.putExtra("DATORETURN", "Vengo de la Actividad 3")
            setResult(Activity.RESULT_OK, intentoResultado)
            finish()
        }
    }
}
````
**Layouts de las actividades**
**activity_main.xml** - Layout 1
````xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#FF9800"
    android:orientation="horizontal"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/activity3_button"
        android:layout_width="186dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center|right"
        android:text="actividad dos" />

    <Button
        android:id="@+id/activity2_button"
        android:layout_width="186dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center|left"
        android:text="actividad uno" />


</androidx.coordinatorlayout.widget.CoordinatorLayout>
````
**activity2.xml** - Layout 2
````xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:background="#AB86ED">

    <TextView
        android:id="@+id/textoActivity2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Actividad 1"
        android:textSize="30dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
````
**activity3.xml** - Layout 3
````xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:background="#BFED8A">

    <TextView
        android:id="@+id/textoActivity3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Actividad 2"
        android:textSize="30dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
````

**Añadir al Manifest.xml**
````xml
<activity android:name=".Activity2" />
<activity android:name=".Activity3" />
````

