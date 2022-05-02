Cuando selecionemos una u otra nos saldrá un layout u otro cambiando su visibilidad

**MainActivity.kt**
````kotlin
class MainActivity : AppCompatActivity() {


    private lateinit var binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)


        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)

        binding.RadioGroupCliente.setOnCheckedChangeListener { _, checkedId ->

            var layoutParticular = findViewById<LinearLayout>(R.id.LayoutParticular)
            var layoutCorporativo = findViewById<LinearLayout>(R.id.LayoutCorporativo)


            if (checkedId.equals(binding.RadioButtonParticular.id)) {
                layoutParticular.isVisible = true
                layoutCorporativo.isVisible = false
            } else {
                layoutCorporativo.isVisible = true
                layoutParticular.isVisible = false
            }
        }
    }
}
````
**activity_main**
````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/TextViewTipoCliente"
        android:layout_width="107dp"
        android:layout_height="wrap_content"
        android:text="Tipo de cliente"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <RadioGroup
        android:id="@+id/RadioGroupCliente"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:checkedButton="@id/RadioButtonParticular">
        <RadioButton
            android:id="@+id/RadioButtonCorporativo"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Corporativo" />

        <RadioButton
            android:id="@+id/RadioButtonParticular"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Particular"
            android:checked="true"/>
    </RadioGroup>

    <LinearLayout
        android:id="@+id/LayoutParticular"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:visibility="visible">

        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Nombre Completo"/>
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Profesion"/>
    </LinearLayout>

    <LinearLayout
        android:id="@+id/LayoutCorporativo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:visibility="gone">

        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Razón Social"/>
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Representante"/>
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Número de empleados"/>
    </LinearLayout>

</LinearLayout>
````
