# Homework JavaScript Avanzado I

## Scope & Hoisting

Determiná que será impreso en la consola, sin ejecutar el código.

> Investiga cuál es la diferencia entre declarar una variable con `var` y directamente asignarle un valor.

```javascript
x = 1;
var a = 5;
var b = 10;
var c = function (a, b, c) {
   var x = 10;
   console.log(x); //10
   console.log(a); //8
   var f = function (a, b, c) {
      b = a;
      console.log(b); //8
      b = c;
      var x = 5;
   };
   f(a, b, c);
   console.log(b); //9
};
c(8, 9, 10);
console.log(b); //10
console.log(x); //1
```

```javascript
console.log(bar); //undefined
console.log(baz); //undefined en ES5. En ES6 devuelve ReferenceError
foo();
function foo() {
   console.log('Hola!'); //Hola! en ES5. En ES6 este codigo no se ejecuta porque está después del error
}
var bar = 1;
baz = 2;
```

```javascript
var instructor = 'Tony';
if (true) {
   var instructor = 'Franco';
}
console.log(instructor); //Franco
//var permite declarar mas de 1 vez una variable, cosa que no ocurre con let
```

```javascript
var instructor = 'Tony';
console.log(instructor); //Tony
(function () {
   if (true) {
      var instructor = 'Franco';
      console.log(instructor); //Franco
   }
})();
console.log(instructor); //Tony
//var globalmente vale 'Tony'
```

```javascript
var instructor = 'Tony';
let pm = 'Franco';
if (true) {
   var instructor = 'The Flash';
   let pm = 'Reverse Flash';
   console.log(instructor); //The Flash
   console.log(pm); //Reverse Flash
}
console.log(instructor); //The Flash
console.log(pm); //Franco
//el var dentro del if modifica al var fuera del if
//En cambio el let dentro del if tiene su scope dentro de ese if y fuera del if tiene el valor global Franco para este caso
```

### Coerción de Datos

¿Cuál crees que será el resultado de la ejecución de estas operaciones?:

```javascript
6 / "3" //2
"2" * "3" //6
4 + 5 + "px" //9px
"$" + 4 + 5 //$45
"4" - 2 //2
"4px" - 2 //NaN
7 / 0 //Infinity
{}[0] //Object o undefined
parseInt("09") //9
5 && 2 //2
2 && 5 //5
5 || 0 //5
0 || 5 //0
[3]+[3]-[10] //23 porque por precedencia primero hace la concatenacion de 3 y 3 y despues convierte eso a numero y le resta 10
3>2>1 //false porque primero hace 3>2 da true y despues hace convierte true a numero que sería 1 y compara 1>1 y da false
[] == ![] //true porque por coerción [] es igual a "", ![] es igual a false, luego se convierte "" a 0 y false tambien a 0 entonces da true
```

> Si te quedó alguna duda repasá con [este artículo](http://javascript.info/tutorial/object-conversion).

### Hoisting

¿Cuál es el output o salida en consola luego de ejecutar este código? Explicar por qué:

```javascript
function test() {
   console.log(a);
   console.log(foo());

   var a = 1;
   function foo() {
      return 2;
   }
}

test();
//undefined
//2
//a es undefined porque en el contexto de ejecución de test var por hoisting se declara pero no se inicializa
//foo se ejecuta por hoisting aunque haya sido llamada antes de declararse y retorna 2
```

Y el de este código? :

```javascript
var snack = 'Meow Mix';

function getFood(food) {
   if (food) {
      var snack = 'Friskies';
      return snack;
   }
   return snack;
}

getFood(false);
//undefined
//porque por hoisting la variable var se inicializa dentro del contexto de ejecucion de la funcion pero no toma ningun valor al ser false la condicion del if. Por lo tanto se retorna undefined localmente dentro de la funcion.
//En realidad por consola no sale nada porque no hay un console.log() pero el getFood(false) devuelve undefined
```

### This

¿Cuál es el output o salida en consola luego de ejecutar esté código? Explicar por qué:

```javascript
var fullname = 'Juan Perez';
var obj = {
   fullname: 'Natalia Nerea',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function () {
         return this.fullname;
      },
   },
};

console.log(obj.prop.getFullname()); //Aurelio De Rosa

var test = obj.prop.getFullname;

console.log(test()); //undefined
```

### Event loop

Considerando el siguiente código, ¿Cuál sería el orden en el que se muestra por consola? ¿Por qué?

```javascript
function printing() {
   console.log(1);
   setTimeout(function () {
      console.log(2);
   }, 1000);
   setTimeout(function () {
      console.log(3);
   }, 0);
   console.log(4);
}

printing();
//1
//4
//3
//2
```

</br >

---

## **✅ FEEDBACK**

### Usa este [**formulario**](https://docs.google.com/forms/d/e/1FAIpQLSe1MybH_Y-xcp1RP0jKPLndLdJYg8cwyHkSb9MwSrEjoxyzWg/viewform) para reportar tus observaciones de mejora o errores. Tu feedback es muy importante para seguir mejorando el modelo educativo.
