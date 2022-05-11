# Menus

- [Menus](https://developer.android.com/guide/topics/ui/menus?hl=es)

## tipos y  propiedades XML

### tipos

- **[OverFlow Menu](#crear-overflow-menu):** menu principal 
- **[Contextual Menu](#crear-context-menu):** menu que se abre con pulsación larga sobre los elementos (textView,button,ext...) a los que se lo pongamos 
- **PopupMenu:** menu vinculado a un elemento de la vista.
- **Navigation Drawer:** menu deslizante de [Material Desing](https://material.io/components/navigation-drawer#usage),se suele encontrar en la pantalla principal...

### Propiedades XML

**\<item\>**:

- **android:showAsAction:** muestra el icono,el titulo o ambas en la cabecera(dependiendo de su valor "ifRoom","withText","never","always","collapseActionView").
- **android:id , android:icon y android:title:** estos son los mas habituales

**\<group\>(dar propiedades a un grupo de items)**:

- **android:checkableBehavior:** hace seleccionables todos("all"), uno("single") o ninguno("none") de los elementos del grupo.
- **android:visible, android:enabled**

## Crear OverFlow Menu

- New > Drawable resource File >>>  
- File Name: ...
- Resource type : Menu

### Añadir items en el xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu
xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/option_1"
          android:title="@string/option_1"/>
    <item android:id="@+id/option_2"
          android:title="@string/option_2"/>
    ...
    <group android:id="@+id/group1_1">
        <item android:id="@+id/group_op1"
              android:title="@string/group_op1"/>
        <item android:id="@+id/group_op2"
              android:title="@string/group_op2"/>
    </group>
</menu>
```

### sobreescribir **onCreateOptionsMenu** y **onOptionsItemSelected** en la activity o fragment que queremos que se muestre Ej.MainActivity.kt

```kt
override fun onCreateOptionsMenu(menu: Menu): Boolean {
    val inflater: MenuInflater = menuInflater
    inflater.inflate(R.menu.menu_overflow, menu)
    return true
}
```

```kt
override fun onOptionsItemSelected(item: MenuItem): Boolean {
    Toast.makeText(this,
            "Pulsaste la opción de menú ${item.toString()}",
            Toast.LENGTH_SHORT).show()
    return true
}

```

- **onPrepareOptionsMenu(menu: Menu?):** nos se llama cada vez que se abre el menu y nos permite hacer modificaciones

```kt
override fun onPrepareOptionsMenu(menu: Menu?): Boolean {
    //add item
    menu.add()
    //add menu
    menu.addSubMenu()
    return super.onPrepareOptionsMenu(menu)
}
```

## Crear Context Menu

> Creamos los objetos a los vamos a asignar los menus Ej: un Button y un textView

### Crear 2 menus:

> res/menu/menu_contextual_textview

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/op12"
    android:title="12" />
    <item android:id="@+id/op16"
    android:title="16" />
    <item android:id="@+id/op20"
    android:title="20" />
    <item android:id="@+id/op24"
    android:title="24" />
</menu>
```

> res/menu/menu_contextual_button

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/opRojo"
    android:title="Rojo" />
    <item android:id="@+id/opAzul"
    android:title="Azul" />
    <item android:id="@+id/opVerde"
    android:title="Verde" />
</menu>
```

```kt {highlight=[9,10]}
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)

        registerForContextMenu(binding.button)
        registerForContextMenu(binding.text)
    }
    override fun onCreateContextMenu(
        menu: ContextMenu?,
        v: View?,
        menuInfo: ContextMenu.ContextMenuInfo?
    ) {
        super.onCreateContextMenu(menu, v, menuInfo)
        if (v!!.id == R.id.text) {
            menuInflater.inflate(R.menu.menu_contextual_textview, menu)
        }
        if (v!!.id == R.id.button) {
            menuInflater.inflate(R.menu.menu_contextual_button, menu)
        }
    }

    override fun onContextItemSelected(item: MenuItem): Boolean {
        when (item.itemId) {
            R.id.op12 -> binding.text.textSize = 12F
            R.id.op16 -> binding.text.textSize = 16F
            R.id.op20 -> binding.text.textSize = 20F
            R.id.op24 -> binding.text.textSize = 24F
            R.id.opAzul -> binding.button.setBackgroundColor(BLUE)
            R.id.opRojo -> binding.button.setBackgroundColor(RED)
            R.id.opVerde -> binding.button.setBackgroundColor(GREEN)
        }
        return super.onContextItemSelected(item)
    }
```

- **Líneas 9,10:** Registramos los ids de las vistas en las que queremos el menu
- **onCreateContextMenu:**infla la lista de opciones del menu correspondiente

## PopMenu

### Crear Menu

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/opSms"
        android:title="@string/opSms"
        android:icon="@drawable/outline_share_24"/>
    <item android:id="@+id/opMail"
        android:title="@string/opMail"
        android:icon="@drawable/outline_email_24"/>
</menu>
```

### Codigo kotlin

```kt
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)

        binding.buttton.setOnClickListener {
            showPopup(binding.buttton)
        }
    }
    private fun showPopup(view: View) {
        val popup = PopupMenu(this, view)
        popup.inflate(R.menu.menu_pop)
        popup.setOnMenuItemClickListener { item: MenuItem? ->
            when (item!!.itemId) {
                R.id.opMail -> {
                    Toast.makeText(this@MainActivity, item.title, Toast.LENGTH_SHORT)
                        .show()}
                R.id.opSms -> {
                    Toast.makeText(this@MainActivity, item.title, Toast.LENGTH_SHORT)
                        .show()}
            }
            true
        }
        popup.show()
    }
```

- el when no hace nada pero lo dejo porque lo he practicado poco

## Navigation Drawer

