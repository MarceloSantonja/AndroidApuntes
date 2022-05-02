Al presionar un botón añadimos +1 al número del circulo
**MainActivity.kt**
````kotlin
class MainActivity : AppCompatActivity() {
    @SuppressLint("CutPasteId")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<Button>(R.id.añadirCarro).setOnClickListener()
        {
            val valor : String = findViewById<TextView>(R.id.numeroArticulos).text.toString()
            val valorNumerico : Int = Integer.parseInt(valor)
            findViewById<TextView>(R.id.numeroArticulos).text = (valorNumerico + 1).toString()
        }
    }
}
````

**activity_main.xml**
````xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="#009688">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center|left"
            android:layout_marginLeft="5dp"
            android:text="Contenedor de productos"
            android:textColor="#FFFFFF"
            android:textSize="20dp" />

        <ImageView
            android:layout_width="48dp"
            android:layout_height="52dp"
            android:layout_gravity="right"
            android:src="@drawable/ic_baseline_shopping_cart_24" />

        <TextView
            android:id="@+id/numeroArticulos"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="right"
            android:background="@drawable/rounded_back"
            android:text="0"
            android:textAlignment="center"
            android:textColor="#FFFFFF"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            tools:ignore="RtlCompat" />

    </FrameLayout>

    <Button
        android:id="@+id/añadirCarro"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:backgroundTint="#848C93"
        android:text="Agregar Producto" />

</FrameLayout>

````

**Añadir y usar forma**

- **rounded_back.xml** -> Carpeta Drawable
````xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">
    <solid android:color="#ea0d0d"/>
    <size android:height="20dp"
        android:width="20dp"/>
</shape>
````

- **activity_main.xml**
````xml
android:background="@drawable/rounded_back"
````

**theme.xml** - Quitar toolbar
````xml
    <style name="Theme.Carrito" parent="Theme.MaterialComponents.DayNight.NoActionBar">
````
**MainActivity.kt**

````kotlin
package com.example.carrito

import android.annotation.SuppressLint
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import org.w3c.dom.Text

class MainActivity : AppCompatActivity() {
    @SuppressLint("CutPasteId")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        findViewById<Button>(R.id.añadirCarro).setOnClickListener()
        {
            val valor : String = findViewById<TextView>(R.id.numeroArticulos).text.toString()
            val valorNumerico : Int = Integer.parseInt(valor)
            findViewById<TextView>(R.id.numeroArticulos).text = (valorNumerico + 1).toString()
        }
    }
}
````
