# GUÍA DE ESTUDIO DART

![GitHub Followers](https://img.shields.io/github/followers/kristiancdev?style=social)
![GitHub Followers](https://img.shields.io/github/stars/kristiancdev?style=social)

> [!IMPORTANT]
> La guía aún está en trabajo.

![Logo](https://dart.dev/assets/img/shared/dart/logo+text/horizontal/white.svg)

Página oficial [Dart](https://dart.dev/)

## Introducción

Dart es un lenguaje de programación de código abierto, creado por Google en 2011 y se ha utilizado para desarrollar una variedad de aplicaciones, particularmente en el desarrollo de aplicaciones web y móviles.

Dart se destaca por ser un lenguaje de programación orientado a objetos con una sintaxis limpia y fácil de aprender. Es conocido por su capacidad de crear aplicaciones de alto rendimiento. Además, se utiliza con frecuencia con el framework Flutter para desarrollar aplicaciones móviles tanto para Android como para iOS.

Algunas de las características clave de Dart incluyen la capacidad de ser compilado tanto a código máquina como a JavaScript, lo que lo hace versátil y útil para una amplia gama de aplicaciones.

## Sintaxis

Al igual que otros lenguajes de programación requiere de una función principal de tipo `main()`, para iniciar la ejecución.

A continuación, veremos la sintaxis de Dart con nuestro primer _"Hola, Mundo"_.

```dart
void main() {
  print('Hola Mundo!');
}
```

En este ejemplo, el programa inicia su ejecución en la función `main()`, que es el punto partida en la mayoría de los programas escritos en Dart. La función `print()` se utiliza para mostrar el texto "Hola Mundo!" en la consola.

> Lea más sobre la función main() en Dart, incluyendo parámetros opcionales para argumentos de línea de comandos. ==> En construcción 🛠️

### [Variables](variables/variables.md)

Incluso en Dart que tiene un `tipeado fuerte`, puedes declarar la mayoría de las variables sin especificar explícitamente su tipo usando la palabra `var`. ==> En construcción 🛠️

```dart
var name = 'Voyager I';
var year = 2023;
var antennaDiameter  = 3.7;
var flybyObjects  = ['Jupiter', 'Saturn', 'Uranus', 'Neptune'];
var image = {
  'tags': ['saturn'],
  'url': '//path/to/saturn.jpg'
};
```

> Lee más sobre [variables](variables/variables) en Dart, incluyendo valores por defecto, las palabras clave final y const, y tipos estáticos. ==>link variables

### Sentencias de control

En Dart, al igual que en muchos otros lenguajes de programación, se utilizan varias sentencias de control para manejar la lógica y el flujo de ejecución del programa. Las principales sentencias de flujo de control en Dart incluyen:

- Condicional IF
- Ciclo For
- Ciclo ForEach
- Cilo While

Ejemplo de sentencias de control.

```dart
if (year >= 2001) {
  print('21st century');
} else if (year >= 1901) {
  print('20th century');
}

for (int month = 1; month <= 12; month++) {
  print(month);
}

for (final object in flybyObjects) {
  print(object);
}

while (year < 2016) {
  year += 1;
}
```

> Lea más sobre las [sentencias de flujo o control](#sentencias_flujo) en Dart, incluyendo break y continue, switch y case, y assert. ==> En construcción 🛠️

### Funciones

Es recomendable especificar los tipos de argumentos y valores de retorno de cada función:

```dart
int fibonacci(int n) {
  if (n == 0 || n == 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

var result = fibonacci(20);
```

La sintaxis abreviada `=>` (flecha) es especialmente útil para definir funciones que contienen una única expresión o sentencia. Esta forma abreviada simplifica la escritura de funciones de manera concisa y clara. Se utiliza comúnmente para funciones anónimas o funciones que se pasan como argumentos a otras funciones, como en el caso de `map`, `where`, `forEach`, entre otros métodos de iteración.

```dart
flybyObjects.where((name) => name.contains('turn')).forEach(print);
```

Además de mostrar una función anónima (el argumento de `where()`), en este código muestra que se puede utilizar una función como argumento: la función `print()` es un argumento de `forEach()`.

> Lea más acerca de las [funciones]() en Dart, incluyendo parámetros opcionales, valores de parámetros por defecto y alcance léxico. ==> En construcción 🛠️

### Comentarios

Los comentarios suelen empezar por `//`, este tipo de comentario suele ser usado para comentarios de una línea, para comentarios de varias líneas se puede usar `/* comentario */`.

```dart
// This is a normal, one-line comment.

/*
This is a documentation comment, used to document libraries,
classes, and their members. Tools like IDEs and dartdoc treat
doc comments specially.
*/
```

> Más información sobre los [comentarios en Dart](#comentarios), incluido el funcionamiento de las herramientas de documentación.

### Importaciones

Para importar bibliotecas o archivos que has creado o que provienen de fuentes externas, se utiliza la palabra clave `import` seguida de la ruta del archivo.

```dart
// Importing core libraries
import 'dart:math';

// Importing libraries from external packages
import 'package:test/test.dart';

// Importing files
import 'path/to/my_other_file.dart';
```

> Lea más sobre [bibliotecas y visibilidad en Dart](), incluyendo prefijos de bibliotecas, mostrar y ocultar, y carga perezosa a través de la palabra clave deferred. ==> En construcción 🛠️

### Clases

Las clases son bloques fundamentales de la programación orientada a objetos (OOP) que permiten modelar entidades, definir atributos y comportamientos. Las clases son plantillas para crear objetos, y cada objeto es una instancia de una clase.

Aquí tienes un ejemplo básico de cómo se define una clase en Dart:

```dart
// Definición de una clase llamada 'Persona'
class Persona {
  // Atributos o propiedades de la clase
  String nombre;
  int edad;

  // Constructor de la clase
  Persona(this.nombre, this.edad);

  // Métodos (funciones) de la clase
  void saludar() {
    print('¡Hola! Mi nombre es $nombre y tengo $edad años.');
  }
}
```

> Más información sobre [cadenas](#cadenas), incluida la interpolación de cadenas, literales, expresiones y el método toString().

Podrías utilizar la clase `class Persona` de la siguiente manera:

```dart
void main() {
  // Creación de un objeto 'persona' a partir de la clase 'Persona'
  var persona = Persona('Juan', 30);

  // Acceso a los atributos y métodos del objeto 'persona'
  print(persona.nombre); // Imprime el nombre: Juan
  print(persona.edad); // Imprime la edad: 30
  persona.saludar(); // Llama al método 'saludar' de la clase Persona
}
```

> Lea más acerca de las [clases en Dart](), incluyendo listas inicializadoras, new y const opcionales, redireccionamiento de constructores, constructores de fábrica, getters, setters, y mucho más. ==> En construcción 🛠️

### Enumeradores

Los enums son una forma de enumerar un conjunto predefinido de valores o instancias de forma que se garantice que no puede haber ninguna otra instancia de ese tipo.

He aquí un ejemplo de un enum sencillo que define una lista simple de tipos de planeta predefinidos:

```dart
enum PlanetType { terrestrial, gas, ice }
```

He aquí un ejemplo de declaración enum mejorada de una clase que describe planetas, con un conjunto definido de instancias constantes, a saber, los planetas de nuestro propio sistema solar.

```dart
/// Enum that enumerates the different planets in our solar system
/// and some of their properties.
enum Planet {
  mercury(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  venus(planetType: PlanetType.terrestrial, moons: 0, hasRings: false),
  // ···
  uranus(planetType: PlanetType.ice, moons: 27, hasRings: true),
  neptune(planetType: PlanetType.ice, moons: 14, hasRings: true);

  /// A constant generating constructor
  const Planet(
      {required this.planetType, required this.moons, required this.hasRings});

  /// All instance variables are final
  final PlanetType planetType;
  final int moons;
  final bool hasRings;

  /// Enhanced enums support getters and other methods
  bool get isGiant =>
      planetType == PlanetType.gas || planetType == PlanetType.ice;
}
```

Puede utilizar el enum Planeta de la siguiente manera:

```dart
final yourPlanet = Planet.earth;

if (!yourPlanet.isGiant) {
  print('Your planet is not a "giant planet".');
}
```

> Lea más sobre los enums en Dart, incluyendo los requisitos mejorados de los enums, propiedades introducidas automáticamente, acceso a nombres de valores enumerados, soporte de sentencias switch, y mucho más. ==> En construcción 🛠️

### Herencia

En Dart, la herencia se logra extendiendo una clase base (también conocida como superclase) para crear una nueva clase (llamada subclase) que hereda los atributos y métodos de la superclase.

Aquí tienes un ejemplo básico de cómo se utiliza la herencia en Dart:

```dart
class Orbiter extends Spacecraft {
  double altitude;

  Orbiter(super.name, DateTime super.launchDate, this.altitude);
}
```

> Más información sobre la extensión de clases, la anotación opcional @override y mucho más.

### Mixins

Los mixins son una forma de reutilizar código en múltiples jerarquías de clases. A continuación se muestra una declaración mixin:

```dart
mixin Piloted {
  int astronauts = 1;

  void describeCrew() {
    print('Number of astronauts: $astronauts');
  }
}
```

Para añadir las capacidades de un mixin a una clase, basta con extender la clase con el mixin.

```dart
class PilotedCraft extends Spacecraft with Piloted {
  // ···
}
```

PilotedCraft ahora tiene el campo astronautas, así como el método describeCrew().

Más información sobre mixins. ==> Link

### Interfaces y clases abstractas

Todas las clases definen implícitamente una interfaz. Por lo tanto, puedes implementar cualquier clase.

```dart
class MockSpaceship implements Spacecraft {
  // ···
}
```

Más información sobre interfaces implícitas o sobre la palabra clave interfaz explícita.

Puedes crear una clase abstracta para que sea extendida (o implementada) por una clase concreta. Las clases abstractas pueden contener métodos abstractos (con cuerpos vacíos).

```dart
abstract class Describable {
  void describe();

  void describeWithEmphasis() {
    print('=========');
    describe();
    print('=========');
  }
}
```

Cualquier clase que extienda a Describable tiene el método describeWithEmphasis(), que llama a la implementación de describe() del extensor.

Más información sobre clases y métodos abstractos.

### Asíncrono

Evita el invfierno de devoluciónes de llamadas de retorno y haz que tu código sea mucho más legible utilizando async y await.

```dart
const oneSecond = Duration(seconds: 1);
// ···
Future<void> printWithDelay(String message) async {
  await Future.delayed(oneSecond);
  print(message);
}
```

El método anterior es equivalente a:

```dart
Future<void> printWithDelay(String message) {
  return Future.delayed(oneSecond).then((_) {
    print(message);
  });
}
```

Como muestra el siguiente ejemplo, async y await ayudan a que el código asíncrono sea fácil de leer.

```dart
Future<void> createDescriptions(Iterable<String> objects) async {
  for (final object in objects) {
    try {
      var file = File('$object.txt');
      if (await file.exists()) {
        var modified = await file.lastModified();
        print(
            'File for $object already exists. It was modified on $modified.');
        continue;
      }
      await file.create();
      await file.writeAsString('Start describing $object in this file.');
    } on IOException catch (e) {
      print('Cannot create description for $object: $e');
    }
  }
}
```

También puedes usar dart async\*, que te da una forma agradable y legible de construir flujos.

```dart
Stream<String> report(Spacecraft craft, Iterable<String> objects) async* {
  for (final object in objects) {
    await Future.delayed(oneSecond);
    yield '${craft.name} flies by $object';
  }
}
```

Más información sobre el soporte asíncrono, incluyendo funciones asíncronas, Future, Stream, y el bucle asíncrono (await for).

### Excepciones

Para lanzar una excepción, utilice throw:

```dart
if (astronauts == 0) {
  throw StateError('No astronauts.');
}
```

Para capturar una excepción, utilice una sentencia try con on o catch (o ambos):

```dart
Future<void> describeFlybyObjects(List<String> flybyObjects) async {
  try {
    for (final object in flybyObjects) {
      var description = await File('$object.txt').readAsString();
      print(description);
    }
  } on IOException catch (e) {
    print('Could not describe object: $e');
  } finally {
    flybyObjects.clear();
  }
}
```

Ten en cuenta que el código anterior es asíncrono; try funciona tanto para código síncrono como para código en una función asíncrona.

> Lee más sobre excepciones, incluyendo stack traces, rethrow, y la diferencia entre Error y Excepción.

### Conceptos importantes

A medida que continúe aprendiendo sobre el lenguaje Dart, tenga en cuenta estos hechos y conceptos:

- Todo lo que puedes colocar en una variable es un objeto, y cada objeto es una instancia de una clase. Incluso los números, las funciones y null son objetos. Con la excepción de null (si habilita la seguridad de sonido null), todos los objetos heredan de la clase Object.

- Aunque Dart es fuertemente tipado, las anotaciones de tipo son opcionales porque Dart puede inferir tipos. En var number = 101, se infiere que number es de tipo int.

- Si activas la seguridad de nulos, las variables no pueden contener nulos a menos que digas que pueden. Puedes hacer que una variable sea anulable poniendo un signo de interrogación (?) al final de su tipo. Por ejemplo, una variable de tipo int? puede ser un número entero o puede ser nula. Si sabe que una expresión nunca se evalúa como nula pero Dart no está de acuerdo, puede añadir ! para afirmar que no es nula (y lanzar una excepción si lo es). ¡Un ejemplo: int x = nullableButNotNullInt!

- Cuando quiera decir explícitamente que cualquier tipo está permitido, utilice el tipo Object? (si ha activado la seguridad de nulos), Object o, si debe aplazar la comprobación de tipos hasta el tiempo de ejecución, el tipo especial dynamic.

- Dart soporta tipos genéricos, como List<int> (una lista de enteros) o List<Object> (una lista de objetos de cualquier tipo).

- Dart soporta funciones de nivel superior (como main()), así como funciones ligadas a una clase u objeto (métodos estáticos y de instancia, respectivamente). También puedes crear funciones dentro de funciones (funciones anidadas o locales).

- Similarly, Dart supports top-level variables, as well as variables tied to a class or object (static and instance variables). Instance variables are sometimes known as fields or properties.

- A diferencia de Java, Dart no tiene las palabras clave public, protected y private. Si un identificador comienza con un guión bajo (\_), es privado para su biblioteca. Para más detalles, ver Bibliotecas e importaciones.

- Los identificadores pueden empezar por una letra o un guión bajo (\_), seguidos de cualquier combinación de esos caracteres más dígitos.

- Dart tiene tanto expresiones (que tienen valores en tiempo de ejecución) como sentencias (que no los tienen). Por ejemplo, la expresión condicional condition ? expr1 : expr2 tiene un valor de expr1 o expr2. Compárelo con una sentencia if-else, que no tiene valor. Una sentencia suele contener una o varias expresiones, pero una expresión no puede contener directamente una sentencia.

- Las herramientas Dart pueden reportar dos tipos de problemas: advertencias y errores. Las advertencias son sólo indicaciones de que su código podría no funcionar, pero no impiden que su programa se ejecute. Los errores pueden ser de compilación o de ejecución. Un error en tiempo de compilación impide que el código se ejecute; un error en tiempo de ejecución produce una excepción mientras el código se ejecuta.

### Recursos adicionales

Puedes encontrar más documentación y ejemplos de código en el recorrido por la biblioteca y en la referencia de la API de Dart. El código de este sitio sigue las convenciones de la guía de estilo de Dart.
https://dart.dev/guides/libraries/library-tour
https://api.dart.dev/stable/3.1.5/index.html
https://dart.dev/effective-dart/style

[![BuyMeACoffee](https://img.shields.io/badge/Buy_Me_A_Coffee-apoya_mi_trabajo-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=white&labelColor=101010)](https://www.buymeacoffee.com/kristiancdev)
