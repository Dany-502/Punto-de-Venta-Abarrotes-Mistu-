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
●	Librerías personalizadas:

	SoloLetras, ValidarCorreoContra, PDF_registro

●	UI personalizados:

	LIB.JPanelRound, LIB.JTexfieldPH_FielTex, CaptchaPanel, etc.

●	Librerías externas:

    JavaMail para envío de correo.

    toedter.calendar.JDateChooser para el selector de fecha.


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
Al si
