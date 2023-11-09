# Variables

A continuación crearemos e inicilizaremos una variable.

```dart
var nombre = 'Bob';
```

Las variables almacenan referencias. En el ejemplo la variable llamada `nombre` contiene una referencia a un objeto tipo `String` con valor "Bob".

El tipo de la variable `nombre` se infiere que es `String`, pero puedes cambiar ese tipo especificándolo. Si un objeto no está restringido a un único tipo, especifique el tipo Object (o dinámico si es necesario).

```dart
Object name = 'Bob';
```

Otra opción es declarar explícitamente el tipo que se inferirá:

```dart
String name = 'Bob';
```

> **Nota:** Esta página sigue la recomendación de la guía de estilo de utilizar var, en lugar de anotaciones de tipo, para las variables locales.

## Null Safety, o seguridad de nulos

Dart asegura que no se produzcan errores al acceder accidentalmente a variables que están establecidas como nulas. Esto previene lo que se conoce como un error de referencia nula (null dereference error). Este error ocurre cuando intentas acceder a una propiedad o llamar a un método en una expresión que evalúa a null. Una excepción a esta regla es cuando null soporta la propiedad o el método, como por ejemplo `toString()` o `hashCode`. Con la seguridad de nulos, el compilador de Dart detecta estos posibles errores en tiempo de compilación.

La seguridad de nulos introduce tres cambios clave en Dart:

1. **Control de nulabilidad en tipos:** Al especificar un tipo para una variable, parámetro u otro componente relevante, puedes controlar si ese tipo permite nulos. Para habilitar la nulabilidad, se agrega un ? al final de la declaración del tipo.

```dart
String? name // Tipo nullable. Puede ser 'null' o una cadena de texto.`
String name   // Tipo no nullable. No puede ser 'null', pero puede ser una cadena de texto.`
```

2. **Inicialización de variables:** En Dart, debes inicializar las variables antes de usarlas. Las variables que pueden ser nulas tienen un valor predeterminado de 'null', por lo que se inicializan de forma predeterminada. Dart no establece valores iniciales para tipos no nulos y te obliga a definir un valor inicial. Esto evita que puedas acceder a propiedades o llamar a métodos donde el tipo del receptor puede ser nulo, pero el nulo no soporta el método o propiedad utilizado.

3. **Acceso a propiedades o métodos en tipos nulos:** No puedes acceder a propiedades o llamar a métodos en una expresión con un tipo nulo. La misma excepción se aplica cuando se trata de una propiedad o método que null admite, como hashCode o toString().

La seguridad de nulos "Sound null safety" convierte los posibles errores en tiempo de ejecución en errores de análisis en tiempo de edición. La seguridad de nulos señala un aviso sobre una variable no nula en los siguientes casos:

1. **No inicializada con un valor no nulo:** Si una variable no se inicializa con un valor que no sea nulo.
2. **Asignada con un valor nulo:** Si a una variable no nula se le asigna un valor nulo en algún punto del programa.

Esta verificación te permite corregir estos errores antes de implementar tu aplicación, lo que significa que puedes identificar y solucionar posibles problemas relacionados con nulos durante la fase de desarrollo, antes de que la aplicación esté en funcionamiento.

## Valores por Defecto

Las variables no inicializadas que tienen un tipo `nullable` tienen un valor inicial nulo. Incluso las variables con tipos numéricos son inicialmente nulas, porque los números como todo lo demás en Dart son objetos.

```dart
int? lineCount;
assert(lineCount == null);
```

Con el control de nulos, debe inicializar las variables no `nullable` antes de ser utilizadas:

```dart
int lineCount = 0;
```

Esto significa que si declaras una variable numérica, como por ejemplo un entero (int), y no le asignas un valor inicial, automáticamente se inicializará como null en lugar de un valor numérico predeterminado (como el 0 en otros lenguajes). Lo mismo ocurre con otros tipos de variables que son declaradas como nullable y no se les asigna un valor en su inicio: adquieren el valor nulo por defecto.

```dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
```

Las variables a nivel superior (top-level) y las variables de clase se inicializan de manera perezosa (lazy initialization); es decir, el código de inicialización se ejecuta la primera vez que se utiliza la variable.

> **Quiere decir:**
> Cuando declaras una variable a nivel superior (fuera de cualquier función o clase) o una variable de clase en Dart, no se inicializa inmediatamente. En cambio, el código de inicialización asociado a esa variable no se ejecuta hasta que la variable es referenciada o utilizada por primera vez en el código. En ese momento, se ejecuta el código de inicialización y la variable adquiere su valor inicial.

## Variables tardias (Late Variables)

En Dart, el modificador "late" tiene dos casos de uso:

1. Declarar una variable no nula que se inicializa después de su declaración.
2. Inicializar perezosamente una variable.

A menudo, el análisis de flujo de control de Dart puede detectar cuándo una variable no nula se establece con un valor no nulo antes de ser utilizada, pero a veces el análisis falla. Dos casos comunes son las variables de nivel superior y las variables de instancia: Dart a menudo no puede determinar si se establecen, por lo que no intenta hacerlo.

Si estás seguro de que una variable está configurada antes de su uso, pero Dart no está de acuerdo, puedes solucionar el error marcando la variable como "late": esta anotación le indica al compilador que confíes en que la variable se inicializará antes de ser utilizada, evitando así errores de análisis estático. La palabra clave "late" es una señal para el compilador de que sepa que la variable no es inicializada inmediatamente, sino que será inicializada más tarde antes de ser utilizada.

```dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
```

> Si no se inicializa una variable tardía, se produce un error de ejecución cuando se utiliza la variable.

Cuando marcas una variable como "late" pero la inicializas en su declaración, el inicializador se ejecuta la primera vez que se utiliza la variable. Esta inicialización perezosa es útil en un par de casos:

1. La variable podría no ser necesaria y su inicialización es costosa.
2. Estás inicializando una variable de instancia y su inicializador necesita acceso a la instancia (utiliza la palabra clave `this`).

En el siguiente ejemplo, si la variable `temperature` nunca se utiliza, entonces la función costosa `readThermometer()` nunca se llama:

```dart
class Weather {
  late double temperature = readThermometer(); // El valor se inicializa perezosamente

  double readThermometer() {
    // Código costoso para leer la temperatura
    return 25.0;
  }
}

void main() {
  var weather = Weather();

  // El método readThermometer() no se llama
  // si la variable temperature no se utiliza en ninguna parte del código.
}
```

En este ejemplo, la función `readThermometer()` no se ejecuta inmediatamente al crear una instancia de la clase `Weather`. En cambio, se ejecutará solo si la variable `temperature` se usa en algún lugar del código. Esta estrategia es útil cuando la inicialización de la variable es costosa y es posible que no se utilice en todas las ejecuciones del programa.

## Final y const

Si no tienes la intención de cambiar una variable, se recomienda utilizar `final` o `const`, ya sea en lugar de `var` o además de especificar un tipo. Un variable `final` solo puede ser establecida una vez; mientras que una variable `const` es una constante en tiempo de compilación. (Las variables `const` son implícitamente `final`).

- **`final`:** Una variable final puede ser inicializada solo una vez y su valor no puede cambiar. Es decir, una vez que se le asigna un valor, no se puede reasignar.
- **`const`:** Una variable constante es un valor que se conoce en tiempo de compilación y es inmutable. Las variables `const` son, por lo tanto, constantes en tiempo de compilación y no pueden ser modificadas.

```dart
// Ejemplo de final y const
final int finalNumber = 10; // Variable final
const double PI = 3.14;     // Variable constante

void main() {
  // Intentar reasignar valores a variables final o const generará un error.
  // finalNumber = 20; // Error: Una vez asignado, no puede ser modificado.
  // PI = 3.1416;      // Error: Las variables const no pueden ser modificadas.

  // Variables final y const pueden ser usadas como constantes en tiempo de compilación.
  print(finalNumber); // Salida: 10
  print(PI);          // Salida: 3.14
}
```

En resumen, usar `final` o `const` es útil cuando estás seguro de que el valor de una variable no cambiará. `final` permite asignar el valor en tiempo de ejecución y `const` es para valores conocidos y constantes en tiempo de compilación.

> ❌ No se puede cambiar el valor de una variable final:

```dart
final int finalNumber = 3; // Variable final
```

Correcto, en Dart, se utiliza `const` para variables que se desean definir como constantes en tiempo de compilación. Si la variable constante se encuentra a nivel de clase, se la marca como `static const`. Además, al declarar la variable, se establece el valor a una constante en tiempo de compilación, como un número o cadena literal, una variable constante o el resultado de una operación aritmética en números constantes.

Por ejemplo:

```dart
const bar = 1000000; // Unidad de presión (dinas/cm2)
const double atm = 1.01325 * bar; // Atmósfera estándar

class Pressure {
  static const double bar = 1.0;
  static const double atm = 1.01325 * bar;
}

void main() {
  print(bar); // Salida: 1000000
  print(atm); // Salida: 1013250.0
  print(Pressure.atm); // Salida: 1.01325
}
```

En este ejemplo, `bar` es una constante con un valor de 1000000 y `atm` se define como una constante calculada basada en el valor de `bar`. Además, en la clase `Pressure`, se utilizan variables estáticas `const` para representar las mismas constantes relacionadas con la presión.

En Dart, la palabra clave `const` no solo se utiliza para declarar variables constantes, sino también para crear valores constantes, así como para declarar constructores que crean valores constantes. Cualquier variable puede tener un valor constante.

```dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalente a `const []`
```

En este caso, `foo`, `bar` y `baz` son variables con valores constantes. Sin embargo, hay diferencias importantes en cómo se comportan:

- `foo` es una variable modificable, inicializada con una lista constante. Aunque inicialmente es constante, su valor puede cambiar más tarde a una lista diferente.
- `bar` es una variable inmutable (no se puede reasignar) que contiene una lista constante. No se puede cambiar su valor.
- `baz` se declara con `const` directamente y su valor no se puede cambiar, ya que es una lista constante desde el principio. Al no especificar un valor en la declaración, Dart asume `const []` por defecto.

```dart
foo = [1, 2, 3]; // Era const []
// Ahora, foo ya no es una lista constante, se cambió a [1, 2, 3]
```

Puedes cambiar el valor de una variable no final y no constante, incluso si inicialmente tenía un valor constante.

> ❌ En contraste, no puedes cambiar el valor de una variable constante:

```dart
baz = [42]; // Error: Las variables constantes no pueden ser reasignadas.
```

Además, es posible definir constantes que utilicen verificaciones y conversiones de tipo (is y as), operadores de colección condicionales (if), y operadores de propagación (spread):

```dart
const Object i = 3; // Donde i es un Object constante con un valor int...
const list = [i as int]; // Utilización de una conversión de tipo.
const map = {if (i is int) i: 'int'}; // Utilización de is y collection if.
const set = {if (list is List<int>) ...list}; // ...y una propagación (spread).
```

Estos ejemplos muestran cómo se puede utilizar `const` para crear valores constantes y cómo se comportan las variables que contienen estos valores en Dart.

> **Nota:** Aunque un objeto final no puede modificarse, sus campos sí pueden cambiarse. En comparación, un objeto const y sus campos no pueden modificarse: son inmutables.

**[Volver al menu 🔙](/README.md)**
