# Tema 5. Interfaz de Usuario I

## ViewBinding
- ``findViewById``, permite vincular las vistas de la aplicación con las clases para acceder a determinadas propiedades de los widgets de las
vistas.
- View Binding sirve para enlazar los elementos de los layouts con las clases.
- Configuración del archivo ``build.gradle`` a nivel de ``Module:app`` > Android Studio 4.0.
````
android {
  ...
  viewBinding {
    enabled = true
  }
}
````

- Si ``activity_secundaria.xml`` la clase de vinculación generada se llamará ``ActivitySecundariaBinding``.
- Para poder usarlo hay que hacer en ``onCreate()``:

````
private lateinit var binding: ActivitySecundariaBinding
override fun onCreate(savedInstanceState: Bundle) {
    super.onCreate(savedInstanceState)
    binding = ActivitySecundariaBinding.inflate(layoutInflater)
    val view = binding.root
    setContentView(view)
}
````

## Botones

### Filled, elevated button

### Filled, unelevated button

### Outlined button

### Text button

### Icon button

### Manejar eventos botón

### Toggle Button

### Floating Action Button

### TextInputLayout etiquetas flotantes

### AutoComplete TextView

### Controles de selección

#### CheckBox

#### RadioButton

#### Switches

#### SnackBar

##### SnackBar con acción

##### Descartar SnackBar
