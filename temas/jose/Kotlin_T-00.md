# TEORIA Kotlin

# T-00  Kotlin

### Hacer que una variable pueda ser nula
````kotlin
var numeroAnulable:Int?
````
### Llamada segura variable
````kotlin
println(cadenaAnulable?.length)
````
### Asignación nula
Si es nulo salta excepción

````kotlin
println(cadenaAnulable!!.length)
````
### Elvis
?? =  ?:
````kotlin
println(cadenaAnulable?.length?:0)
````
### Usar variables al usar ``println``
````kotlin
  println("$cadena $a + $b es: ${a + b}")
````
### For
````kotlin
for(i in (0..v).reversed()) println("$i")
````
### Do-While
````kotlin
var contador:Int=0
do{
    var numero=readLine()!!.toInt();
    contador++;
}
while(contador<tope && numero!in 1..100)
````
### When
``When`` con argumentos
````kotlin
fun getEstacion(entrada:Int):String
{
return when(entrada)
{
    1-> "primavera"
    2-> "verano"
    3-> "otoño"
    4-> "invierno"
    else -> "Estación incorrecta"
}
}
````
``When`` sin argumentos
````kotlin
fun noHagoNada(x:Int, s:String, v:Float):String
{
  val res = when {
      x in 1..10 -> "entero positivo menor de 10"
      s.contains("cadena") -> "incluyo cadena"
      v is Comparable<*>-> "Soy Comparable"
      else -> ""
  }
  return res
}
````
### Funciones

``fun nombreFuncion([nombreVariable:Tipo, nombreVariable:Tipo, ... ]):TipoDevolucion``
### Devolver valor usando alternativa a ternaria
````Kotlin
return if(numeroUno>numeroDos) numeroUno else numeroDos
````
### Funciones de extensión
Añadir funciión ``Escribe()`` a ``String``
````kotlin
String.Escribe()=println(this);
main() {"Soy una cadena".Escribe()}
````

### Clases e Interfaces
````kotlin
class ExcepcionEdad(cadena:String):Exception(cadena){}
class Persona //Constructor vacío
{
  val nombre:String
  get() = field.toUpperCase()
  //Field pertenece a nombre, devolviéndolo en mayúsculas
  var edad: Int=0
  set(value)
    {
      if(value <0 || value>125) throw ExcepcionEdad("Edad Invalida")
      else field = value
    }
}
````
### Uso de init
````kotlin
class Persona(nombre:String, var edad:Int=0)
{
  val nombre:String
  get() {
    return field.toUpperCase()
  }
//Init hace referencia al constructor principal  
init{
    this.nombre=nombre
    if(edad<0 || edad>125) throw ExcepcionEdad("Edad Invalida")
    else this.edad=edad
  }
}
````
### Segundo constructor usando propiedades del primero
````Kotlin
//this(nombre, edad) son las propiedades del constructor anterior
constructor(nombre:String, edad:Int=0, dni:String):this(nombre, edad)
  {
    this.dni=dni
  }
````

### Herencia
Clase padre ``Persona``
````kotlin
//open Hacer clase open para que pueda ser heredada
open class Persona(nombre:String, var edad:Int=0)
````
Clase hija ``Estudiante``
````kotlin
class Estudiante(nombre:String, edad:Int=0, var estudios:String):Persona(nombre, edad)
````
#### Hacer propiedad reescribible
Clase padre ``Persona``
````kotlin
open class Persona(nombre:String, var edad:Int=0)
{
  open var dni:String="NINGUNO"
  ...
  open fun imprimir()= println("Nombre: $nombre Edad: $edad")
  fun esMayor() = if (edad >= 18) true else false
}
````
Clase hija ``Estudiante``
````kotlin
class Estudiante(nombre:String, edad:Int=0, var estudios:String):Persona(nombre, edad)
{
  override var dni:String="ESTUDIANTE SIN DNI"
  override fun imprimir()
  {
    super.imprimir();
    println("Soy estudiante de $estudios")
  }
}
````

## Interfaces
Hacer interfaz ``IEstudios``
````kotlin
interface IEstudios
{
  var curso: Int // Propiedad abstracta
  val ultimoCurso: Boolean // Propiedad regular
      get() = curso ==2
  fun estudios():String // Método abstracto
  fun soyEstudiante() { // Método regular
    println("Soy Estudiante de " +estudios())
}
````
Implementar interfaz ``IEstudios``
````kotlin
class Estudiante(nombre:String, edad:Int=0, >var estudios:String):Persona(nombre, edad)
{
  override var curso:Int=0
    set(value) {field=curso}
  override var dni:String="ESTUDIANTE SIN >DNI"
  override fun estudios()= estudios
  }
````
## Clases Enum (No se usarán mucho)
Declarar **enumeración**
````Kotlin
enum class CiclosInformatica {SMR, ASIR, DAM, DAW}
````
### Valor en las enumeraciones
````Kotlin
enum class CiclosInformatica( val valor: Int, val grado: String)
{
  SMR(1,"Grado Medio"),
  ASIR(2,"Grado Superior"),
  DAM(3,"Grado Superior"),
  DAW(4,"Grado Superior")
}
fun main()
{
  for(v in CiclosInformatica.values()) println(v.name+" "+ v.ordinal)
  //it para hacer referencia a los campos
  CiclosInformatica.values().forEach{println("${it.valor} - ${it.name} - ${it.grado}")}
}
````
### Enumeraciones con comportamiento
````Kotlin
enum class CiclosInformatica( val valor: Int, val grado: String, val nombre : String)
{
  SMR(1,"Grado Medio","Sistemas Microinformáticos y Redes"),
  ASIR(2,"Grado Superior","Administración de Sistemas Informáticos en Red"),
  DAM(3,"Grado Superior","Desarrollo de Aplicaciones Multiplataforma"),
  DAW(4,"Grado Superior","Desarrollo de Aplicaciones Web");

  fun informacionCompleta()= "${name} - ${nombre} - ${grado}"
}
fun main()
{
  CiclosInformatica.values().forEach{println("${it.informacionCompleta()}")}
}
````
## Clases y métodos parametrizados
### Clases Genéricas
````kotlin
class ClaseGenerica<T>(t: T, c:String)
````
Crear objeto tipo entero
````Kotlin
val objeto=ClaseGenerica(3, "Hola")
````
Hacer restricción del tipo parametrizado
````Kotlin
class ClaseGenerica<T: Comparable<T>>(t: T, c:String)
````
### Funciones Genéricas
````Kotlin
fun <T> funcionGenerica(param: T): T {
return param
}
````
## Colecciones
### Listas
- **arrayOf**
  * Array de objetos tradicional
  * arrayOf(1, 2, 3)
  * No es inmutable
  * No puede modificarse longitud
- **arrayListOf**
  * Lista mutable
  * arrayListOf(1,
2, 3)
  * No es inmutable
  * Puede modificarse longitud

### Arrays
````kotlin
val weekDays = arrayOf("primavera", "verano", "otoño", "invierno")
for (dato in weekDays) println(dato) //Similar al foreach de C#
for (i in weekDays.indices) println(weekDays.get(i)) //Acceso mediante índice
for ((posicion, valor) in weekDays.withIndex()) //Volcando ambos datos en una tupla
  println("La posición $posicion contiene el valor $valor")
````
Clase ``Persona``
````kotlin
class Persona(val nombre: String, val edad: Int)
{
  fun imprimir()= println("Nombre: $nombre Edad: $edad")
  fun esMayor() = if (edad >= 18) true else false
}
````
Función ``Main``
````Kotlin
fun main()
{
  val personas=arrayOfNulls<Persona>(2)
  personas.set(0,Persona("Ana",12))
  personas.get(0)?.imprimir()
}
````
#### Array Bidimensional
````kotlin
val matriz = Array(4) { IntArray(4) }
matriz[1][1]=3
for (e in matriz) println(e.contentToString())
````
Diferentes columnas

````Kotlin
val dentada = arrayOfNulls<IntArray>(3) //Tres filas
dentada[0] = IntArray(2)
dentada[1] = IntArray(3) //Tamaño de columnas
dentada[2] = IntArray(4)

for(i in 0..dentada.size-1)
for(j in 0..dentada[i]!!.size-1) dentada[i]?.set(j, 3)
//Inicializar valor a 3
````
Matriz con 1 en diagonal

````Kotlin
val matriz = Array(4) { f -> IntArray(4) { c -> if(f==c)1 else 0 } }
````

### Listas Mutables

Lista mutable tipo ``Persona``
````kotlin
val personas=ArrayList<Persona>()
personas.add(Persona("Ana",12))
personas.add(Persona("Pedro", 15))
for(p in personas) p.imprimir()
````
Opciones para las Listas

````Kotlin
val personas=ArrayList<Persona>()
personas.add(Persona("Ana",12))
personas.add(Persona("Pedro", 15))
personas.add(Persona("Rosa",13))
personas.add(Persona("Andrea",15))
val itr = personas.iterator ()
while (itr.hasNext ()) itr.next().imprimir()
personas.forEach{it.imprimir()}
````
Filtrar y recorrer

````kotlin
personas.filter{it.edad==15}.forEach{it.imprimir()}
````

### Mapas (Diccionarios)

````kotlin
val personas = mutableMapOf<String, Persona>()

personas["21456874L"] = Persona("Ana",12)
personas["13232345K"]=Persona("Luis", 13)
personas.forEach{print(it.key + " ")
                it.value.imprimir()}
````
Introducir elementos en mapa mutable
````Kotlin
val personas = mutableMapOf<String, Persona>(Pair("21456874L", Persona("Ana",12)),
                                             Pair("13232345K",Persona("Luis", 13)))
personas+=Pair("24568947L", Persona("Pedro",15))
personas+=Pair("25412321L", Persona("Laura",12))
//Filtramos por nombres que comienzan por L y contamos
println(personas.filter{ it.value.nombre.startsWith('L') }.size)
// Lo mismo que antes pero usando coutn
println(personas.count { it.value.nombre.startsWith('L') })
````
Recorrer usando tuplas

````kotlin
for((dni,valor) in personas)
  {
    print(dni)
    valor.imprimir()
  }
````
