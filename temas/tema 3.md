<style>
r { color: Red }
o { color: Orange }
g { color: Green }
b { color: Blue }
</style>

# [Tema 3](tema3_Componentes_Aplicacion.pdf)

## Componentes de una aplicación

<b>Activity:</b>Las Activitys son los componentes visibles de la aplicación, tienen una interface de usuario que permite interactuar con ellas.

<b>Services:</b> Un servicio es una entidad que ejecuta instrucciones en segundo plano sin que el usuario lo note en la interfaz.

<b>View:</b>Las vistas (view) son los componentes básicos con los que se construye la interfaz gráfica de la aplicación.

<b>Fragment:</b> Los fragmentos (fragment) se pueden entender como secciones o partes (habitualmente reutilizables)

<b>Widget:</b>Los widgets son elementos visuales, normalmente interactivos, que pueden mostrarse en la pantalla principal del dispositivo Android y recibir actualizaciones periódicas.

<b>Content provider:</b>Con el componente Content Provider,se puede almacenar datos en un fichero, en una base de datos SQLite, **estos datos pueden ser compartidos entre distintas aplicaciones**. Una clase que implemente el componente Content Provider contendrá una serie de métodos que permite almacenar, recuperar, actualizar y compartir los datos de una aplicación.

<b>Intents:</b>Es un **objeto de mensajería** que facilita la comunicación entre componentes.

<b>Broadcast receiver:</b>**Reaccionan a intents específicos pudiendo a su vez ejecutar una acción** o iniciando una activity.

## Ciclo de vida de una Activity
Como hemos comentado en el punto anterior. La activity es uno de los componentes esenciales de
una aplicación Android, además que es el componente que tiene asociada la interfaz de usuario.
Una misma aplicación puede tener una o varias actividades y Android permite controlar por
completo el ciclo de vida de cada una de estas. Los estados por los cuales puede pasar una Activity son los siguientes: Creación, Ejecución,
Reanudación, Pausa, Parada y Destrucción.
