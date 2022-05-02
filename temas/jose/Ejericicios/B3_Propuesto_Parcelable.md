IMCOMPLETO
Actividad donde rellenamos los datos y al pulsar el botón nos dirige a otra actividad en otro proyecto

- Hacer una clase ``Persona`` que estará en una ``libreriaPersona``
**Persona.kt**

````kotlin
package com.jose.b5.personalibrary

import android.os.Parcel
import android.os.Parcelable

//Parcelable es similar a serializable solo que en este caso se hace heredando
class Persona() : Parcelable
{

    var dni: String
    var nombre: String
    var edad: Int

    constructor(parcel: Parcel) : this() {
        dni = parcel.readString().toString()
        nombre = parcel.readString().toString()
        //Este constructor saca propiedades y las asigna
        // con esto nos saldrá persona.object o parecido, debemos de override el toString();
        // parcel.readString()!! tambien puede funcionar, en caso de no funcionar lanza excepcion;
        edad = parcel.readInt()
    }
    init {
        dni = ""
        nombre = ""
        edad = 0
    }

    constructor(dni: String, nombre: String, edad: Int) : this() {
        this.dni = dni
        this.nombre = nombre
        this.edad = edad
    }

    override fun writeToParcel(parcel: Parcel, flags: Int) {
        parcel.writeString(dni)
        parcel.writeString(nombre)
        parcel.writeInt(edad)
        //no debe modificarse ya que va por posiciones primero nombre y luego edad
    }

    override fun describeContents(): Int {
        return 0
    }

    companion object CREATOR : Parcelable.Creator<Persona> {
        override fun createFromParcel(parcel: Parcel): Persona {
            return Persona(parcel)
        }

        override fun newArray(size: Int): Array<Persona?> {
            return arrayOfNulls(size)
        }
    }

    override fun toString(): String {
        return "$dni $nombre $edad"
        //Es mejor usar la de arriba, pero debe de ponerse $ delante de cada variable

    }
}
````
