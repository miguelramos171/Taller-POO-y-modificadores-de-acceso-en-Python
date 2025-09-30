# Taller: POO y Modificadores de Acceso en Python  

## Ejercicio 1
Dada la clase  

```python
class A:
    x = 1
    _y = 2
    __z = 3

a = A()

```
¿Cuáles de los siguientes nombres existen como atributos accesibles directamente desde a?

```
A) a.x
B) a._y
C) a.__z
D) a._A__z
```

**RTA:** A, B, D


## Ejercicio 2
```
class A:
    def __init__(self):
        self.__secret = 42

a = A()
print(hasattr(a, '__secret'), hasattr(a, '_A__secret'))
```
¿Que imprime?

**RTA:** False True


## Ejercicio 3
Responde verdadero o falso


**_a)_** El prefijo `_` impide el acceso desde fuera de la clase.  
**RTA:** es solo una convención, no impide el acceso.

**_b)_** El prefijo `__` hace imposible acceder al atributo.  
**RTA:** Falso, activa name mangling, se puede acceder como _Clase__atributo.  

**_c)_** El name mangling depende del nombre de la clase.  
**RTA:** Verdadero, el atributo __x en clase A se guarda como _A__x, en clase B sería _B__x.  


## Ejercicio 4
```python
class Base:
    def __init__(self):
        self._token = "abc"

class Sub(Base):
    def reveal(self):
        return self._token

print(Sub().reveal())
```
¿Qué se imprime y por qué no hay error de acceso?
**RTA:** abc, y no hay error porque solo tiene `_` y no `__` entonces no está restringido su acceso

## Ejercicio 5
```python
class Base:
    def __init__(self):
        self.__v = 1

class Sub(Base):
    def __init__(self):
        super().__init__()
        self.__v = 2
    def show(self):
        return (self.__v, self._Base__v)

print(Sub().show())
```
