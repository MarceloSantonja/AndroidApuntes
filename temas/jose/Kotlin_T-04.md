## Paleta de colores

``colors.xml``

````xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="purple_200">#FFBB86FC</color>
    <color name="purple_500">#FF6200EE</color>
    <color name="purple_700">#FF3700B3</color>
    <color name="teal_200">#FF03DAC5</color>
    <color name="teal_700">#FF018786</color>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
</resources>
````

- Una vez descargado el archivo hay que copiarlo a la carpeta ``res/values`` sustituyendo el archivo de configuración de colores predeterminado por el nuevo.

- Necesario reasiganar los name a los colores para hacerlos coincidir en archivo ``res/values/styles.xml``.

## Layouts

### LinearLayout

### Temas y estilos

- Para el ejemplo del LinearLayout
themes.xml
````xml

<resources xmlns:tools="http://schemas.android.com/tools">
<!-- Base application theme. -->
<style name="Theme.EjemploLinearLayout"
    parent="Theme.MaterialComponents.DayNight.DarkActionBar">
    <!-- Primary brand color. -->
    <item name="colorPrimary">@color/purple_500</item>
    <item name="colorPrimaryVariant">@color/purple_700</item>
    <item name="colorOnPrimary">@color/white</item>
    <!-- Secondary brand color. -->
    <item name="colorSecondary">@color/teal_200</item>
    <item name="colorSecondaryVariant">@color/teal_700</item>
    <item name="colorOnSecondary">@color/black</item>
    <!-- Status bar color. -->
    <item name="android:statusBarColor" tools:targetApi="l">
        ?attr/colorPrimaryVariant
    </item>
    <!-- Customize your theme here. -->
</style>
<style name="Theme.EjemploLinearLayoutPropio"
    parent="Theme.MaterialComponents.DayNight.DarkActionBar">
    <!-- Primary brand color. -->
    <item name="colorPrimary">#F44336</item>
    <item name="colorPrimaryVariant">#D32F2F</item>
    <item name="colorOnPrimary">@color/black</item>
    <!-- Secondary brand color. -->
    <item name="colorSecondary">#F06292</item>
    <item name="colorSecondaryVariant">#F48FB1</item>
    <item name="colorOnSecondary">@color/black</item>
    <!-- Status bar color. -->
    <item name="android:statusBarColor" tools:targetApi="l">
        ?attr/colorPrimaryVariant
    </item>
    <!-- Customize your theme here. -->
</style>
</resources>
````

- Modificar ``AndroidManifest.xml ``

````xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.example.ejemplolinearlayout">
<application
    android:allowBackup="true"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:roundIcon="@mipmap/ic_launcher_round"
    android:supportsRtl="true"
    android:theme="@style/Theme.EjemploLinearLayoutPropio">
    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
</manifest>
````
