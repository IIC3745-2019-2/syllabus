# IIC3745 - Actividad 2

Luego de pestañear, te encuentras en un mundo lleno de seres mágicos con poderes, cuyo vocabulario recae en una sola palabra por ser. Al ver a tu compañero te das cuenta que estás en el mundo _Pokémon_.

Lamentablemente, despiertas de un salto para percatarte que todo era un sueño. Sin embargo, ves que mientras dormías escribiste un programa en _ruby_ para simular batallas pokémon.

Como no confías en tu trabajo sonámbulo, decides generar una batería de _tests_ para comprobar que el método `Pokemon.attack` funciona correctamente.

De acuerdo a tus conocimientos de _testing_, sabes que es necesario medir el _coverage_ sobre tu código, por lo que decides aplicar los siguientes criterios para asegurar cierto nivel de calidad:

1. _Predicate Coverage_
2. _Clause Coverage_
3. _Restricted Active Clause Coverage_
4. _Correlated Active Clause Coverage_

### Batalla Pokémon

En este programa existen entidades llamadas pokémones que luchan entre sí para nuestra entretención. En estas batallas un pokémon desafía a otro, por lo que adquieren el nombre de "desafiante" y "desafiado" respectivamente.

Cada pokémon tiene distintas características como: velocidad, daño físico, defensa física, un tipo y vida.

Además, cada pokemón tiene solo 1 ataque para realizar, el cual realiza daño al oponente. Este daño se ve aumentado o disminuido dependiendo de los tipos de pokémones y el estado de estos.

Los pokémones se golpearan por turnos y ganará el que logre bajarle la vida a su contrincante. 

A medida que la vida comience a bajar en los pokémones, estos ganarán bonificaciones en ataque. Si este se encuentra bien de salud, tendrá una bonificación constante en su daño.

Además, si un pokémon se ve en desventaja (menor ataque y velocidad) también obtendrá un tipo de ventaja en su daño.

Por último, el pokémon con mayor velocidad comienza atacando. Si ambos tienen la misma velocidad, comienza el desafiado.


## Código

En el repositorio [activity02-template](https://github.com/IIC3745-2019-2/activity02-template) podrá encontrar el código que desarrolló mientras dormía.


## To Do

En grupos de **exactamente** 3 personas y con la ayuda de la librería `minitest` generen 4 baterías de _tests_ unitarios **mínimamente necesarios e independientes** para cubrir el funcionamiento del método `Pokemon.attack` según los criterios de cobertura listados anteriormente. Deben explicar qué requisitos de prueba se están cubriendo con cada una de sus pruebas según el criterio de cobertura que estén evaluando (puede ser un bloque de comentarios junto a cada prueba).

## Información de utilidad

### Estructura de un _test_

Por lo general, los _tests_ siguen la siguiente estructura independiente del lenguaje y librerías que se utilicen:

```
# nombre descriptivo del test

## Setup: donde se inicializan todas las variables necesarias 
## para testear el método.


## Acá va la prueba misma mediante el famoso "assert".


## Teardown: donde se limpian/resetean todas las variables que
## mutaron durante el test.

```

### Buenas prácticas

A continuación hay un listado de buenas prácticas al momento de escribir un _test_:

1. Nombres de _test_ descriptivos
2. _Setup_ y _teardown_ para cada _test_
3. Un _assert_ por _test_

### Material adicional

Para más información pueden consultar los siguientes enlaces: 
* [stackify-unit-testing-best-practices](https://stackify.com/unit-testing-basics-best-practices/)
* [microsoft-unit-testing-best-practices](https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
* [dev-minittest-intro-ruby](https://dev.to/exampro/minitest-writing-test-code-in-ruby-part-2-of-3-4306)
* [launch-school-intro-minittest-ruby***](https://launchschool.com/blog/assert-yourself-an-introduction-to-minitest)

### Ejemplo Cobertura _GACC_

A continuación se muestra un ejemplo de como probar un método de una clase. Veamos el siguiente código:

```rb
# year_classifier.rb

class YearClassifier

    def is_leap_year(year)
        return (year % 400).zero? || ((year % 4).zero? && (year % 100).positive?)
    end
    
end
```

Para este caso en particular, veremos como _testear_ buscando satisfacer el criterio de _coverage_ conocido como _General Active Clause Coverage (GACC)_. Como se puede ver en el método, hay tres condiciones a tomar en cuenta: 

**a)** `(year % 400).zero?`
**b)** `(year % 4).zero?`
**c)** `(year % 100).positive?`

Usando la librería `minitest` podemos desarrollar los siguientes _tests_,

```rb
# test_leap_year.rb

require 'minitest/autorun'
require './year_classifier'

class TestYearClassifier < Minitest::Test

    def setup
        @year_classifier = YearClassifier.new
    end
    
    def test_divisible_only_by_four
        assert @year_classifier.is_leap_year(2004)?
    end
    
    def test_divisible_by_one_hundred
        assert_not @year_classifier.is_leap_year(1900)?
    end
    
    def test_divisible_by_four_hundred
        assert @year_classifier.is_leap_year(2000)?
    end
    
    def test_divisible_by_odd_year
        assert_not @year_classifier.is_leap_year(2001)?
    end
    
end
```

Como se puede ver en el ejemplo anterior, cumplimos con las siguientes cláusulas del método:

|| Input | `(year % 400).zero?` | `(year % 4).zero?` | `(year % 100).positive?` | Output |
|-|-------|:--------------------:|:------------------:|:------------------------:|:---------:|
|T1| 1900 | False | True | True | **False** |
|T2| 2000 | True | True | True | **True** |
|T3| 2001 | False | False | False | **False** |
|T4| 2004 | False | True | False | **True** |

Para poder alcanzar un 100% de _GACC_, hay que cumplir con 5 requerimientos lógicos, estos se ven reflejados en los cuatro casos de _tests_ mostrados anteriormente.

## Formato de Entrega

En la encuesta _Actividad 2_ un integrante de cada grupo debe completar su número de grupo (designado al momento de firmar la lista), nombres de los integrantes y subir un archivo `.zip` que contenga los archivos `pc.rb`, `cc.rb`, `cacc.rb` y `racc.rb` con sus códigos de pruebas y justificaciones.
