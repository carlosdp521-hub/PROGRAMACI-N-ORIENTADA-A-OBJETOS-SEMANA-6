# Biblioteca JDBC - Proyecto Java con MySQL

Este proyecto corresponde a una aplicación de consola desarrollada en **Java** utilizando **Programación Orientada a Objetos**, **JDBC**, **Maven** y **MySQL**. Su objetivo es gestionar libros de una biblioteca mediante operaciones CRUD: registrar, listar, actualizar y eliminar libros.

---

## 1. Requisitos previos

Antes de ejecutar el proyecto, verifica que tengas instalado lo siguiente:

- **Java JDK 17 o superior**
- **Visual Studio Code**
- **Extension Pack for Java** en VS Code
- **Maven**
- **MySQL Server**, **MySQL Workbench**, **XAMPP** o **phpMyAdmin**

Para comprobar Java y Maven, abre una terminal y ejecuta:

```bash
java -version
mvn -version
```

Si alguno de los comandos no funciona, debes instalar o configurar la variable de entorno correspondiente.

---

## 2. Abrir el proyecto en Visual Studio Code

1. Descomprime el archivo del proyecto.
2. Abre Visual Studio Code.
3. Selecciona **File > Open Folder**.
4. Abre la carpeta:

```text
BibliotecaJDBC_Corregido
```

5. Espera a que VS Code cargue el proyecto Maven.

La estructura principal debe verse así:

```text
BibliotecaJDBC_Corregido/
│
├── pom.xml
├── base_datos.sql
├── README.md
├── .vscode/
│   ├── launch.json
│   └── settings.json
└── src/
    └── main/
        └── java/
            └── cl/
                └── iacc/
                    └── biblioteca/
                        ├── ConexionBD.java
                        ├── Libro.java
                        ├── LibroDAO.java
                        └── Main.java
```

---

## 3. Crear la base de datos

Antes de ejecutar la aplicación, se debe crear la base de datos en MySQL.

### Opción A: Usando MySQL Workbench

1. Abre **MySQL Workbench**.
2. Conéctate a tu servidor local.
3. Abre el archivo:

```text
base_datos.sql
```

4. Ejecuta todo el script.
5. Verifica que se haya creado la base de datos `biblioteca_jdbc`.

### Opción B: Usando phpMyAdmin o XAMPP

1. Inicia **Apache** y **MySQL** desde XAMPP.
2. Ingresa a **phpMyAdmin**.
3. Selecciona la pestaña **SQL**.
4. Copia y pega el contenido del archivo `base_datos.sql`.
5. Presiona **Continuar** o **Ejecutar**.

---

## 4. Revisar el archivo de conexión

La conexión a MySQL se encuentra en:

```text
src/main/java/cl/iacc/biblioteca/ConexionBD.java
```

El archivo contiene la configuración JDBC:

```java
private static final String URL = "jdbc:mysql://localhost:3306/biblioteca_jdbc?useSSL=false&serverTimezone=America/Santiago&allowPublicKeyRetrieval=true";
private static final String USUARIO = "root";
private static final String CLAVE = "";
```

Si usas XAMPP, normalmente el usuario es:

```java
private static final String USUARIO = "root";
private static final String CLAVE = "";
```

Si tu MySQL tiene contraseña, debes escribirla en `CLAVE`. Ejemplo:

```java
private static final String CLAVE = "mi_contraseña";
```

---

## 5. Compilar el proyecto

Abre la terminal integrada de VS Code:

```text
Terminal > New Terminal
```

Luego ejecuta:

```bash
mvn clean compile
```

Este comando descarga las dependencias necesarias y compila el proyecto.

La dependencia principal se encuentra en el archivo `pom.xml`:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.4.0</version>
</dependency>
```

Esto permite que Java pueda conectarse a MySQL mediante JDBC.

---

## 6. Ejecutar la aplicación

Para iniciar el sistema, ejecuta:

```bash
mvn exec:java
```

También puedes abrir la clase:

```text
Main.java
```

y presionar el botón **Run** de Visual Studio Code.

---

## 7. Menú principal del sistema

Al ejecutar el programa, se mostrará un menú similar a este:

```text
===== SISTEMA BIBLIOTECA JDBC =====
1. Registrar libro
2. Listar libros
3. Actualizar libro
4. Eliminar libro
5. Salir
Seleccione una opción:
```

Cada opción permite realizar una operación sobre la tabla `libros` de la base de datos.

---

## 8. Funcionamiento de las clases

### `ConexionBD.java`

Centraliza la conexión con la base de datos MySQL mediante JDBC.

### `Libro.java`

Representa el modelo de datos del libro. Contiene atributos, constructores, métodos getters, setters y `toString()`.

### `LibroDAO.java`

Implementa el patrón DAO. Contiene los métodos para registrar, listar, actualizar y eliminar libros usando consultas SQL.

### `Main.java`

Contiene el método `main` y el menú principal de interacción con el usuario.

---

## 9. Errores comunes y soluciones

### Error: `Access denied for user 'root'@'localhost'`

La contraseña de MySQL no coincide.

Solución: revisa `ConexionBD.java` y actualiza el valor de `CLAVE`.

---

### Error: `Unknown database 'biblioteca_jdbc'`

La base de datos no fue creada.

Solución: ejecuta el archivo `base_datos.sql` en MySQL.

---

### Error: `Communications link failure`

MySQL no está iniciado.

Solución: inicia el servicio MySQL desde XAMPP, MySQL Workbench o Servicios de Windows.

---

### Error: `mvn no se reconoce como comando`

Maven no está instalado o no está agregado al PATH.

Solución: instala Maven o configura su variable de entorno.

---

### Error: `Main method not found`

Se está ejecutando una clase incorrecta.

Solución: ejecuta la clase `Main.java` o usa:

```bash
mvn exec:java
```

---

## 10. Comandos útiles

Compilar el proyecto:

```bash
mvn clean compile
```

Ejecutar la aplicación:

```bash
mvn exec:java
```

Limpiar archivos generados:

```bash
mvn clean
```

---

## 11. Resultado esperado

Al finalizar la ejecución, el sistema debe permitir:

- Registrar libros en MySQL.
- Consultar el listado de libros almacenados.
- Actualizar los datos de un libro existente.
- Eliminar libros desde la base de datos.
- Aplicar correctamente JDBC dentro de un proyecto Java orientado a objetos.

---

## 12. Observación académica

Este proyecto cumple con una estructura básica y ordenada de desarrollo en Java, aplicando separación de responsabilidades mediante clases, conexión JDBC centralizada, uso de `PreparedStatement` para ejecutar consultas SQL de forma segura y organización del código bajo el enfoque de Programación Orientada a Objetos.
