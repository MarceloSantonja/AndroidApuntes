# Dudas 3

1. Quisiera saber que tiene de especial un Framelayout (he visto que es un layout que suele tener solo un hijo y que puede tener mas puestos orientados por gravity) ? es como un cardview? esta anticuado o tiene utilidad?
** El FrameLayout puede tener tantos hijos como quiera, pero pone uno sobre otro, alineados a la parte de arriba a la izq. Se pueden alinear cada uno con las propiedades de layoutgravity como dices. El CardView hereda de este, pero se le puede dar elevación y redondear bordes. Se puede usar para cuando quieres poner una vista sobre otra y así haces visible o invisible la que quieras en cada momento.
3. se usa mucho el Exposed dropdown menu? en el tema 9 se explica vagamente porque esta explicado en otro tema,  tambien he visto videos por ahi que lo explican decentemente, es importante?... porque no me parece que se vaya a usar mucho eso teniendo otros menus. 
** Ese se explica en los temas iniciales y es el AutocompleteTextView, pero es mejor que le des importancia al resto (al poput no)
4. no encuentro la manera de que me salga el icon de hamburguesa en el ejercicio de ejemplo de el navigation drawer **tema9 pagina 11**
// al final lo he arreglado con :

```kt
supportActionBar?.setDisplayHomeAsUpEnabled(true)
```
**Eso se explica cuando se da ToolBar, también en los temas de inicio

codigo reducido ActivityMain:

```kt
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        navigationView= binding.navigationView
        drawer_layout = binding.drawerLayout

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
        toggle = ActionBarDrawerToggle(this,drawer_layout,R.string.navivigation_open,R.string.navivigation_close)
        drawer_layout.addDrawerListener(toggle)
        supportActionBar?.setDisplayHomeAsUpEnabled(true)

    }
    override fun onPostCreate(savedInstanceState: Bundle?, persistentState: PersistableBundle?) {
        super.onPostCreate(savedInstanceState, persistentState)
        toggle.syncState()
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        if(toggle.onOptionsItemSelected(item)){
            return true
        }
        return super.onOptionsItemSelected(item)
    }
```

codigo del ejemplo:

````kt
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        navigationView= binding.navigationView
        drawer_layout = binding.drawerLayout
        toolbar=binding.topAppBar

        navigationView.setNavigationItemSelectedListener(this)
        setSupportActionBar(toolbar)
        toggle = ActionBarDrawerToggle(this,drawer_layout,R.string.navivigation_open,R.string.navivigation_close)
        drawer_layout.addDrawerListener(toggle)
        supportActionBar?.setDisplayHomeAsUpEnabled(true)

    }

    override fun onPostCreate(savedInstanceState: Bundle?, persistentState: PersistableBundle?) {
        super.onPostCreate(savedInstanceState, persistentState)
        toggle.syncState()
    }

    override fun onConfigurationChanged(newConfig: Configuration) {
        if (newConfig !=null){
            super.onConfigurationChanged(newConfig)
        }
        toggle.onConfigurationChanged(newConfig)

    }

    override fun onNavigationItemSelected(item: MenuItem): Boolean {
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
        return true
    }

    override fun onOptionsItemSelected(item: MenuItem): Boolean {
        if(toggle.onOptionsItemSelected(item)){
            return true
        }
        return super.onOptionsItemSelected(item)
    }

```
