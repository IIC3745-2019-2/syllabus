# IIC3745 - Testing - Actividad 1

## Diseño de pruebas

Su empresa ha decidido validar los emails de los usuarios que se inscriben en su plataforma debido a que al parecer no reciben los correos.

Se ha pensado que como los usuarios son las únicas entidades que necesitan verificar el email, este modelo tendrá un método `validate_email(email)` que recibe un email y retorna `true` si este es un email válido y `false` en caso contrario.

Un email válido debe tener sólo caracteres alfanuméricos, además, puede tener puntos (`.`) y guiones bajos (`_`). También debe tener un dominio válido con tamaño máximo 67.

**a)** Diseñe casos de prueba con su resultado esperado para la función `validate_email(email)`. Es decir, escriba todos los casos útiles que se le ocurran para poder probar si la función está realizando su trabajo correctamente.

**b)** Implemente en _ruby_ la función `validate_email(email)` que cumpla con lo pedido y valide que los casos de prueba descritos anteriormente son exitosos.

**c)** ¿Está función soluciona el problema de la empresa? Justifique con un máximo de 5 líneas.

## Code Coverage

_Code coverage_ corresponde a una medida de _testing_ que indica el porcentaje de código que fue ejecutado bajo una baterías de tests. Este porcentaje está sujeto a diferentes criterios dependiendo del enfoque con que se quiera medir. Para efectos de esta actividad solamente se tendrá en cuenta 3 criterios de cobertura:

1. _Statement Coverage_: Cantidad de líneas de código ejecutadas sobre la cantidad total de líneas de código.
2. _Branch Coverage_: Cantidad de ramas condicionales creadas en la ejecución del código (e.g. `if`/`else`). Esta métrica indica la cantidad de divisiones en el programa.
3. [_Condition Coverage_](https://www.youtube.com/watch?v=ZnPmJd5aqyw): Cantidad de condiciones booleanas evaluadas sobre la cantidad total de posibles valores que pueden tomar las condiciones booleanas.

**a)** A continuación se muestra un método para pagar deudas, este toma como _input_ el saldo del usuario (`balance`) y una instancia del objeto `Debt` (`debt`) que representa la deuda a pagar y retorna el saldo final del usuario. Analice el código y diseñe los casos de prueba **mínimos** para alcanzar un _code coverage_ del 100% bajo los siguientes criterios:

* _Statement Coverage_
* _Branch Coverage_
* _Condition Coverage_

```ruby
class Debt
  def initialize(id, value, paid)
     @debt_id = id
     @value = value
     @paid = paid
  end
end

def pay_debt(balance, debt)
   dif = balance - debt.value
   if dif >= 0 && !debt.paid
       debt.paid = true
       balance = dif
       puts "Debt paid."
       if dif == 0
           puts "But your balance is $0 now."
       end
   else
       if debt.paid
           puts "The debt is already paid."
       else
           puts "Insufficient funds."
       end
   end
   return balance
end
```

**b)** Como todos saben, la duración del año trópico es de 365 días, 5 horas, 48 minutos y 45 segundos. Debido a este desfase con el calendario común se dio origen a los años bisiestos. Para que un año sea considerado bisiesto se debe cumplir con que:

* El año debe ser divisible por 4.
* Pero si el año es divisible por 100, entonces este no es bisiesto.
* A su vez, si es divisible por 400, entonces es bisiesto.

Se desea probar un programa<sup>1</sup> que indica si un año es bisiesto o no. Para esto se usa dos series de años de prueba que se indican a continuación:

1. [2000, 2002, 2003, 2004, 2005, 2006, 2007, 2008]
2. [4, 100, 400, 2001]

En base a un grafo de control de flujo responda: ¿cuál de los conjuntos de casos de prueba anteriores presenta mayor _condition coverage_ y _branch coverage_?

<sup>1</sup> Como puede ver, el caso anterior corresponde a _black box testing_, haga su mejor esfuerzo para inferir la lógica del programa.

**c)** Conceptos: para cada una de las siguiente preguntas justifique su respuesta con un máximo de 5 líneas:

1. ¿Es aceptable tener un _code coverage_ menor al 100%?
2. ¿Es posible tener una batería de tests confiable si no se mide el _code coverage_?
3. ¿Mi código esta libre de _bugs_ si pasa todas las pruebas y tiene un _code coverage_ del 100%?
