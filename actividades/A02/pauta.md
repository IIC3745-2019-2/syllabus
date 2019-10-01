# Pauta AC02

## _Predicate Coverage_

Los predicados son:

* _p1_ = `((@current_hp % 2).zero? || (@current_hp % 5).zero?) && @current_hp < 25`

* _p2_ = `!(((@current_hp % 2).zero? || (@current_hp % 5).zero?) && @current_hp < 25) && (@current_hp < 50 || other.healthier_than?(self))`

* _p3_ = `!(((@current_hp % 2).zero? || (@current_hp % 5).zero?) && @current_hp < 25) && !(@current_hp < 50 || other.healthier_than?(self))`

* _p4_ = `bonification <= 1 || (other.faster_than?(self) && @speed > 5)`

Los requisitos son que tanto _p1_, _p2_, _p3_ y _p4_ sean _T_ y _F_. Por lo tanto, se tienen los siguientes _test requirements_ (TRs):


| _TR#_ | _p1_ |
| --- |----|
|  1  | T |
|  2  | F |

| _TR#_ | _p2_ |
| --- |----|
|  3  | T |
|  4  | F |

| _TR#_ | _p3_ |
| --- |----|
|  5  | T |
|  6  | F |

| _TR#_ | _p4_ |
| --- |----|
|  7  | T |
|  8  | F |

Estos _TRs_ se pueden cubrir con _test cases_ (_TCs_) de muchas maneras, una forma sería la siguiente:

| _TC#_ | _p1_ | _p2_ | _p3_ | _p4_ | _TRs_ cubiertos |
|---|--- |--- |--- |--- | ---- |
| 1 | T  | F  | F  | T  | 1, 4, 6, 7 |
| 2 | F  | T  | F  | F  | 2, 3, 6, 8 |
| 3 | F  | F  | T  | F  | 2, 4, 5, 8 |

Por ejemplo, con los casos de pruebas 1, 2 y 3 se tiene _coverage_ completo según _PC_.


### Tests

Algunos ejemplo de _tests_ que representan estos casos de prueba son:

```ruby
class PC < Minitest::Test
  def setup
    @pokemon1 = Pokemon.new('Charmander', 'Fire', 20, 7, 6, 3)
    @pokemon2 = Pokemon.new('Squirtle', 'Water', 49, 6, 6, 4)
    @pokemon3 = Pokemon.new('Bulbasaur', 'Grass', 51, 6, 6, 5)
  end

  def test_case_1
    # covers TRs: 1, 4, 6 and 7
    assert @pokemon1.attack(@pokemon2) == 15.0
  end

  def test_case_2
    # covers TRs: 2, 3, 6 and 8
    assert @pokemon2.attack(@pokemon3) == 4.5
  end

  def test_case_3
    # covers TRs: 2, 4, 5 and 8
    assert @pokemon3.attack(@pokemon2) == 7.0
  end

  def teardown
    # Innecesario porque cada test no tiene persistencia (base de datos, archivos, etc)
  end
end
```

## _Clause Coverage_

Las cláusulas son:

* _a_ = `(@current_hp % 2).zero?`

* _b_ = `(@current_hp % 5).zero?`

* _c_ = `@current_hp < 25`

* _d_ = `@current_hp < 50`

* _e_ = `other.healthier_than?(self)`

* _f_ = `bonification <= 1`

* _g_ = `other.faster_than?(self)`

* _h_ = `@speed > 5`

Los requisitos son que tanto _a_, _b_, _c_, _d_, _e_, _f_, _g_, _h_ sean _T_ y _F_. Por lo tanto, los _TRs_ son:


| _TR#_ | _a_ |
| --- |---|
|  1  | T |
|  2  | F |

| _TR#_ | _b_ |
| --- |---|
|  3  | T |
|  4  | F |

| _TR#_ | _c_ |
| --- |---|
|  5  | T |
|  6  | F |

| _TR#_ | _d_ |
| --- |---|
|  7  | T |
|  8  | F |

| _TR#_ | _e_ |
| --- |---|
|  9  | T |
| 10  | F |

| _TR#_ | _f_ |
| --- |---|
| 11  | T |
| 12  | F |

| _TR#_ | _g_ |
| --- |---|
| 13  | T |
| 14  | F |

| _TR#_ | _h_ |
| --- |---|
| 15  | T |
| 16  | F |

Combinados, nos quedan los siguientes _TCs_:

| _TC#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _f_ | _g_ | _h_ | _TR_ cubiertos |
|-----|---|---|---|---|---|---|---|---|--------------|
| 1 | T | T | T | T | T | T | T | T | 1, 3, 5, 7, 9, 11, 13, 15 |
| 2 | F | F | F | F | F | F | F | F | 2, 4, 6, 8, 10, 12, 14, 16 |

Por ejemplo, con los casos 1 y 2 se tiene _coverage_ completo según _CC_.

### Tests

Algunos ejemplos de _tests_ que representan estos casos de prueba son:

```ruby
class PC < Minitest::Test
  def setup
    # Innecesario porque en test se inicializan distintos pokémones
  end

  def test_case_1
    # covers TRs: 1, 3, 5, 7, 9, 11, 13, 15
    pokemon1 = Pokemon.new('Charmander', 'Fire', 10, 7, 6, 6)
    pokemon2 = Pokemon.new('Squirtle', 'Water', 11, 6, 6, 7)
    assert pokemon1.attack(pokemon2) == 15.0
  end

  def test_case_2
    # covers TRs: 2, 4, 6, 8, 10, 12, 14, 16
    pokemon1 = Pokemon.new('Squirtle', 'Water', 51, 6, 6, 4)
    pokemon2 = Pokemon.new('Charmander', 'Fire', 50, 6, 6, 3)
    assert pokemon1.attack(pokemon2) == 7.0
  end
end
```

## _Restricted Active Clause Coverage_

En este criterio, las cláusulas y los predicados son los mismos que en _CC_ y _PC_.

Los requisitos son que para cada predicado y para cada cláusula mayor en ese predicado, se tenga que cada cláusula mayor determine el predicado con la restricción de que las cláusula menores deben tener los mismos valores para ambos casos.

### Primer predicado

El primer predicado es de la forma:

* _p1_ = `(a || b) && c`

#### Cláusula activa: a

Para que el valor del predicado dependa de la cláusula `a` se debe tener que `b` sea _F_ y `c` sea _T_. Por ejemplo, se tienen los siguientes _TRs_:

| _TR#_ | _a_     | _b_ | _c_ | _p1_    |
|---|---    |---|---|---    |
| 1 | **T** | F | T | **T** |
| 2 | **F** | F | T | **F** |

#### Cláusula activa: b

Con respecto a `b`, `a` debe ser _F_ y `c` debe ser _T_:

| _TR#_ | _a_ | _b_     | _c_ | _p1_    |
|---|---|---    |---|---    |
| 3 | F | **T** | T | **T** |
| 4 | F | **F** | T | **F** |

#### Cláusula activa: c

Con respecto a `c`,  `a` o `b` deben ser _T_:

| _TR#_ | _a_ | _b_ | _c_     | _p1_    |
|---|---|---|---    |---    |
| 5 | T | F | **T** | **T** |
| 6 | T | F | **F** | **F** |

#### Resumen primer predicado

Por lo tanto, combinando estos requisitos en casos de tests nos queda:

|_TC#_| _a_ | _b_ | _c_ | _TR_ cubiertos |
|---|---|---|---| --- |
| 1 | T | F | T | 1, 5 |
| 2 | F | F | T | 2, 4 |
| 3 | F | T | T | 3 |
| 4 | T | F | F | 6 |

### Segundo predicado

Con respecto al segundo predicado, se realiza el trabajo de manera similar. Se tiene la siguiente forma:

* _p2_ = `!((a || b) && c) && (d || e)`


#### Cláusula activa: a

De la misma forma que en el predicado anterior, debemos buscar la combinación de `b`, `c`, `d` y `e` para que el predicado dependa de `a`. En este caso, para que el predicado dependa de `a`, `b` debe ser _F_, `c` debe ser _T_ y `d` o `e` deben ser _T_. Por lo tanto, se pueden tener las combinaciones:

| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p2_ |
|---|---|---|---|---|---|---|
| 7 | **T** | F | T | T | F | **F** |
| 8 | **F** | F | T | T | F | **T** |


#### Cláusula activa: b

Análogamente, para que el predicado dependa de `b`: `a` debe ser _F_, `c` debe ser _T_ y `d` o `e` deben ser _T_. Por lo tanto, se tiene las siguientes combinaciones:


| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p2_ |
|---|---|---|---|---|---|---|
| 9 | F | **T** | T | T | F | **F** |
|10 | F | **F** | T | T | F | **T** |


#### Cláusula activa: c

Para que el predicado dependa de `c`: `a` o `b` deben ser _T_ y `d` o `e` deben ser _T_. Las combinaciones que se pueden tener son las siguientes:

| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p2_ |
|---|---|---|---|---|---|---|
|11 | T | F | **T** | T | F | **F** |
|12 | T | F | **F** | T | F | **T** |


#### Cláusula activa: d

Para que el predicado dependa de `d` o `e`, como mínimo se tiene que el _sub_-predicado `!((a || b) && c)` debe ser _T_. Para lograr esto, se pueden tener muchas combinaciones.

La escogida será:

| _a_ | _b_ | _c_ | `!(a || b && c)` |
| ---|---|---|--------|
| T | F | F | T |


Para que dependa de `d`: `!((a || b) && c)` debe ser _T_ y `e` debe ser _F_. Por lo tanto, se tiene:

| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p2_ |
|---|---|---|---|---|---|---|
|13 | T | F | F | **T** | F | **T** |
|14 | T | F | F | **F** | F | **F** |


#### Cláusula activa: e

Por último, para que el predicado dependa de `e`: `!((a || b) && c)` debe ser _T_ y `d` debe ser _F_. Por lo tanto, se tiene:

| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p2_ |
|---|---|---|---|---|---|---|
|15 | T | F | F | F | **T** | **T** |
|16 | T | F | F | F | **F** | **F** |

### Resumen primer y segundo predicado

Combinando estos requisitos con los anteriores, nuestra tabla de casos de prueba va creciendo:

| _TC#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _TR_ cubiertos |
|---|---|---|---|---|---| ---- |
| 1 | T | F | T | T | F | 1, 5, 7, 11 |
| 2 | F | F | T | T | F | 2, 5, 8, 10 |
| 3 | F | T | T | T | F | 3, 9 |
| 4 | T | F | F | T | F | 6, 12, 13 |
| 5 | T | F | F | F | F | 14, 16 |
| 6 | T | F | F | F | T | 15 |

### Tercer predicado

El siguiente predicado es de la forma:

* _p3_ = `!((a || b) && c) && !(d || e)`

#### Cláusula a

Para que el predicado dependa a `a`, `b` debe ser _F_, `c` debe ser _T_ y `d` y `e` deben ser _F_.


| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p3_ |
|---|---|---|---|---|---|---|
|17 | **T** | F | T | F | F | **F** |
|18 | **F** | F | T | F | F | **T** |

Algo curioso es que dado que existen cláusulas dependientes, pueden haber casos de prueba infactibles. Esto lo podemos ver con las cláusulas c y d, las cuales son:

* _c_ = `@current_hp < 25`

* _d_ = `@current_hp < 50`

Lo cual nos deja fuera el caso en que `c` sea _T_ y `d` sea _F_. Esto nos deja con que los dos _TRs_ 17 y 18 sean infactibles.

#### Cláusula b

Para que el predicado dependa de `b`, `a` debe ser _F_, `c` debe ser _T_ y `d` y `e` deben ser _F_.

| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p3_ |
|---|---|---|---|---|---|---|
|19 | F | **T** | T | F | F | **F** |
|20 | F | **F** | T | F | F | **T** |

De la misma forma, los TRs 19 y 20 son infactibles.

#### Cláusula c

Para que el predicado dependa de `c`, `a` o `b` debe ser _T_, y `d` y `e` deben ser _F_.


| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p3_ |
|---|---|---|---|---|---|---|
|21 | T | F | **T** | F | F | **F** |
|22 | T | F | **F** | F | F | **T** |


En este caso, sólo el _TR_ 21 es infactible.

#### Cláusula d

Análogamente, para que el predicado dependa de `d` o `e`, como mínimo se tiene que el _sub_-predicado `!(a || b && c)` debe ser _T_. Para lograr esto, se pueden tener muchas combinaciones.

La escogida será:

| _a_ | _b_ | _c_ | `!(a || b && c)` |
| ---|---|---|--------|
| T | F | F | T |

Para que el predicado dependa de `d`, `e` debe ser _F_:


| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p3_ |
|---|---|---|---|---|---|---|
|23 | T | F | F | **T** | F | **F** |
|24 | T | F | F | **F** | F | **T** |

#### Cláusula e

Para que dependa de `c`, `d` debe ser _F_:


| _TR#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _p3_ |
|---|---|---|---|---|---|---|
|25 | T | F | F | F | **T** | **F** |
|26 | T | F | F | F | **F** | **T** |

### Resumen primer, segundo y tercer predicado

Combinando estos requisitos con los anteriores, nuestra tabla de casos de prueba va creciendo:

| _TC#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _TR_ cubiertos |
|---|---|---|---|---|---| ---- |
| 1 | T | F | T | T | F | 1, 5, 7, 11 |
| 2 | F | F | T | T | F | 2, 5, 8, 10 |
| 3 | F | T | T | T | F | 3, 9 |
| 4 | T | F | F | T | F | 6, 12, 13, 23 |
| 5 | T | F | F | F | F | 14, 16, 22, 24, 26 |
| 6 | T | F | F | F | T | 15, 25 |

### Cuarto predicado

El último predicado es de la forma:

* _p4_ = `f || (g && h)`

#### Cláusula f

Para que se cubra con respecto a `f`, `g` o `h` deben ser _F_.

| _TC#_ | _f_     | _g_ | _h_ | _p4_    |
|---|---    |---|---|---    |
| 27 | **T** | T | F | **T** |
| 28 | **F** | T | F | **F** |


#### Cláusula g

Para cubrirlo con respecto a `g`, `f` debe ser _F_ y `h` debe ser _T_.

| _TC#_ | _f_     | _g_ | _h_ | _p4_    |
|---|---|---    |---|---    |
| 29 | F | **T** | T | **T** |
| 30 | F | **F** | T | **F** |


#### Cláusula h

Para cubrirlo con respecto a `h`, `f` debe ser _F_ y `g` debe ser _T_.

| _TC#_ | _f_     | _g_ | _h_ | _p4_    |
|---|---|---|---    |---    |
| 31 | F | T | **F** | **F** |
| 32 | F | T | **T** | **T** |

### Resumen 4 predicados

Combinando todos los requisitos del cuarto predicado, nuestra tabla de casos de prueba queda como:

| _TC#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _f_ | _g_ | _h_ | _TR_ cubiertos |
|---|---|---|---|---|---|---|---|---    | ---- |
| 1 | T | F | T | T | F | T | T | F | 1, 5, 7, 11, 27 |
| 2 | F | F | T | T | F | F | T | F | 2, 5, 8, 10, 28, 31 |
| 3 | F | T | T | T | F | F | T | T | 3, 9, 29, 32 |
| 4 | T | F | F | T | F | F | F | T | 6, 12, 13, 23, 30 |
| 5 | T | F | F | F | F | - | - | - | 14, 16, 22, 24, 26 |
| 6 | T | F | F | F | T | - | - | - | 15, 25 |

Con esto tenemos el _coverage_ completo por lo que podemos dejar cualquier valor de `f`, `g` y `h` para los casos 5, 6, 7, 8, 9 y 10. En este ejemplo, completaremos con los mismas combinaciones existentes.

## Casos de prueba

Combinando todos los requisitos, nuestra tabla de casos de prueba queda como:

| _TC#_ | _a_ | _b_ | _c_ | _d_ | _e_ | _f_ | _g_ | _h_ | _TR_ cubiertos |
|---|---|---|---|---|---|---|---|---    | ---- |
| 1 | T | F | T | T | F | T | T | F | 1, 5, 7, 11, 27 |
| 2 | F | F | T | T | F | F | T | F | 2, 5, 8, 10, 28, 31 |
| 3 | F | T | T | T | F | F | T | T | 3, 9, 29, 32 |
| 4 | T | F | F | T | F | F | F | T | 6, 12, 13, 23, 30 |
| 5 | T | F | F | F | F | T | T | F | 14, 16, 22, 24, 26, 27 |
| 6 | T | F | F | F | T | F | T | F | 15, 25, 28, 31 |


### Tests

Algunos _tests_ de ejemplo serían:

```ruby
class PC < Minitest::Test
  def setup
    # Innecesario porque cada test debe inicializar distintos pokémones
  end

  def test_case_1
    # covers TRs: 1, 5, 7, 11, 27
    pokemon1 = Pokemon.new('Charmander', 'Fire', 12, 7, 6, 4)
    pokemon2 = Pokemon.new('Squirtle', 'Water', 11, 6, 6, 5)
    assert pokemon1.attack(pokemon2) == 15.0
  end

  def test_case_2
    # covers TRs: 2, 5, 8, 10, 28, 31
    pokemon1 = Pokemon.new('Squirtle', 'Water', 11, 6, 6, 5)
    pokemon2 = Pokemon.new('Charmander', 'Fire', 5, 6, 6, 6)
    assert pokemon1.attack(pokemon2) == 18.0
  end

  def test_case_3
    # covers TRs: 3, 9, 29, 32
    pokemon1 = Pokemon.new('Charmander', 'Fire', 5, 6, 6, 6)
    pokemon2 = Pokemon.new('Squirtle', 'Water', 5, 6, 6, 7)
    assert pokemon1.attack(pokemon2) == 7.5
  end

  def test_case_4
    # covers TRs: 6, 12, 13, 23, 30
    pokemon1 = Pokemon.new('Squirtle', 'Water', 26, 6, 6, 7)
    pokemon2 = Pokemon.new('Charmander', 'Fire', 5, 6, 6, 6)
    assert pokemon1.attack(pokemon2) == 18.0
  end

  def test_case_5
    # covers TR: 14, 16, 22, 24, 26, 27
    pokemon1 = Pokemon.new('Charmander', 'Fire', 54, 6, 6, 4)
    pokemon2 = Pokemon.new('Squirtle', 'Water', 5, 6, 6, 7)
    assert pokemon1.attack(pokemon2) == 3.0
  end

  def test_case_6
    # covers TRs: 15, 25, 28, 31
    pokemon1 = Pokemon.new('Squirtle', 'Water', 52, 6, 6, 3)
    pokemon2 = Pokemon.new('Charmander', 'Fire', 54, 6, 6, 4)
    assert pokemon1.attack(pokemon2) == 18.0
  end

  def teardown
    # Innecesario porque cada test no tiene persistencia (base de datos, archivos, etc)
  end
end
```

## _Correlated Active Clause Coverage_

Revisando los casos de prueba para _RACC_ que permitirían modificar los casos para _CACC_, nos damos cuenta que estos no reducirían la cantidad de pruebas necesarias. Por esta razón podemos aprovechamos los casos de prueba ya formalizados para _RACC_ y así cubrir de forma completa y mínima bajo el criterio _CACC_ con estos también.
