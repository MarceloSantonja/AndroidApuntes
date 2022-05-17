# tema 11 Persistencia

1. **Ejercicio resuelto BD** :en el ejercicio me a costado mucho buscar un metodo que me **actualice los DATOS del ReciclerView**, cada vez que meto un dato nuevo y le doy al boton mostrar cargo todos los datos de la base de datos tendria que  haber usado un ViewModel con un mutableLiveData o eso no se puede usar con recyclerView?? 

```kt
        findViewById<Button>(R.id.buttonMostrar).setOnClickListener { view->

            datos = bdAdapter.seleccionarDatosCodigo(
                arrayOf("dni", "nombre", "apellidos"),
                null,
                null,
                "apellidos")?:ArrayList<Cliente>()

            recyclerView.adapter=Adaptador(datos)

        }
        findViewById<Button>(R.id.buttonAdd).setOnClickListener {
            val dni = findViewById<EditText>(R.id.editTextDni).text.toString()
            val nombre = findViewById<EditText>(R.id.editTextNombre).text.toString()
            val apellidos = findViewById<EditText>(R.id.editTextApellidos).text.toString()
            val cliente = Cliente(dni,nombre,apellidos)
            bdAdapter.insertContentValues(cliente)
        }
```

2. para un spinner necesitamos un layout??? **Tema 11 pagina 14 uso de SimpleCursorAdapter**