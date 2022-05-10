
# dudas

1. En el ejercicio de pajaros tenemos 2 activity_main con el mismo nombre(uno  para portrait y otro para lanscape) eso no nos da problemas con los ids? **EjericioResueltoPajaros.pdf pagina 3**
 
3. esta bien meter la clase holder dentro de la clase adapter **EjericioResueltoPajaros.pdf pagina 7**
4. Adapter porque se asegura de que la vista no sea nula en el onclick? en la explicacion no viene igual **EjericioResueltoPajaros.pdf pagina 7**

```kt
override fun onClick(v: View) {
if (listener != null) listener!!.onClick(v)
}
```

5. diferencia entre findbyId e inflater.inflate() 
//en teoria finbyid te crea una referenciaa una vista existente y el inflater te crea una nueva gerarquia de vistas basadas en ese xml o eso entendi...
// xusa: inflater es para inflar el xml entero y el findbyid sirve para los elementos de un xml... 




[enlace](https://stackoverflow.com/questions/28015060/the-difference-between-layoutinflater-inflate-and-findviewbyid)

1. diferecia entre una propiedad de un fragment y un companion object
// el companion object es igual a una propiedad static de otro lenguaje se puede acceder a ella llamando directamente a la clase...

[enlace](https://developer.android.com/kotlin/common-patterns#companion)

7. si las vistas las buscamos por id para que sirve poner el android:name en los xml? para asociarlos a una clase.kt?

// cuando queremos carga un fragment estatico(es decir que nunca se va a cambiar) en una vista se el name/ y cuando es la navegacion para declarar el navhostFragment

8. comunicacion por interfaces...


9. lista de conceptos importantes....
