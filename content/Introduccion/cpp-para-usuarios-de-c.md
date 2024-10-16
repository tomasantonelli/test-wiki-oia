+++
title = 'C++ para usuarios de C'
date = 2024-10-12T23:12:13-03:00
+++

En la olimpiada usamos C++, una version mejorada de C que trae varias cosas que nos facilitan la vida.

Esta sección intenta dar los puntos más utiles de C++ (en cuanto a la OIA), para un estudiante que ya conoce C.

## g++ (compilar por consola)

Para compilar codigo en C por consola, se suele usar un comando como `gcc codigo.c -o mi_ejecutable`.

En C++ es muy parecido, pero se usa el comando `g++`.

Por ejemplo, para generar un ejecutable llamado `baldosas` a partir de un archivo de codigo fuente `baldosas.cpp`, escribimos `g++ baldosas.cpp -o baldosas`

## cin y cout (entrada y salida por consola)

```c++
// documentación:
// https://en.cppreference.com/w/cpp/io/cin
// https://en.cppreference.com/w/cpp/io/cout
cin >> x >> y;  // lee valores para las variables `x` e `y` por consola.
cout << x << y; // imprime las variables `x` e `y` por consola.
```

------------

Para leer y escribir en la consola, C++ trae el paquete `<iostream>` que hace entrada y salida,
a diferencia de C, sin necesidad de explicitar los tipos de dato.

Por ejemplo, para leer dos enteros y después imprimir su suma podemos escribir el siguiente código en C.

```c
#include<stdio.h>
int main() {
    int a, b;
    scanf("%d%d", &a, &b);
    printf("%d\n", a + b);
}
```

En cambio, el paquete `<iostream>` de C++ nos permite escribir los siguiente:

```c++
#include<iostream>
using namespace std;
int main() {
    int a, b;
    cin >> a >> b;
    cout << (a + b) << '\n';
}
```

Linea por linea:

```c++
#include<iostream>
```

Incluye el paquete `<iostream>` (similar a incluir el paquete `<stdio.h>` en C)

```c++
using namespace std;
```

Esta linea nos ahorra tener que escribir `std::` al usar un componente de la biblioteca estandar de C++. Debe ir antes que el resto del codigo.

Si interesa saber mas, googleando "using namespace std" o "namespaces C++" aparece bastante rapido.

```c++
cin >> a >> b;
```

Aca leemos dos enteros por consola. Notemos que en ningun lado se especifica que a y b son enteros, sino que el paquete `<iostream>` está diseñado para darse cuenta solo.

Se puede usar `cin` para leer otras cosas, como cadenas, numeros flotantes, caracteres, y más.

```c++
cout << (a + b) << '\n';
```

`cout` se usa para imprimir a la consola y, al igual que `cin`, no necesita que se especifiquen los tipos y también se puede usar para imprimir cadenas, enteros, flotantes, etc. (por ejemplo acá mezclamos `(a+b)`, que es un entero y `'\n'`, que es un caracter)

## Estructuras

Al igual que en C, C++ permite definir tipos de datos a medida. A diferencia de C, no hace falta escribir `struct` cada vez que se nombra un tipo personalizado, por lo que tampoco hace falta "el truco del `typedef`".

```c++
struct punto {
    float x, y;
};

// En C tendriamos que escribir `struct punto p = ...;`
punto p = {3.0, 4.0};
```

Aparte de variables-miembro (como `x` e `y` en el ejemplo anterior), C++ nos deja definir funciones-miembro: funciones que van ligadas al tipo de dato y se llaman con una sintaxis especial.

Estas funciones tienen acceso a las variables de la estrucura pero, aparte de eso, son identicas a cualquier otra funcion.

```c++
#include <math.h>

struct punto {
    float x, y;

    float distancia_al_origen() {
        return sqrt(x*x + y*y);
    }
};

int main() {
    punto p = {3.0, 4.0};
    float d = p.distancia_al_origen(); // devuelve 5.0
}
```

La biblioteca estandar de C++ usa funciones de este estilo por todos lados.

## vector (manejo de arrays)

```c++
// documentación:
// https://en.cppreference.com/w/cpp/container/vector
vector<char> vec;  // declaro `vec` como un "vector de caracteres".
vec.push_back(x);  // agrega el elemento `x` al final de `vec`.
vec.size();        // devuelve la longitud de `vec`.
vec[i];            // devuelve el elemento `i`-esimo de `vec`.
```

------------

En C++ podemos crear arrays sin saber su longitud de antemano! Para esto usamos el tipo de datos `vector`, del paquete `<vector>`.

`vector` es un tipo de datos genérico, lo que significa que le tenemos que decir qué tipo de datos va a contener. Por ejemplo, para declarar un "array" de enteros, usamos el tipo de datos `vector<int>`. Para "arrays" de flotantes, usamos `vector<float>`. (`vector` puede guardar casi cualquier cosa: caracteres, cadenas, estructuras, etc.)

Por ejemplo, para declarar algunos arrays globales, podemos escribir asi:

```c++
#include<vector>
using namespace std;

vector<int> numeros_primos = {2, 3, 5, 7, 11, 13};

struct punto { float x, y; };
vector<punto> puntos_importantes;
```

`vector` nos permite consultar su tamano usando la funcion-miembro `size`.

Aparte, con `push_back` podemos ir agregando elementos usando a medida que necesitemos, y el arreglo cambia su tamano dinamicamente.

```c++
#include<vector>
using namespace std;
int main(){
    vector<int> v = {1, 2, 3};
    cout << v.size() << '\n'; // imprime 3
    v.push_back(42);
    cout << v.size() << '\n'; // imprime 4
}
```

## string (manejo de cadenas)

```c++
https://en.cppreference.com/w/cpp/header/string
```

------------

Parece razonable usar `vector<char>` para almacenar cadenas, pero C++ ya trae un tipo
de datos especifico para este caso: `string`, del paquete `<string>`.

`string` tiene mucha de la funcionalidad de `vector`, y un par de cosas mas. En
particular, podemos leer y escribir en la consola usando `cin`/`cout`, lo cual no es
posible con `vector`. Aparte, se puede iniciar usando un literal.

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
    string baldosas;

    // leemos un `string` por consola
    cin >> baldosas;

    // igual que con `vector`, podemos tomar el tamano de un `string`
    int n = baldosas.size();

    // iniciamos un `string` usando un literal
    string letras = "AVR";

    // ...

    // escribimos un `string` por consola
    cout << baldosas << '\n';
}
```