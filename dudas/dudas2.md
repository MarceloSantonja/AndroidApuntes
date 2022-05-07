
# dudas

1. En el ejercicio de pajaros tenemos 2 activity_main con el mismo nombre(uno  para portrait y otro para lanscape) eso no nos da problemas con los ids? **EjericioResueltoPajaros.pdf pagina 3**
2. pila de llamadas al iniciar el progama  :
    1. MainActivity carga el navegador 
       1. navegador portrait
          1. carga dialogfragment o carga fragmente detalle
       2. navegador landscape(si en vez de un dialogFragment cargase un fragment normal esto nos daria problemas el Haber 2 fragments en esta vista?)
          1. carga el dialogfragment  
3. esta bien meter la clase holder dentro de la clase adapter **EjericioResueltoPajaros.pdf pagina 7**
4. Adapter porque se asegura de que la vista no se nula en el onclick? en la explicacion no viene igual **EjericioResueltoPajaros.pdf pagina 7**

````kt
override fun onClick(v: View) {
if (listener != null) listener!!.onClick(v)
}
```

5. diferencia entre findbyId e inflater.inflate() 
//en teoria finbyid te crea una referenciaa una vista existente y el inflater te crea una nueva gerarquia de vistas basadas en ese xml o eso entendi...

[enlace](https://stackoverflow.com/questions/28015060/the-difference-between-layoutinflater-inflate-and-findviewbyid)

6. diferecia entre una propiedad de una propiedad de un fragment y un companion object
// el companion object es igual a una propiedad static de otro lenguaje...

[enlace](https://developer.android.com/kotlin/common-patterns#companion)


7. si las vistas las buscamos por id para que sirve poner el android:name en los xml? para asociarlos a una clase.kt?
