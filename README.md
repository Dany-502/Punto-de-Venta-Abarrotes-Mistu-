# Punto-de-Venta-Abarrotes-Mistu-

# Indice
- [Autores](#Autores)
- [Descripcion del proyecto](#Descripcion_del_proyecto)
- [Requisitos](#Requisitos)
- [Interfaces creadas](#Interfaces_creadas)
- [Clases auxiliares](#Clases_auxiliares)
- [librerias usadas](#Librerias_usadas)
- [Instrucciones de implementación](#Instrucciones_de_implementación)
- [Video explicativo](#Video-explicativo)

# Autores
-- _Rodriguez Juarez Jose Daniel_

-- _Alonso Heredia Miguel Alberto_

# Descripcion del proyecto
Este proyecto es un sistema de gestión para mini-supermercados desarrollado en Java Netbeans que integra módulos para administrar productos, usuarios y ventas. Permite registrar y editar productos con control de inventario, gestionar usuarios con roles específicos (administrador, cajero, almacenista) y validaciones de seguridad (contraseñas encriptadas, formatos de correo), además de procesar ventas generando tickets en PDF y enviando confirmaciones por correo. Utiliza interfaces graficas, se conecta a una base de datos PostgreSQL, e incluye funcionalidades como búsquedas dinámicas, validación de datos en tiempo real y generación de reportes, todo diseñado para optimizar y automatizar las operaciones de pequeños comercios de manera segura y eficiente.

# Requisitos 

1.- Java JDK 8 o superior (Version JDK recomendada: 18).

2.- Apache Netbeans IDE 20.

3.- Conexión a internet.

# Interfaces creadas 

## Pantalla de Inicio de Sesión  
La clase IntfzInicioScion es la interfaz gráfica de usuario (GUI) que permite a los usuarios iniciar sesión en el sistema. Está implementada en Java Swing y conectada a una base de datos donde se valida que el correo electrónico y la contraseña coincidan con un usuario registrado.

### Vista de la interfaz
![InicioSesion](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/InicioSesion.png)

### Caracteristicas principales
- Valida credenciales (correo y contraseña) contra la base de datos PostgreSQL.
- Muestra mensajes de error si los campos están vacíos o las credenciales son incorrectas.
- Al iniciar sesión correctamente, almacena el nombre y rol del usuario en la clase UsuarioSesion
- Redirige al Menu_Principal según el rol
- Utiliza la clase ConexionBaseDatos para establecer la conexion con la base de datos principal.
- Consulta la tabla usuarios con filtros por correo y contraseña.

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
![MenuPrincipal](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/MenuPrincipal.png)

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
![usuarios](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/Usuarios.png)

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

## Interfaz para editar usuario
Esta interfaz permite modificar datos de usuarios existentes. Recibe los datos actuales del usuario (nombres, apellidos, teléfono, etc.) y permite editarlos, validando que todos los campos estén completos antes de actualizar la base de datos. Al guardar los cambios, regresa a la ventana de gestión de usuarios (Usuarios) y muestra confirmación de la operación.

### Vista de la interfaz
![EditarUsuarios](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/EditarUsuario.png)

### Caracteristicas principales 
1.-Interfaz gráfica:
- Campos para editar: apellidos, nombres, teléfono, fecha de nacimiento y correo
- Selector de fecha (dateFecha) con formato "yyyy-MM-dd"
- Botones para: guardar cambios, cancelar y regresar

2.-Funcionalidad principal:
- Actualiza registros en la tabla usuarios mediante consultas parametrizadas
- Usa el idUsuario como clave para identificar el registro a modificar

3.-Navegación:
- Redirección a Usuarios (tras edición exitosa)
- Opción de cancelar y volver al Menu_Principal

### ¿Como funciona?
1.-Inicialización:
- Recibe los datos actuales del usuario en el constructor
- Rellena automáticamente los campos del formulario

2.-Edición:
- El usuario modifica los campos necesarios
- Al hacer clic en "Editar": Valida que todos los campos tengan datos. Prepara y ejecuta la consulta SQL de actualización. Muestra confirmación/error

3.-Resultado:
- Si es exitoso: cierra el formulario y recarga la lista de usuarios
- Si falla: muestra mensaje de error específico

### Validaciones
1.-Campos obligatorios:
- Verifica que ningún campo esté vacío (validarCampos())
- Incluye validación de fecha seleccionada

2.-SQL:
- Uso de PreparedStatement para evitar inyecciones
- Conversión segura de tipos (especialmente fechas)

3.-Retroalimentacion:
- Mensajes claros cuando faltan datos
- Confirmación explícita de actualización exitosa

### Dependencias
● Librerias usadas para crear el JFrame:
- _javax.swing:_ Para componentes gráficos
- _java.awt:_ Para manejo de eventos y colores
- _java.sql:_ Para conexión con base de datos

● Clases que se relacionan con el JFrame:
- _ConexionBaseDatos:_ Gestión de conexiones SQL
- _Usuarios:_ Ventana de gestión de usuarios
- _Menu_Principal:_ Retorno al menú
  
## Interfaz de Caja
La interfaz caja es un módulo de punto de venta (POS) que gestiona transacciones comerciales, permitiendo seleccionar productos, calcular totales y generar tickets en PDF. Implementa control de inventario en tiempo real, validación de stock y búsqueda de productos. Incluye funciones para modificar pedidos y conexión directa con la base de datos para actualizar existencias.

### Vista de la interfaz
![Caja](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/Caja.png)

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
● Librerias usadas para crear el JFrame:
- _javax.swing:_ Para componentes gráficos
- _java.awt:_ Para manejo de eventos y colores
- _java.sql:_ Para conexión con base de datos
- _itextpdf:_ Generación de tickets PDF (con logo, formato profesional)
- _java.desktop:_ Para abrir PDF automáticamente

● Clases que se relacionan con el JFrame:
- _ConexionBaseDatos:_ Gestión de conexiones SQL
- _Menu_Principal:_ Retorno al menú

## Interfaz para agregar producto
Esta interfaz permite registrar nuevos productos en el sistema. Ingresa nombre, descripción, precio y cantidad, validando que los campos estén completos y los valores numéricos sean correctos antes de insertarlos en la base de datos. Tras agregar el producto, limpia los campos y redirige al menú principal, mostrando confirmación de la operación.

### Vista de la interfaz
![AgregarProducto](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/IngresarProducto.png)

### Caracteristicas principales 
1.-Interfaz gráfica:
- Contiene campos para: nombre, descripción, precio y cantidad del producto
- Tiene botones para: agregar, limpiar campos y cerrar/regresar

2.-Operaciones:
- Inserta nuevos registros en la tabla productos mediante consultas parametrizadas
- Usa try-with-resources para manejo automático de conexiones

### ¿Como funciona?
1.-Inicialización:
- Muestra formulario vacío listo para capturar datos

2.-Registro:
- Usuario ingresa datos del producto
- Al hacer clic en "Agregar": Valida campos obligatorios. Verifica formato numérico en precio/cantidad. Ejecuta inserción SQL si todo es válido

3.-Resultado:
- Muestra confirmación de éxito o error específico
- Limpia campos tras inserción exitosa
- Redirige al Menu_Principal

4.-Opciones disponibles:
- "Limpiar": Vacía todos los campos
- "Cerrar": Regresa al menú principal sin guardar

### Validaciones
1.-Campos obligatorios:
- Nombre, precio y descripción no pueden estar vacíos (validarCampos())

2-Formatos numéricos:
- Precio debe ser un double válido
- Cantidad debe ser un entero (int)

3.-Feedback:
- Mensajes claros cuando faltan datos o hay formatos inválidos
- Confirmación explícita de registro exitoso

### Dependencias
● Librerias usadas para crear el JFrame:
- _javax.swing:_ Para componentes gráficos
- _java.awt:_ Para manejo de eventos y colores
- _java.sql:_ Para conexión con base de datos

● Clases que se relacionan con el JFrame:
- _ConexionBaseDatos:_ Gestión de conexiones SQL
- _Menu_Principal:_ Retorno al menú

## Interfaz para editar producto
Esta interfaz permite modificar productos existentes en el sistema. Recibe los datos actuales del producto (ID, nombre, descripción, precio y cantidad) y permite editarlos, validando que todos los campos estén completos y los valores numéricos sean correctos antes de actualizar la base de datos. Al guardar los cambios, regresa al menú principal mostrando confirmación de la operación.

### Vista de la interfaz
![EditarProducto](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/bad2b1593a0bd219a307e70c8ea56c806cdce229/Build/EditarProducto.png)

### Caracteristicas principales 
1.-Interfaz gráfica:
- Campos pre-llenados con los datos actuales del producto
- Botones para: guardar cambios, cancelar y cerrar

2-Operaciones:
- Actualiza registros en la tabla productos mediante consultas parametrizadas
- Usa el idArticulo como clave para identificar el producto a modificar

### ¿Como funciona?
1.-Inicialización:
- Recibe los datos actuales del producto en el constructor
- Pre-llena los campos del formulario

2.-Edición:
- Usuario modifica los campos necesarios
- Al hacer clic en "Editar": Valida campos obligatorios. Verifica formatos numéricos. Ejecuta actualización SQL si todo es válido

3.-Resultado:
- Muestra confirmación de éxito/error
- Redirige al menú principal tras operación exitosa

### Validaciones
1.-Campos obligatorios:
- Nombre, descripción, precio y cantidad no pueden estar vacíos

2.-Formatos numéricos:
- Precio debe ser un valor decimal válido (double)
- Cantidad debe ser un entero válido (int)

3.-Retroalimentacion:
- Mensajes claros para campos vacíos o formatos inválidos
- Confirmación explícita de actualización exitosa

### Dependencias
● Librerias usadas para crear el JFrame:
- _javax.swing:_ Para componentes gráficos
- _java.awt:_ Para manejo de eventos y colores
- _java.sql:_ Para conexión con base de datos

● Clases que se relacionan con el JFrame:
- _ConexionBaseDatos:_ Gestión de conexiones SQL
- _Menu_Principal:_ Retorno al menú

# Clases auxiliares
## ConexionBaseDatos
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConexionBaseDatos {
    private static final String URL = "jdbc:postgresql://localhost:5432/minisupermitsuuu";
    private static final String USER = "postgres";
    private static final String PASSWORD = "miguelito159a";

    static {
        try {
            // Carga el driver de PostgreSQL al iniciar la clase
            Class.forName("org.postgresql.Driver");
        } catch (ClassNotFoundException e) {
            throw new RuntimeException("Error: Driver PostgreSQL no encontrado", e);
        }
    }

    public static Connection conectar() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}
```
La clase ConexionBaseDatos es utilizado para gestionar conexiones a una base de datos PostgreSQL. Utiliza el patrón Singleton implícito a través de métodos estáticos y carga el driver JDBC de PostgreSQL durante la inicialización de la clase. Establece y retorna una nueva conexión usando las credenciales predefinidas.

## EncriptarContraseñas
```java
package Validaciones;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
/**
 *
 * @author migue
 */
public class Encriptar {
    public static String hashSHA256(String textoPlano) {
        try {
            MessageDigest digest = MessageDigest.getInstance("SHA-256");
            byte[] hash = digest.digest(textoPlano.getBytes("UTF-8"));

            // Convertir el array de bytes a una representación en hexadecimal
            StringBuilder hexString = new StringBuilder();
            for (byte b : hash) {
                hexString.append(String.format("%02x", b));
            }
            return hexString.toString();

        } catch (Exception ex) {
            throw new RuntimeException("Error al encriptar contraseña", ex);
        }
    }
}
```
La clase Encriptar sirve para convertir texto plano en un hash seguro , generando una cadena hexadecimal de 64 caracteres irrevertible. Esto protege datos sensibles almacenándolos de forma cifrada en bases de datos, evitando que se lean directamente si hay un acceso no autorizado.

## PDF_Registro
```java
import com.itextpdf.text.Chunk;
import com.itextpdf.text.Document;
import com.itextpdf.text.Element;
import com.itextpdf.text.Font;
import com.itextpdf.text.Image;
import com.itextpdf.text.Paragraph;
import com.itextpdf.text.pdf.PdfWriter;

import java.io.FileOutputStream;

public class PDF_registro {

    public static String generarPDF(String nombre, String usuario, String contrasena, String rutaCompletaArchivo) {
        try {
            Document documento = new Document();
            PdfWriter.getInstance(documento, new FileOutputStream(rutaCompletaArchivo));
            documento.open();

            // Fuente para el título
            Font fontTitulo = new Font(Font.FontFamily.HELVETICA, 18, Font.BOLD);
            Paragraph titulo = new Paragraph("Cuenta Mistu Abarrotes", fontTitulo);
            titulo.setAlignment(Element.ALIGN_CENTER);
            documento.add(titulo);

            documento.add(Chunk.NEWLINE); // Espacio

            // Imagen - asegúrate que la imagen esté en la ruta correcta dentro del proyecto
            Image imagen = Image.getInstance(PDF_registro.class.getResource("/imagenes/LogoTienda-removebg-preview.png"));
            imagen.scaleToFit(150, 150);
            imagen.setAlignment(Element.ALIGN_CENTER);
            documento.add(imagen);

            documento.add(Chunk.NEWLINE); // Espacio debajo de la imagen

            // Contenido del PDF
            documento.add(new Paragraph("Hola " + nombre + ","));
            documento.add(new Paragraph("Gracias por registrarte en Mi Tienda de Abarrotes."));
            documento.add(new Paragraph(" "));
            documento.add(new Paragraph("Tus credenciales de acceso son:"));
            documento.add(new Paragraph("Usuario: " + usuario));
            documento.add(new Paragraph("Contraseña: " + contrasena));

            documento.close();

        } catch (Exception e) {
            e.printStackTrace();
        }

        return rutaCompletaArchivo;
    }
}
```
La clase PDF_registro genera un documento PDF con los datos de registro de un usuario (nombre, usuario y contraseña), incluyendo un título, el logo de la tienda y un mensaje de bienvenida. Utiliza la biblioteca iTextPDF para crear el archivo en la ruta especificada, formateando el contenido con estilo profesional (alineación centrada, saltos de línea y fuente destacada para el título).

## SoloLetras
```java
package Validaciones;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import javax.swing.JTextField;
/**
 *
 * @author HP
 */
public class SoloLetras {
    public static void validarLetras(JTextField campoTexto){
        campoTexto.addKeyListener(new KeyAdapter() {
            @Override
            public void keyTyped(KeyEvent e) {
                char c = e.getKeyChar();
                if (!Character.isLetter(c) && c != KeyEvent.VK_BACK_SPACE && c != KeyEvent.VK_SPACE) {
                    e.consume(); 
                }
            }
        });
    }
}
```
La clase SoloLetras es un validador que restringe la entrada en campos de texto (JTextField) para aceptar únicamente letras, espacios y la tecla de borrado (backspace). Implementa un KeyListener que intercepta cada tecla presionada y bloquea (mediante e.consume()) cualquier carácter que no sea alfabético, asegurando que no se puedan ingresar números o símbolos accidentalmente.

## ValidarCorreoContra
```java
package Validaciones;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class ValidarCorreoContra {
    public static boolean validarCorreo(String correo){
        String expresion = "^[a-zA-Z0-9_+&*-]+@(yahoo|outlook|gmail|hotmail|itoaxaca)\\.(com|mx|edu(\\.mx)?)$";
        Pattern pattern = Pattern.compile(expresion);
        Matcher matcher = pattern.matcher(correo);   
    return matcher.matches();
}
    public static boolean validarContra(String contra){
        String expresion = "[a-zA-Z0-9]{8}";
        Pattern pattern = Pattern.compile(expresion);
        Matcher matcher = pattern.matcher(contra);   
        return matcher.matches();
    }
    
}
```
La clase ValidarCorreoContra proporciona dos métodos estáticos para validar formatos:

- validarCorreo(): Verifica si un correo electrónico cumple con el patrón usuario@dominio.extensión, aceptando dominios comunes (Gmail, Yahoo, Outlook, etc.) y extensiones (.com, .mx, .edu.mx).

- validarContra(): Valida que una contraseña tenga exactamente 8 caracteres alfanuméricos (letras y números, sin símbolos).
Ambos métodos usan expresiones regulares (regex) para garantizar que los datos ingresados cumplan con los formatos requeridos, devolviendo true o false según corresponda. Ideal para formularios de registro o login.

## ValidarMinusculas
```java
package Validaciones;
import javax.swing.text.*;
/**
 *
 * @author HP
 */
public class ValidarMinusculas extends DocumentFilter {
    @Override
    public void insertString(FilterBypass bypass, int posicion, String texto, AttributeSet atributos) throws BadLocationException {
        bypass.insertString(posicion, texto.toLowerCase(), atributos);
    }
    @Override
     public void replace(FilterBypass bypass, int posicion, int longitud, String texto, AttributeSet atributos) throws BadLocationException {
        bypass.replace(posicion, longitud, texto.toLowerCase(), atributos);
    }
}
```
Esta clase es un filtro de texto que fuerza la conversión a minúsculas en tiempo real para cualquier texto ingresado en un componente Swing (como JTextField). Hereda de DocumentFilter y sobrescribe los métodos insertString() y replace() para transformar automáticamente los caracteres a minúsculas antes de insertarlos.

# Librerias usadas
## Generador Captcha
1.- Función: Implementa sistemas de verificación CAPTCHA para distinguir usuarios humanos de bots.

2.-Características clave:
-  Integración en formularios web para prevenir spam y automatización.

## Generador de PDF
1.- Función: Crear y manipular documentos PDF de forma programática.

2.-Características clave:

- Soporta fuentes personalizadas, estilos y alineación.
- Permite añadir logos, marcas de agua y firmas digitales.
- Usada en comprobantes, reportes y documentos legales.

## Envio de correos
1.- Función: Enviar correos electrónicos desde aplicaciones Java.

2.-Características clave:
- Envío con autenticación OAuth2 o contraseñas de aplicación (ej: Gmail).
- Soporte para adjuntos, HTML en el cuerpo y correos masivos.
- Usada en confirmaciones de registro, notificaciones y recuperación de contraseñas.

# Instrucciones de implementación 
## 1.-Descargar y descomprimir el archivo .zip 
![paso1](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/a34c9e94f14b160bac15c357c20a675719e3078b/Build/Paso1.png)

## 2.-Abrir netbeans y buscar en la interfaz de opciones "abrir proyecto"
![paso2](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/a34c9e94f14b160bac15c357c20a675719e3078b/Build/Paso2.png)

## 3.-Busca el proyecto en tus archivos y abrelo.
![paso3](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/a34c9e94f14b160bac15c357c20a675719e3078b/Build/Paso3.png)

## 4.-Una vez abierto te pedira incorporar las librerias utilizadas para crear el proyecto.
![paso4](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/a34c9e94f14b160bac15c357c20a675719e3078b/Build/Paso4.png)

## 5.-Simplemente incorporalos con las librerias que vienen en el archivo zip
![paso5](https://github.com/Dany-502/Punto-de-Venta-Abarrotes-Mistu-/blob/a34c9e94f14b160bac15c357c20a675719e3078b/Build/Paso5.png)

# Video Explicativo
https://youtu.be/7m6rwbPrW9w
