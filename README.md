# Punto-de-Venta-Abarrotes-Mistu-

# Indice
- [Autores](#Autores)
- [Explicación general](#Explicación-general)
- [Requisitos previos](#Requisitos-previos)
- [Explicación del codigo](#Explicación-del-codigo)
- [Instrucciones para importar el .jar y el JSON](#Instrucciones-para-importar-el-jar-y-el-JSON)
- [Video explicativo](#Video-explicativo)

# Autores
-- _Rodriguez Juarez Jose Daniel_

-- _Alonso Heredia Miguel Alberto_

# ¿En que consiste nuestro proyecto?


# Requisitos 

1.- Java JDK 8 o superior (Version JDK recomendada: 18).

2.- Apache Netbeans IDE 20.

3.- Conexión a internet.

# Explicación de cada interfaz creada 

## Pantalla de Inicio de Sesión  
La clase IntfzInicioScion es la interfaz gráfica de usuario (GUI) que permite a los usuarios iniciar sesión en el sistema. Está implementada en Java Swing y conectada a una base de datos donde se valida que el correo electrónico y la contraseña coincidan con un usuario registrado.

### Vista de la interfaz

### Caracteristicas principales


### Dependencias 
  ●	_Base de datos:_ Requiere conexión activa con una tabla usuarios que contenga las columnas correo_electronico, contrasena, nombres y rol.

  ●	_Clases externas:_
  
  - ConexionBaseDatos: para conectar con la BD.
  - Menu_Principal: ventana principal del sistema.
  - UsuarioSesion: clase que gestiona los datos del usuario logueado.

  
## Interfaz de registro de usuario
La clase Registrarse es una interfaz gráfica (Java Swing) para registrar nuevos usuarios al sistema. Permite la captura, validación y almacenamiento de los datos del usuario en una base de datos, así como la generación de un PDF con sus credenciales y el envío automático de un correo de confirmación.

### Vista de la interfaz

### Caracteristicas principales 
●	Validación de campos obligatorios y formato.

●	Verificación de que el correo no haya sido registrado previamente.

●	Validación de contraseña segura y confirmación.

●	Captcha integrado para validar el registro.

●	Generación automática de PDF con credenciales.

●	Envío automático de correo electrónico con adjunto.

●	Limpieza del formulario tras el registro.

●	Redirección a la pantalla de menú de usuarios (Usuarios).

### ¿Como funciona?
1.- El usuario completa el formulario

2.- Al hacer clic en "Registrarse":

- Se validan todos los campos
- Si son válidos, se inserta el usuario en la BD
- Se envía correo de confirmación
- Se limpia el formulario y se redirige a la ventana de usuarios

3.- Si hay errores, se muestran mensajes al usuario.

### Validaciones
● Valida que todos los campos obligatorios estén completos

● Verifica formato de correo electrónico y fortaleza de contraseña

● Confirma que las contraseñas coincidan

● Valida que solo se ingresen letras en nombres y apellidos

### Dependencias
● Librerías utilizadas:
- SoloLetras: Clase que verifica que solo se ingresen letras en un txt
- ValidarCorreoContra: Clase que verifica un correo valido.
- JavaMail: Es utilizado para enviar el correo de confirmación.
- toedter.calendar.JDateChooser: Utilizado para el selector de fecha.

● Componentes visuales personalizados:
- LIB.JPanelRound: Paneles que permiten agregar mas colores y formas
- CaptchaPanel: Sirve para verificar si el usuario que está interactuando con una página web o aplicación es una persona real, y no un bot o programa automatizado
- PDF_registro: Permite crear archivos pdf con contendio personalizado


## Menu Principal
Menu_Principal es la interfaz principal del sistema Mi Tienda de Abarrotes, diseñada en Java Swing. Esta clase permite la visualización y gestión de productos en inventario, realizando operaciones como: Mostrar todos los productos registrados, buscar productos por ID o nombre, Agregar, editar y eliminar productos, navegar hacia otras secciones (usuarios, ventas), restringir funcionalidades según el rol del usuario

### Vista de la interfaz

### Caracteristicas principales 
1.-Interfaz gráfica:
- Ventana principal del sistema (hereda de JFrame)
- Muestra una tabla con productos (JTproductos)
- Contiene botones para: agregar, editar, eliminar productos, realizar ventas, gestionar usuarios y salir
- Muestra el nombre y rol del usuario actual

2.-Control de acceso por roles:
- Restringe funcionalidades según el rol del usuario (Administrador, Almacenista, Cajero)
- Deshabilita botones y muestra mensajes de acceso restringido

3.-Gestión de productos:
- Muestra lista completa de productos desde la base de datos
- Permite operaciones CRUD (Crear, Leer, Actualizar, Eliminar)

4.-Integración con otras ventanas:
- Redirección a las siguientes ventanas: agregar, editar, caja y usuarios

### ¿Como funciona?
Al ser el menú principal, este contiene varias funciones:

1.-Inicializacion:
- Al crearse la ventana, carga los datos del usuario actual (UsuarioSesion)
- Muestra los productos en la tabla (mostrarDatos())
- Configura los permisos según el rol (opcionRol())

2.-Interacciones que puede hacer el usuario:
- Agregar: Abre ventana para agregar nuevos productos
- Editar: Abre ventana de edición con datos del producto seleccionado
- Eliminar: Confirma y elimina el producto seleccionado
- Venta: Abre módulo de caja/ventas
- Usuarios: Abre gestión de usuarios (solo para administradores)
- Salir: Confirma y cierra la aplicación

       Al abrir otras ventanas, cierra la ventana actual (dispose())
       Al salir, termina la aplicación (System.exit(0))

### Validaciones 
1.-Selección de productos:
- Verifica que se haya seleccionado un producto antes de editar/eliminar
- Muestra mensajes de advertencia si no hay selección

2.-Confirmaciones:
- Pide confirmación antes de eliminar productos
- Pide confirmación antes de salir de la aplicación

3-Control de acceso:
- Valida el rol del usuario para habilitar/deshabilitar funciones
- Muestra mensajes de "Acceso Restringido" para funciones no permitidas

### Dependencias 
● Librerias usadas para crear el JFrame:
- _javax.swing:_ Para componentes gráficos
- _java.awt:_ Para manejo de eventos y colores
- _java.sql:_ Para conexión con base de datos
- _java.math.BigDecimal:_ Para manejo de valores monetarios y cantidades

● Clases que se relacionan con el JFrame:
- _Agregar:_ Ventana para añadir productos
- _Editar:_ Ventana para modificar productos
- _Caja:_ Módulo de ventas
- _Usuarios:_ Gestión de usuarios


## Interfaz de control de Usuarios
Interfaz que gestiona los usuarios registrados en el sistema, mostrando datos en una tabla con opciones para agregar, editar y eliminar registros. Este se conecta a la base de datos para cargar y modificar información, implementa validaciones de selección y confirmaciones antes de eliminar, además, redirige a otros JFrame como Registrarse y EditarUsuario.

### Vista de la interfaz

### Caracteristicas principales
1.-Interfaz gráfica:
- Ventana de gestión de usuarios
- Muestra una tabla (tablaUsuarios) con todos los usuarios registrados
- Contiene botones para: agregar, editar, eliminar usuarios y regresar al menú principal
- La tabla muestra: ID, apellidos, nombres, teléfono, fecha de nacimiento y correo

2.-Operaciones disponibles:
- _Agregar:_ Abre formulario de registro (Registrarse)
- _Editar:_ Abre formulario de edición (EditarUsuario) con datos del usuario seleccionado
- _Eliminar:_ Elimina usuarios con confirmación previa

3.-Integración de la base de datos:
- Conexión a tabla usuarios en la base de datos
- Mapeo de columnas específicas (fechas como java.sql.Date)

4.-Integración con otras ventanas:
- Redirección a las siguientes ventanas: agregarUsuario, editar, y menu principal

### ¿Como funciona?
1.-Inicialización:
- Al abrirse, carga y muestra todos los usuarios (mostrarDatos())
- Configura la tabla con tipos de datos específicos por columna

2.-Interacciones que puede hacer el usuario:
- Agregar: Abre ventana de registro y cierra la actual
- Editar: Valida que se haya seleccionado un usuario. Pasa todos los datos a la ventana de edición. Cierra la ventana actual
- Eliminar: Valida selección. Pide confirmación. Si se confirma, elimina el usuario y actualiza la tabla
- Cerrar: Regresa al menú principal

### Validaciones
1.-Selección de usuarios:
- Verifica que se haya seleccionado un usuario antes de editar/eliminar
- Muestra mensajes de advertencia si no hay selección

2.-Confirmaciones:
- Pide confirmación explícita antes de eliminar usuarios
- Muestra detalles del usuario a eliminar (nombre e ID)

3.-Integridad de datos:
- Conversión segura de tipos al extraer valores de la tabla
- Manejo de errores SQL con mensajes descriptivos

### Dependencias
● Librerias usadas para crear el JFrame:
- _javax.swing:_ Para componentes gráficos
- _java.awt:_ Para manejo de eventos y colores
- _java.sql:_ Para conexión con base de datos

● Clases que se relacionan con el JFrame:
- _Registrarse:_ Formulario de registro de nuevos usuarios
- _EditarUsuario:_ Formulario para modificar usuarios existentes
- _Menu_Principal:_ Ventana principal del sistema
- _ConexionBaseDatos:_ Maneja la conexión a la base de datos

  
## Interfaz de Caja
La interfaz caja es un módulo de punto de venta (POS) que gestiona transacciones comerciales, permitiendo seleccionar productos, calcular totales y generar tickets en PDF. Implementa control de inventario en tiempo real, validación de stock y búsqueda de productos. Incluye funciones para modificar pedidos y conexión directa con la base de datos para actualizar existencias.

### Vista de la interfaz

### Caracteristicas principales 
1.-Interfaz gráfica:
- Tabla de productos disponibles con búsqueda por ID/nombre
- Tabla de pedido actual con cantidades y subtotales
- Calculadora automática de totales
- Botones para: confirmar venta, cancelar, modificar pedido y regresar

2.-Gestión de ventas:
- Sistema de doble-clic para agregar productos con validación de stock
- Modificación de cantidades en pedidos existentes
- Generación de tickets PDF con numeración automática

3.-Integración con la base de datos:
- Actualización automática de inventario al confirmar ventas
- Búsqueda dinámica con filtros combinados (ID + nombre)

4.-Componentes especiales:
- Listener para cálculo automático de totales
- Formateo profesional de tickets (logo, fecha localizada, alineación)

### ¿Como funciona?
1.-Inicialización:
- Carga todos los productos disponibles al abrirse
- Configura listener para cálculo automático de totales

2.-Proceso de venta:
- Agrega productos: Dar doble click, ingresar producto → validación de stock
- Modificar producto: Seleccionar producto, ajustar cantidades o eliminar
- Confirmar cambios: Actualiza inventario en BD. Genera PDF con ticket. Reinicia interfaz para nueva venta

3.-Buscar producto:
- Filtra productos por ID o nombre

### Validaciones
1.-Stock:
- Impide agregar más unidades de las disponibles
- Verifica disponibilidad antes de confirmar venta

2.-Datos:
- Valida formatos numéricos en cantidades
- Maneja casos de productos nulos o sin selección

3.-Confirmaciones:
- Pide confirmación para operaciones críticas (eliminar productos)

4.-Errores:
- Mensajes claros para problemas de stock/conexión BD

### Dependencias
