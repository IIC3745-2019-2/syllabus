# Pauta AC03

## Predicados

* p1 = `ingredients.include?('Tomato') && ingredients.include?('Cheese')`
* p2 = `ingredients.include?('Tomato') && ingredients.include?('Cheese') && (ingredients.include?('Ham') || ingredients.include?('Olives'))`
* p3 = `!(ingredients.include?('Cheese') || ingredients.include?('Extra cheese'))`

## Cláusulas

* c1 = `ingredients.include?('Tomato')`
* c2 = `ingredients.include?('Cheese')`
* c3 = `ingredients.include?('Ham')`
* c4 = `ingredients.include?('Olives')`
* c5 = `ingredients.include?('Extra cheese')`

## _Correlated Active Clause Coverage_

### Primer predicado

* _p1_ = `c1 && c2`

#### Cláusula activa: c1

| _TR#_ | _c1_  | _c2_ | _p1_  |
| ---   | ---   | ---  | ---   |
| 1     | **T** | T    | **T** |
| 2     | **F** | T    | **F** |

#### Cláusula activa: c2

| _TR#_ | _c1_ | _c2_  | _p1_  |
| ---   | ---  | ---   | ---   |
| 3     | T    | **T** | **T** |
| 4     | T    | **F** | **F** |

### Segundo predicado

* _p2_ = `c1 && c2 && (c3 || c4 )`

#### Cláusula activa: c1

| _TR#_ | _c1_  | _c2_ | _c3_ | _c4_ | _p2_  |
| ---   | ---   | ---  | ---  | ---  | ---   |
| 5     | **T** | T    | T/F  | F/T  | **T** |
| 6     | **F** | T    | T/F  | F/T  | **F** |

#### Cláusula activa: c2

| _TR#_ | _c1_ | _c2_  | _c3_ | _c4_ | _p2_  |
| ---   | ---  | ---   | ---  | ---  | ---   |
| 7     | T    | **T** | T/F  | F/T  | **T** |
| 8     | T    | **F** | T/F  | F/T  | **F** |

#### Cláusula activa: c3

| _TR#_ | _c1_ | _c2_ | _c3_  | _c4_ | _p2_  |
| ---   | ---  | ---  | ---   | ---  | ---   |
| 9     | T    | T    | **T** | F    | **T** |
| 10    | T    | T    | **F** | F    | **F** |

#### Cláusula activa: c4

| _TR#_ | _c1_ | _c2_ | _c3_ | _c4_  | _p2_  |
| ---   | ---  | ---  | ---  | ---   | ---   |
| 11    | T    | T    | F    | **T** | **T** |
| 12    | T    | T    | F    | **F** | **F** |

### Tercer predicado

* _p3_ = `!(c2 || c5)`

#### Cláusula activa: c2

| _TR#_ | _c2_  | _c5_ | _p3_  |
| ---   | ---   | ---  | ---   |
| 13    | **T** | F    | **F** |
| 14    | **F** | F    | **T** |

#### Cláusula activa: c5

| _TR#_ | _c2_ | _c5_  | _p3_  |
| ---   | ---  | ---   | ---   |
| 15    | F    | **T** | **F** |
| 16    | F    | **F** | **T** |

### Casos de pruebas

| _TC#_ | _c1_ | _c2_ | _c3_ | _c4_ | _c5_ | _TR_ cubiertos    | Input                    | Output                             |
| ---   | ---  | ---  | ---  | ---  | ---  | ---               | ---                      | ---                                |
| 1     | T    | T    | T    | F    | F    | 1, 3, 5, 7, 9, 13 | [Tomato, Cheese, Ham]    | Neapolitan Classic                 |
| 2     | T    | T    | F    | F    | -    | 10, 12            | [Tomato, Cheese]         | Classic From da house              |
| 3     | T    | T    | F    | T    | -    | 11                | [Tomato, Cheese, Olives] | Neapolitan Classic                 |
| 4     | F    | T    | T    | T    | -    | 2, 6              | [Cheese, Ham, Olives]    | Pizza From da house                |
| 5     | T    | F    | T    | T    | F    | 4, 8, 14, 16      | [Tomato, Ham, Olives]    | Pizza From da house Without Cheese |
| 6     | -    | F    | -    | -    | T    | 15                | [Extra Cheese]           | Pizza From da house                |

## _General Inactive Clause Coverage_

### Primer predicado

* _p1_ = `c1 && c2`

#### Cláusula activa: c1

| _TR#_ | _c1_  | _c2_ | _p1_  |
| ---   | ---   | ---  | ---   |
| 1     | **T** | T    | **T** |
| 2     | **T** | F    | **F** |
| 3     | **F** | T/F  | **F** |

#### Cláusula activa: c2

| _TR#_ | _c1_ | _c2_  | _p1_  |
| ---   | ---  | ---   | ---   |
| 4     | T    | **T** | **T** |
| 5     | F    | **T** | **F** |
| 6     | T/F  | **F** | **F** |

### Segundo predicado

* _p2_ = `c1 && c2 && (c3 || c4 )`

#### Cláusula activa: c1

| _TR#_ | _c1_  | _c2_ | _c3_ | _c4_ | _p2_  |
| ---   | ---   | ---  | ---  | ---  | ---   |
| 7     | **T** | T    | T/F  | F/T  | **T** |
| 8     | **T** | T/F  | T/F  | F/T  | **F** |
| 9     | **F** | T/F  | T/F  | T/F  | **F** |

#### Cláusula activa: c2

| _TR#_ | _c1_ | _c2_  | _c3_ | _c4_ | _p2_  |
| ---   | ---  | ---   | ---  | ---  | ---   |
| 10    | T    | **T** | T/F  | F/T  | **T** |
| 11    | T/F  | **T** | T/F  | F/T  | **F** |
| 12    | T/F  | **F** | T/F  | F/T  | **F** |

#### Cláusula activa: c3

| _TR#_ | _c1_ | _c2_ | _c3_  | _c4_ | _p2_  |
| ---   | ---  | ---  | ---   | ---  | ---   |
| 13    |  T   | T    | **T** | T/F  | **T** |
| 14    |  T   | T    | **F** | T    | **T** |
| 15    |  F/T | T/F  | **T** | F/T  | **F** |
| 16    |  F/T | T/F  | **F** | F/T  | **F** |

#### Cláusula activa: c4

| _TR#_ | _c1_ | _c2_ | _c3_ | _c4_  | _p2_  |
| ---   | ---  | ---  | ---  | ---   | ---   |
| 17    |  T   | T    | T/F  | **T** | **T** |
| 18    |  T   | T    | T    | **F** | **T** |
| 19    |  F/T | T/F  | F/T  | **T** | **F** |
| 20    |  F/T | T/F  | F/T  | **F** | **F** |

### Tercer predicado

* _p3_ = `!(c2 || c5)`

#### Cláusula activa: c2

| _TR#_ | _c2_  | _c5_ | _p3_  |
| ---   | ---   | ---  | ---   |
| 21    | **F** | F    | **T** |
| 22    | **T** | T/F  | **F** |
| 23    | **F** | T    | **F** |

#### Cláusula activa: c5

| _TR#_ | _c2_ | _c5_  | _p3_  |
| ---   | ---  | ---   | ---   |
| 24    | F    | **F** | **T** |
| 25    | T/F  | **T** | **F** |
| 26    | T    | **F** | **F** |

### Casos de pruebas

| _TC#_ | _c1_ | _c2_ | _c3_ | _c4_ | _c5_ | _TR_ cubiertos              | Input                               | Output                             |
| ---   | ---  | ---  | ---  | ---  | ---  | ---                         | ---                                 | ---                                |
| 1     | T    | T    | T    | F    | T    | 8, 13, 18, 25               | [Tomato, Cheese, Ham, Extra Cheese] | Neapolitan Classic                 |
| 2     | T    | T    | F    | T    | F    | 1, 4, 7, 10, 14, 17, 22, 26 | [Tomato, Cheese, Olives]            | Neapolitan Classic                 |
| 3     | T    | F    | T    | T    | T    | 2, 6, 12, 15, 19, 23        | [Tomato, Ham, Olives, Extra Cheese] | Pizza From da house                |
| 4     | F    | T    | F    | F    | -    | 3, 5, 9, 11, 16, 20         | [Cheese]                            | Pizza From da house                |
| 5     | -    | F    | -    | -    | F    | 21, 24                      | []                                  | Pizza From da house Without Cheese |
