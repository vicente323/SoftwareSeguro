# Common Weakness Enumeration vs CERT coding standards 

## Similitudes existentes entre ambos

**Orientación para desarrolladores:** Tanto CWE como las CERT Secure Coding Standards están diseñados para ser utilizados por desarrolladores de software y profesionales de seguridad. Ofrecen orientación práctica para escribir código más seguro y reducir las vulnerabilidades en el software.

**Enfoque en la seguridad de software:** Tanto el CWE Framework como las CERT Secure Coding Standards se centran en abordar las vulnerabilidades y debilidades de seguridad en el software. Su objetivo es mejorar la seguridad del software al identificar y mitigar riesgos de seguridad comunes.

**Clasificación de debilidades:** Ambos recursos proporcionan una forma de clasificar debilidades de seguridad. CWE clasifica las debilidades en categorías y subcategorías, mientras que las CERT Secure Coding Standards proporcionan reglas y pautas específicas para evitar estas debilidades.

**Aplicación en diversas etapas del ciclo de vida del software:** Tanto CWE como las CERT Secure Coding Standards son aplicables en diferentes etapas del ciclo de vida del software, desde el diseño y desarrollo hasta las pruebas y la revisión de código.

## Ejemplos de estándares del CERT que corresponda a un CWE

**CWE-119:** Uso incorrecto de funciones de seguridad de la memoria:

**Estándar CERT:** EXP40-C. No asigne directamente punteros a los valores de la función que pueden caducar.

**Descripción:** Este estándar aborda la debilidad de CWE-119, que se relaciona con el uso incorrecto de funciones de seguridad de la memoria, como la asignación de punteros a valores que pueden caducar. El estándar de CERT sugiere prácticas seguras para evitar esta debilidad.
```
#include <stdlib.h>

int main() {
    int *ptr;
    int value = 42;
    ptr = &value; // Violación de la regla CERT
    return 0;
}
```

En este ejemplo, asignamos directamente un puntero a una variable local value que podría caducar cuando la función main() salga del ámbito. La recomendación de CERT sería evitar este tipo de asignación directa y, en su lugar, utilizar funciones de seguridad de memoria o garantizar que el ciclo de vida del objeto sea adecuado



**2.CWE-89:** Inyección de SQL:

**Estándar CERT:** IDS00-J. Evite la inyección de SQL.

**Descripción:** CWE-89 se refiere a la inyección de SQL, una debilidad común en la que los atacantes pueden manipular las consultas SQL de una aplicación. El estándar CERT IDS00-J se centra en prevenir esta debilidad al proporcionar pautas para evitar la inyección de SQL de manera efectiva.


```

import java.sql.*;
import java.util.Scanner;

public class SQLInjectionDemo {
        
       public static void main(String[] args) throws SQLException {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Ingrese un nombre de usuario: ");
        String input = scanner.nextLine();

        // Violación de la regla CERT, ya que no se utiliza una consulta parametrizada para evitar la inyección de SQL.
        String sql = "SELECT * FROM usuarios WHERE nombre = '" + input + "'";
        
        Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/basededatos", "usuario", "contraseña");
        Statement statement = connection.createStatement();
        ResultSet resultSet = statement.executeQuery(sql);

        
    }
}

```


En este ejemplo, se concatena directamente la entrada del usuario en una consulta SQL, lo que podría permitir la inyección de SQL. La recomendación de CERT sería utilizar consultas parametrizadas para prevenir esta debilidad.



**3.CWE-306:** Sesión sin terminar:

**Estándar CERT:** SEC05-J. Maneje adecuadamente las sesiones de usuario.

**Descripción:** CWE-306 se refiere a la posibilidad de que las sesiones de usuario no se manejen adecuadamente, lo que 
podría permitir que un atacante acceda a una sesión de usuario no terminada. El estándar CERT SEC05-J proporciona pautas para garantizar un manejo seguro de sesiones de usuario y prevenir esta debilidad.
```
public class SessionManagementServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) {
        HttpSession session = request.getSession();
        // Violación de la regla CERT, ya que no se maneja adecuadamente la sesión de usuario.
        // La sesión podría quedar sin terminar al no invalidarla correctamente.
        // Sesión sin terminar podría permitir el acceso no autorizado a la sesión.
        // session.invalidate(); // Línea recomendada para terminar la sesión.
    }
}
```
En este ejemplo, no se maneja adecuadamente la sesión de usuario, ya que no se invalida la sesión cuando debería hacerse.
