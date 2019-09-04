# Pauta AC01

## Diseño de Pruebas

**a) (1.0 pts)**


Se espera que ingresen al menos 5 casos de prueba que cumplan las siguientes condiciones:

- No debe provocar falsos positivos (Ej: strings generados al azar sin reglas)
- Debe comprobar una sola cosa a la vez (Ej: Caso con el dominio **y** la dirección incorrecta)
    - Pueden ser acumulativos, pero no es el ideal.
- No deben comprobar cosas fuera del _scope_ de la prueba (Ej: no entregar argumentos a la función, entregar un _booleano_, etc)
- No sea redundante (Ej: dos casos para comprobar lo mismo)

Puntajes:
- **0,5 por no presentar redundancia**
- **0,5 por presentar un mínimo de 5 casos útiles**

**b) (1.0 pts)**

La función creada debe:
- Cumplir con lo pedido en el enunciado:
    - Retornar `true` o `false`
    - Comprueba estructura correcta:
        - Emails con direccion_valida + '@' + dominio_valido
    - Direccion_valida:
        - Puede tener
            - puntos
            - guiones bajo.
            - letras
            - números
        - Tamaño mínimo 1
        - Mínimo 1 caracter alfanumérico
    - Dominio_valido:
        - Mínimos dos subdominios (Ej: En `'uc.cl'`, se tiene tanto a `'uc'` como `'cl'`).
        - Cada subdominio debe ser válido:
            - Tamaño mínimo 1
            - Tamaño máximo 67
            - Puede tener:
                -  letras
                -  números
                -  guiones (opcional)

La función será probada con lo siguientes casos

```ruby

# TRUE
validate_email('string.string@string.string')
validate_email('string_string@string.string')
validate_email('string@string.string')

# FALSE
validate_email('string@' + 'd'*70 + '.com')
validate_email('string@string')
validate_email('string string@ string . string')
validate_email('!#@string.string')
validate_email('@string')
validate_email('@')
validate_email('@@')
validate_email('string@')
validate_email('')

```

Puntajes:

- **(0.25 pts)** Comprueba estructura correcta (direccion + '@' + dominio)
- **(0.25 pts)** Comprueba dirección válida
- **(0.5 pts)** Comprueba dominio válido

**c) (0.5 pts)**

La respuesta es **no**.

Razón: El problema era que los emails no les llegaban a los usuarios. Esto puede ser por muchas razones (entre ellas que escribieron mal el email, o que lo dejaron en blanco), por lo que la solución sería una verificación del email en la creación de cuenta.

Puntajes:
- **(0.25 pts)** respuesta correcta.
- **(0.25 pts)** razón válida.


## _Code Coverage_

**a) (1.5 puntos)**

1. _Statement Coverage_

El alumno debe presentar un mínimo de 3 casos de ejemplo, cada caso tiene una condición obligatoria que se muestra a continuación,

```ruby
# CASO 1: balance = debt.value y debt.paid = false

# CASO 2: balance < debt.value

# CASO 3: debt.paid = true
```

2. _Branch Coverage_

El código posee cuatro ramificaciones, es necesario que el alumno entregue un caso por cada ramificación, es decir, un ejemplo de cada caso que se muestra a continuación,

```ruby
# CASO 1: balance > debt.value y debt.paid = false

# CASO 2: balance = debt.value y debt.paid = false

# CASO 3: balance < debt.value y debt.paid = false

# CASO 4: debt.paid = true
```

3. _Condition Coverage_

Es necesario entregar condiciones para que las variables booleanas entreguen todos los resultados posibles. Basta con entregar ejemplos de cada uno de los casos que se muestran a continuación,

```ruby
# CASO 1: balance = debt.value y debt.paid = false

# CASO 2: balance > debt.value y debt.paid = false

# CASO 3: balance < debt.value y debt.paid = false

# CASO 4: balance >= debt.value y debt.paid = true

# CASO 5: balance < debt.value y debt.paid = true
```

|  | `dif >= 0` | `dif == 0` | `debt.paid` |
|--------|:------------:|:--------------:|:-------------:|
| Caso 1 | TRUE | TRUE | FALSE |
| Caso 2 | TRUE | FALSE | FALSE |
| Caso 3 | FALSE | FALSE | FALSE |
| Caso 4 | TRUE | FALSE v TRUE | TRUE |
| Caso 5 | FALSE | FALSE | TRUE |

Por la semántica del software hay 5 casos posibles bajo _condition coverage_. Esto es porque un átomo es `!debt.paid` y otro es lo contrario `debt.paid`, por lo que siempre tomarán valores opuestos, lo que limita los casos de pruebas posibles.

Puntajes:

- **(0,5 pts)** por obtener 100% de _statement coverage_ con la cantidad mínima de casos (3 casos)
- **(0,5 pts)** por obtener 100% de _branch coverage_ con la cantidad mínima de casos (4 casos)
- **(0,5 pts)** por obtener 100% de _condition coverage_. El alumno puede presentar casos redundantes.

**b) (1.0 puntos)**

![](https://i.imgur.com/AKlb5cz.png)

_Branch Coverage_: En el código existe un total de 4 _branches_, por lo tanto, es necesario cumplir con los siguientes casos para tener un _coverage_ del 100%,

```ruby
# BRANCH 1: year % 4 = 0 y year % 100 = 0 y year % 400 = 0
# BRANCH 2: year % 4 != 0
# BRANCH 3: year % 4 = 0 y year % 100 != 0
# BRANCH 4: year % 4 = 0 y year % 100 = 0 y year % 400 != 0
```

_Condition Coverage_: En el código existe un total de 3 condiciones a probar, lo que entrega un total de 6 casos.

```ruby
# 1. year % 4 = 0 (caso TRUE)
# 2. year % 4 != 0 (caso FALSE)
# 3. year % 100 = 0 (caso TRUE)
# 4. year % 100 != 0 (caso FALSE)
# 5. year % 400 = 0 (caso TRUE)
# 6. year % 400 != 0 (caso FALSE)
```

* Caso 1: [2000, 2002, 2003, 2004, 2005, 2006, 2007, 2008]
    * _Branch Coverage_: 75%
    * _Condition Coverage_: 83,33%

|  | TRUE | FALSE |
|-----------------|:----:|:-----:|
| `year % 4 == 0` | X | X |
| `year % 100 == 0` | X | X |
| `year % 400 == 0` | X |  |

* Caso 2: [4, 100, 400, 2001]
    * _Branch Coverage_: 100%
    * _Condition Coverage_: 100%

|  | TRUE | FALSE |
|-----------------|:----:|:-----:|
| `year % 4 == 0` | X | X |
| `year % 100 == 0` | X | X |
| `year % 400 == 0` | X | X |

Puntajes:

- **(0,75 pts)** por presentar diagrama de flujo que sustenta el problema.
- **(0,25 pts)** por entregar la respuesta correcta.

**c) (1.0 puntos)**

Las respuestas que se muestran a continuación son ejemplos de argumentos válidos.

1. Depende,
    * Si el proyecto permite gastar recursos para alcanzar dicho objetivo.
    * Si el código en su totalidad es testeable. Hay casos como _code legacy_ que testear el sistema es imposible.
2. Sí,
    * Al tener una serie de tests que prueben funcionalidades más críticas del sistema y que estén relacionadas con la integración del sistema o test _end-to-end_. En este caso, no es posible usar _code coverage_
    * Al referirse a _unit test_, hay que tener en cuenta que un buen _code coverage_ es un indicador necesario pero no suficiente para sustentar la calidad de la batería de tests de un software, ya que muchos tests podrían ser redundantes o entregar falsos positivos.
3. No
    * Pueden existir tests que entreguen falsos positivos o que sean redundantes y sin valor para el sistema.
    * _Code coverage_ es un métrica para _unit test_, por lo que los test de mayor nivel no se ven reflejados en esta métrica (test de integración y _end-to-end_)

Puntaje:

**Cada parte vale 1/3 del puntaje, este puntaje asignado va a depender de la calidad del argumento entregado.**
