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
### ¿Cuáles de los siguientes nombres existen como atributos accesibles directamente desde a?

```
A) a.x
B) a._y
C) a.__z
D) a._A__z
```

**RTA:** A, B, D


## Ejercicio 2
```python
class A:
    def __init__(self):
        self.__secret = 42

a = A()
print(hasattr(a, '__secret'), hasattr(a, '_A__secret'))
```
### ¿Que imprime?

**RTA:** False True


## Ejercicio 3
### Responde verdadero o falso


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
### ¿Qué se imprime y por qué no hay error de acceso?
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
### ¿Cual es la salida?
**RTA:** (2, 1)

## Ejercicio 6
```python
class Caja:
    __slots__ = ('x',)

c = Caja()
c.x = 10
c.y = 20
```
### ¿Qué ocurre y por qué?
**RTA:** Ocurre un AttributeError al intentar asignar c.y = 20.


Al definir `__slots__ = ('x',)`, se restrinje la creacion de nuevos atributos como en este caso `y`

## Ejercicio 7
### Completa para que b tenga un atributo “protegido por convención”.

```python
class B:
    def __init__(self):
        self.______ = 99
```

**RTA:** 
```python
class B:
    def __init__(self):
        self._num = 99
```


## Ejercicio 8
```python
class M:
    def __init__(self):
        self._state = 0
    def _step(self):
        self._state += 1
        return self._state
    def __tick(self):
        return self._step()

m = M()
print(hasattr(m, '_step'), hasattr(m, '__tick'), hasattr(m, '_M__tick'))
```

### ¿Qué imprime y por qué?

**RTA:** imprime `True False True`, porque 

`_step` existe y es accesible (True)

`__tick` se transforma por name mangling a _M__tick, por lo que no existe (False)

`_M__tick` sí existe (True)


## Ejercicio 9

```python
class S:
    def __init__(self):
        self.__data = [1, 2]
    def size(self):
        return len(self.__data)

s = S()
```


Accede a __data (solo para comprobar), sin modificar el código de la clase: Escribe una línea que obtenga la lista usando name mangling y la imprima.

### Escribe la línea solicitada.

**RTA:** 
```python 
print(s._S__data)
```


## Ejercicio 10
```python
class D:
    def __init__(self):
        self.__a = 1
        self._b = 2
        self.c = 3

d = D()
names = [n for n in dir(d) if 'a' in n]
print(names)
```

**RTA:** El atributo `__a` sufre name mangling por lo que queda `_D__a`, por eso en `dir(d)` veremos `_D__a`


