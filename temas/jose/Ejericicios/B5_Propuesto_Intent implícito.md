**activity_main.xml**

````kotlin
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <!--Panel 1 Imagen, Nombre y Apellidos -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="0.6"
        android:background="#673AB7">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <!--Panel 1 Imagen-->

            <!--Panel 1 Nombre-->

            <ImageView
                android:id="@+id/imagenCamaraImageView"
                android:layout_width="95dp"
                android:layout_height="121dp"
                android:src="@android:drawable/checkbox_off_background"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.113"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <EditText
                android:id="@+id/nombreEditText"
                android:layout_width="160dp"
                android:layout_height="wrap_content"
                android:hint="Nombre"
                app:layout_constraintBottom_toTopOf="@+id/apellidoEditText"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.597"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintVertical_bias="0.87" />

            <!--Panel 1 Apellidos -->
            <EditText
                android:id="@+id/apellidoEditText"
                android:layout_width="160dp"
                android:layout_height="wrap_content"
                android:hint="Apellido"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.173"
                app:layout_constraintStart_toEndOf="@+id/imagenCamaraImageView"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintVertical_bias="0.701" />

        </androidx.constraintlayout.widget.ConstraintLayout>

    </LinearLayout>
    <!--Panel 2 TextView, CheckBoxs y ImageApellidos -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="0.4"
        android:orientation="vertical">

        <!--Panel 2 TextView-->
        <TextView
            android:id="@+id/etiquetarTextView"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_margin="10dp"
            android:text="Etiquetar como" />

        <!--Panel 2.1 CheckBoxs -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

            <!--Panel 2.1 Familia -->
            <CheckBox
                android:id="@+id/familiaCheckBox"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_margin="10dp"
                android:checked="true"
                android:text="Familia" />

            <!--Panel 2.1 Amigos -->
            <CheckBox
                android:id="@+id/amigosCheckBox"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_margin="10dp"
                android:text="Amigos" />

            <!--Panel 2.1 Trabajo -->
            <CheckBox
                android:id="@+id/trabajoCheckBox"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_margin="10dp"
                android:text="Trabajo" />

        </LinearLayout>

        <!--Panel 3 Tlf boton + imagen -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="20dp"
            android:orientation="horizontal">

            <ImageButton
                android:id="@+id/telefonoImageButton"
                android:layout_width="50dp"
                android:layout_height="50dp"
                android:src="@android:drawable/stat_sys_phone_call" />

            <EditText
                android:id="@+id/telefonoEditText"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="TLF" />

        </LinearLayout>

        <!--Panel 4 Mail boton + imagen -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_margin="20dp"
            android:orientation="horizontal">

            <ImageButton
                android:id="@+id/correoImageButton"
                android:layout_width="50dp"
                android:layout_height="50dp"
                android:src="@android:drawable/ic_dialog_email" />

            <EditText
                android:id="@+id/correoEditText"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:hint="Mail"/>

        </LinearLayout>

    </LinearLayout>

</LinearLayout>
````
**manifest.xml**

````kotlin
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.laurafm.B7.intent_implicito">
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.CALL_PHONE" />
    <uses-permission android:name="android.permission.READ_VOICEMAIL"/>
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Intent_Implicito">

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.SEND" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.SENDTO" />
                <data android:scheme="mailto" />
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.telecom.ConnectionService" />
                <data android:scheme="Tlf"
                    tools:ignore="AppLinkUrlError" />
                <category android:name="android.intent.category.APP_CONTACTS"/>
            </intent-filter>
        </activity>
    </application>

</manifest>
````

**MainActivity.kt**
````kotlin
package com.laurafm.B7.intent_implicito

import android.Manifest.permission.*
import android.app.Activity
import android.app.ActivityManager
import android.content.Intent
import android.content.Intent.ACTION_CALL
import android.content.pm.PackageManager
import android.graphics.Bitmap
import android.net.Uri
import android.os.Build
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.os.Environment
import android.os.Message
import android.provider.MediaStore
import android.view.View
import android.widget.Button
import android.widget.ImageButton
import android.widget.Toast
import androidx.activity.result.ActivityResultCaller
import androidx.activity.result.ActivityResultLauncher
import androidx.activity.result.contract.ActivityResultContracts
import androidx.annotation.RequiresApi
import androidx.core.content.FileProvider
import com.laurafm.B7.intent_implicito.databinding.ActivityMainBinding
import org.w3c.dom.Text
import java.io.File

class MainActivity : AppCompatActivity() {
    @RequiresApi(Build.VERSION_CODES.M)
    private lateinit var binding: ActivityMainBinding
    lateinit var resultadoCamara: ActivityResultLauncher<Intent>



    @RequiresApi(Build.VERSION_CODES.M)
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        val view = binding.root
        setContentView(view)
        solicitarPermisos()
        creaContratos()

        binding.BotonCamaraImageButton.setOnClickListener{
            tomarFoto()
        }
        binding.telefonobuton.setOnClickListener{
            llamada()
        }
        binding.emailbuton.setOnClickListener{
            composeEmail(binding.email.text.toString())
        }
    }
    fun tomarFoto() {
        val cameraIntent = Intent(MediaStore.ACTION_IMAGE_CAPTURE)
        resultadoCamara.launch(cameraIntent)
    }

    @RequiresApi(Build.VERSION_CODES.M)
    fun creaContratos() {
        resultadoCamara =
            registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->
                if (result.resultCode == Activity.RESULT_OK) {
                    binding.BotonCamaraImageButton.setImageBitmap(result.data?.extras?.get("data") as Bitmap)

                }
            }
    }

    @RequiresApi(Build.VERSION_CODES.M)
    fun llamada()
    {
        val intent: Intent =
            Intent(ACTION_CALL, Uri.parse("tel:" + binding.numeroTelefono.text.toString()))
            startActivity(intent)
    }
    fun composeEmail(subject: String) {
        val intent = Intent(Intent.ACTION_SENDTO).apply {
            data = Uri.parse("mailto:")
            putExtra(Intent.EXTRA_SUBJECT, subject)
        }
        if (intent.resolveActivity(packageManager) != null) {
            startActivity(intent)
        }
        else
        {
            println("El campo esta vacio");
        }
    }

    @RequiresApi(Build.VERSION_CODES.M)

        val RESPUESTA_PERMISOS = 111

        @RequiresApi(Build.VERSION_CODES.M)
        fun solicitarPermisos() {
            if (checkSelfPermission(CAMERA) == PackageManager.PERMISSION_DENIED || checkSelfPermission(
                    CALL_PHONE
                ) == PackageManager.PERMISSION_DENIED || checkSelfPermission(READ_VOICEMAIL) == PackageManager.PERMISSION_DENIED
            ) {
                requestPermissions(arrayOf(CAMERA, CALL_PHONE, READ_VOICEMAIL), RESPUESTA_PERMISOS)
            }
        }

        override fun onRequestPermissionsResult(
            requestCode: Int,
            permissions: Array<out String>,
            grantResults: IntArray
        ) {
            super.onRequestPermissionsResult(requestCode, permissions, grantResults)
            when {
                RESPUESTA_PERMISOS == requestCode && grantResults.isNotEmpty() -> {
                    for (i in 0..permissions.size - 1) {
                        if (grantResults[i] == PackageManager.PERMISSION_GRANTED)
                            Toast.makeText(
                                applicationContext, "Permiso Concedido " +
                                        permissions[i], Toast.LENGTH_SHORT
                            ).show()
                    }
                }
            }
        }
    }

````
