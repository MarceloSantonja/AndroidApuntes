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

### activityMain xml

```xml{highlight=[8,23,26,28-29]}
<androidx.drawerlayout.widget.DrawerLayout
  xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  xmlns:tools="http://schemas.android.com/tools"
  android:id="@+id/drawer_layout"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  tools:openDrawer="start"
  tools:context=".MainActivity">
  <androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent">
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hello World!"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"/>
  </androidx.constraintlayout.widget.ConstraintLayout>
  <com.google.android.material.navigation.NavigationView
    android:id="@+id/navigation_view"
    android:layout_width="wrap_content"
    android:layout_height="match_parent"
    android:layout_gravity="start"
    android:fitsSystemWindows="true"
    app:headerLayout="@layout/drawer_header"
    app:menu="@menu/drawer_menu" />
</androidx.drawerlayout.widget.DrawerLayout>
```

- **Linea 8:** herramienta para ver el menu mientras se diseña
- **Linea 23:** id para inchar el navigationView
- **Linea 26:** es donde se posiciona el menu
- **Linea 28:** layout de la cabecera asociada al menu
- **Linea 29:**  archivo xml que establece la vista del menu

### layout drawer_header XML

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout 
xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical">
    <ImageView
        android:layout_width="90dp"
        android:layout_height="90dp"
        android:src="@drawable/ic_baseline_recommend_24" />
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Drawer header"
        android:textSize="20dp"/>
</LinearLayout>
```

### menu drawer_menu

```xml{highlight=[5]}
<?xml version="1.0" encoding="utf-8"?>
<menu 
  xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    tools:showIn="navigation_view" >
    <group android:checkableBehavior="single">
        <item
            android:id="@+id/nav_camera"
            android:icon="@drawable/outline_photo_camera_24"
            android:title="Camera" />
        <item
            android:id="@+id/nav_gallery"
            android:icon="@drawable/outline_photo_library_24"
            android:title="Gallery" />
    </group>
    <group
        android:id="@+id/group1"
        android:checkableBehavior="single">
        <item
            android:id="@+id/nav_manage"
            android:icon="@drawable/outline_build_24"
            android:title="Tools" />
    </group>
    <item android:title="Group">
        <menu>
            <group android:checkableBehavior="single">
                <item
                    android:id="@+id/nav_share"
                    android:icon="@drawable/outline_share_24"
                    android:title="Share" />
                <item
                    android:id="@+id/nav_send"
                    android:icon="@drawable/outline_send_24"
                    android:title="Send" />
            </group>
        </menu>
    </item>
</menu>
```

-**Linea 5:** "tool" para ver la vista.

### activityMain.kt

```kt{highlight=[14,19,20]}
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    private lateinit var drawer_layout: DrawerLayout
    private lateinit var toggle: ActionBarDrawerToggle
    private lateinit var navigationView:NavigationView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        navigationView= binding.navigationView
        drawer_layout = binding.drawerLayout
        toggle = ActionBarDrawerToggle(this,
            drawer_layout,
            R.string.navivigation_open,
            R.string.navivigation_close)
        
        drawer_layout.addDrawerListener(toggle)
        supportActionBar?.setDisplayHomeAsUpEnabled(true)
        
        navigationView.setNavigationItemSelectedListener{ item ->
            val id = item.itemId
            var s=""
            when (id) {
                R.id.nav_camera -> s="CAMARA"
                R.id.nav_gallery-> s="GALLERY"
                R.id.nav_manage-> s="TOOLS"
                R.id.nav_send-> s="SEND"
                R.id.nav_share-> s="SHARE"
            }
            drawer_layout.closeDrawer(GravityCompat.START)
            Toast.makeText(applicationContext,"Pulsaste la opción "+s,
                Toast.LENGTH_SHORT).show()
             true
        }
    }
```

- **Línea 14:** boton hamburguesa
 
