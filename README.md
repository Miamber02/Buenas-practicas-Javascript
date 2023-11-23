# Buenas practicas programando en JS

Recopilación de buenas prácticas programando en Javascript, inspirado en el libro Clean Code, de Robert Martin. Este trabajo ha sido realizado por los alumnos de 2ºDAW del IES Fernando III (2023-24).

## Indice
- [Variables](#variables)
- [Funciones](#funciones)
- [Objetos y estructuras de datos](#objetos-y-estructuras-de-datos)
- [Clases](#clases)
- [Principios SOLID](#principios-solid)
- [Concurrencia](#concurrencia)
- [Manejo de errores](#manejo-de-errores)
- [Formato](#formato)
- [Comentarios](#comentarios)


# Variables
  Para mejorar la legibilidad y mantenibilidad de tu código, haciendo que sea más fácil de entender y menos propenso a errores, la consistencia en la elección de nombres es clave para desarrollar un código limpio y comprensible.

## Nombrando variables :

### Utiliza nombres descriptivos:
Al elegir nombres para tus variables, elige palabras que describan claramente el propósito o contenido de la variable. Esto facilita la comprensión del código.

❌ Ejemplo incorrecto:
```javascript
let x = 'Pedro';
```

✅ Ejemplo correcto:
```javascript
let nombreUsuario = 'Pedro';
```

### Evita nombres de una sola letra, a menos que sea un bucle o casos muy específicos, utiliza nombres que indiquen un propósito o significado :
Nombres de una sola letra como x o y pueden ser confusos y no ofrecen información sobre el propósito de la variable. Elige nombres que reflejen el propósito o significado de la variable para que cualquiera que lea el código pueda entender su función.

❌ Ejemplo incorrecto:
```javascript
let y = 10;
```

✅ Ejemplo correcto:
```javascript
let contador = 10;
```
### Utiliza camelCase para nombrar variables :
CamelCase es una convención de escritura que capitaliza la primera letra de cada palabra, excepto la primera. Esto hace que los nombres de variables sean más legibles.

❌ Ejemplo incorrecto:
```javascript
let nombreusuario = 'Pedro';
```

✅ Ejemplo correcto:
```javascript
let nombreUsuario = 'Pedro';
```
### Prefijo para variables constantes:
Al declarar constantes, es una buena práctica utilizar un prefijo que las distinga claramente como constantes.

❌ Ejemplo incorrecto:
```javascript
const PI = 3.14;
```

✅ Ejemplo correcto:
```javascript
const PI_VALUE = 3.14;
```
### Se consistente en el uso de nombres:
Mantén la consistencia en la elección de nombres para variables relacionadas. Esto facilita la lectura y comprensión del código.

❌ Ejemplo incorrecto:
```javascript
let usuarioId = 1;
let idClient = 2;
```

✅ Ejemplo correcto:
```javascript
let usuarioId = 1;
let clienteId = 2;
```
### Evita abreviaturas confusas:
Si bien algunas abreviaturas son comunes y ampliamente comprendidas, evita abreviaturas que puedan ser confusas o poco claras.

❌ Ejemplo incorrecto:
```javascript
let calc = (a, b) => a * b;
```

✅ Ejemplo correcto:
```javascript
let calcularMultiplicacion = (a, b) => a * b;
```
### Prefijo para variables booleanas:
Al usar variables booleanas, es una buena práctica agregar un prefijo que indique claramente que es un valor booleano.

❌ Ejemplo incorrecto:
```javascript
let mayorDeEdad = true;
```

✅ Ejemplo correcto:
```javascript
let esMayorDeEdad = true;
```

## Usando variables :

### Limita el alcance de las variables:
Limita el alcance de las variables tanto como sea posible. Utiliza const y let según corresponda y evita declarar variables en un ámbito global a menos que sea necesario.

❌ Ejemplo incorrecto:
```javascript
let resultado;

function calcular() {
  resultado = 6;
}
```

✅ Ejemplo correcto:
```javascript
function calcular() {
  let resultado = 6;
  return resultado;
}
```
### Evita mutaciones inesperadas :
Trata de no modificar variables fuera de su ámbito original, especialmente en funciones o bloques de código diferentes. Esto ayuda a prevenir comportamientos inesperados y facilita el rastreo de errores.

❌ Ejemplo incorrecto:
```javascript
let total = 0;

function agregarAlTotal(valor) {
  total += valor;
}
```

✅ Ejemplo correcto:
```javascript
function calcularTotal(valor) {
  let totalLocal = 0;
  totalLocal += valor;
  return totalLocal;
}
```
### Refactoriza código :
Si encuentras que estás usando la misma lógica con diferentes variables, considera refactorizar para eliminar duplicados y hacer tu código más conciso.

❌ Ejemplo incorrecto:
```javascript
let precio1 = 10;
let precio2 = 20;
let total1 = precio1 * 2;
let total2 = precio2 * 2;
```

✅ Ejemplo correcto: 
```javascript
function calcularTotal(precio) {
  return precio * 2;
}

let precio1 = 10;
let precio2 = 20;
let total1 = calcularTotal(precio1);
let total2 = calcularTotal(precio2);
```
### Asignación desestructurada para objetos y matrices :
Utiliza la asignación desestructurada para asignar variables a propiedades de objetos o elementos de matrices. Esto hace que el código sea más legible y conciso.

❌ Ejemplo incorrecto:
```javascript
let nombre = persona.nombre;
let edad = persona.edad;

```

✅ Ejemplo correcto:
```javascript
let { nombre, edad } = persona;
```
### Manejo adecuado de errores :
Si una variable puede contener un valor nulo o indefinido, asegúrate de manejar esos casos adecuadamente para evitar errores.

❌ Ejemplo incorrecto: 
```javascript
let nombreUsuario = usuario.nombre;

```

✅ Ejemplo correcto:
```javascript
let nombreUsuario = usuario ? usuario.nombre : 'Usuario Desconocido';
```
⬆[Indice](#indice)⬆

# Funciones
## ARGUMENTOS DE UNA FUNCIÓN (IDEALMENTE 2 PARÁMETROS)

Es recomendable que en una función no se use más de 2 parámetros, en el caso de que tengas que usar más puedes usar un objeto el cual cuenta como 1 y usas más

❌ Ejemplo incorrecto:
```javascript
function prueba(nombre, apellido, edad, sexo, fechaNacimiento){
    // Funcionalidades
}

```

✅ Ejemplo correcto:
```javascript
function prueba2(persona){
    //
}
```
**o**
```javascript 
function prueba3({nombre, apellido, edad, sexo, fechaNacimiento}){
    //
}
const persona = {
    nombre: "Fran",
    apellido: "López",
    edad: 19,
    sexo: "masculino",
    fechaNacimiento: "28-05-2004"
}
```

## LAS FUNCIONES SOLO DEBEN DE HACER UNA COSA
Es recomendable que se usen una por una para hacer algo, por ejemplo si la usas para buscar algo y enviar un email, hacer 1 función para cada cosa

❌ Ejemplo incorrecto:
```javascript
function sumarYMultiplicar(numeroUno, numeroDos, operacion){
    if(operacion === 'sumar'){
        return numeroUno + numeroDos;
    } else if (operacion === 'multiplicar'){
        return numeroUno * numeroDos;
    }
}
```
✅ Ejemplo correcto:
```javascript
function sumar(numeroUno, numeroDos){
    return numeroUno+numeroDos;
}
function multiplicar(numeroUno, numeroDos){
    return numeroUno*numeroDos;
}
```

## LOS NOMBRES DE LAS FUNCIONES TIENEN QUE DECIR LO QUE HACE LA FUNCIÓN

Es recomendable que el nombre de la función haga lo que la función va a realizar para un mejor entendimiento de código

❌ Ejemplo incorrecto:
```javascript
function añadirAFecha(fecha, mes) {
    // ...
  }
  
const fecha = new Date();
añadirAFecha(fecha, 1);
```

✅ Ejemplo correcto:
```javascript
function agregarMesAFecha(fecha, mes) {
    //
}
fecha = new Date();
agregarMesAFecha(fecha, 1);
```

## LAS FUNCIONES DEBERÍAN SER ÚNICAMENTE DE UN NIVEL DE ABSTRACCIÓN

Es recomendable que cuando tienes más de un nivel de abstracción, tu función normalmente está haciendo demasiado. Separarla por varias funciones más pequeñas te ayudará a poder reutilizar el código y te facilitará el testear éstas

❌ Ejemplo incorrecto:
```javascript
function analizarMejorAlternativaJavascript(codigo) {
    const EXPRESIONES_REGULARES = [
      // ...
    ];
  
    const declaraciones = codigo.split(" ");
    const tokens = [];
    EXPRESIONES_REGULARES.forEach(EXPRESION_REGULAR => {
      declaraciones.forEach(declaracion => {
        // ...
      });
    });
  
    const ast = [];
    tokens.forEach(token => {
      // lex...
    });
  
    ast.forEach(nodo => {
      // parse...
    });
  }
```

✅ Ejemplo correcto:
```javascript
function analizarMejorAlternativaJavascript(codigo) {
    const tokens = tokenize(codigo);
    const ast = lexer(tokens);
    ast.forEach(nodo => {
      // parse...
    });
  }
  
  function tokenize(codigo) {
    const EXPRESIONES_REGULARES = [
      // ...
    ];
  
    const declaraciones = codigo.split(" ");
    const tokens = [];
    EXPRESIONES_REGULARES.forEach(EXPRESION_REGULAR => {
      declaraciones.forEach(declaracion => {
        tokens.push(/* ... */);
      });
    });
  
    return tokens;
  }
  
  function lexer(tokens) {
    const ast = [];
    tokens.forEach(token => {
      ast.push(/* ... */);
    });
  
    return ast;
  }
```
## ELIMINAR CÓDIGO DUPLICADO
Es recomendable que si has hecho una función que haga alguna cosa en concreto, no la vuelvas a hacer dentro de la función para no duplicar el código

❌ Ejemplo incorrecto:
```javascript
function mostrarListaDesarrolladores(desarrolladores) {
    desarrolladores.forEach(desarrollador => {
      const salarioEsperado = desarrollador.calcularSalarioEsperado();
      const experiencia = desarrollador.conseguirExperiencia();
      const enlaceGithub = desarrollador.conseguirEnlaceGithub();
      const datos = {
        salarioEsperado,
        experiencia,
        enlaceGithub
      };
  
      render(datos);
    });
  }
  
  function mostrarListaJefes(jefes) {
    jefes.forEach(jefe => {
      const salarioEsperado = desarrollador.calcularSalarioEsperado();
      const experiencia = desarrollador.conseguirExperiencia();
      const experienciaLaboral = jefe.conseguirProyectosMBA();
      const data = {
        salarioEsperado,
        experiencia,
        experienciaLaboral
      };
  
      render(data);
    });
  }
```
✅ Ejemplo correcto:
```javascript
function mostrarListaEmpleados(empleados) {
    empleados.forEach(empleado => {
      const salarioEsperado = empleado.calcularSalarioEsperado();
      const experiencia = empleado.conseguirExperiencia();
  
      const datos = {
        salarioEsperado,
        experiencia
      };
  
      switch (empleado.tipo) {
        case "jefe":
          datos.portafolio = empleado.conseguirProyectosMBA();
          break;
        case "desarrollador":
          datos.enlaceGithub = empleado.conseguirEnlaceGithub();
          break;
      }
  
      render(datos);
    });
  }
```
## ASIGNA OBJETOS POR DEFECTO CON OBJECT.ASSIGN
Usa los objetos que tiene javaScript por defecto para que sea más útil el código

❌ Ejemplo incorrecto:
```javascript
const configuracionMenu = {
    titulo: null,
    contenido: "Bar",
    textoBoton: null,
    cancelable: true
  };
  
  function crearMenu(config) {
    config.titulo = config.titulo || "Foo";
    config.contenido = config.contenido || "Bar";
    config.textoBoton = config.textoBoton || "Baz";
    config.cancelable =
      config.cancelable !== undefined ? config.cancelable : true;
  }
  
  crearMenu(configuracionMenu);
```
✅ Ejemplo correcto:
```javascript
const configuracionMenus = {
    titulo: "Order",
    // El usuario no incluyó la clave 'contenido'
    textoBoton: "Send",
    cancelable: true
  };
  
  function crearMenu(configuracion) {
    configuracion = Object.assign(
      {
        titulo: "Foo",
        contenido: "Bar",
        textoBoton: "Baz",
        cancelable: true
      },
      configuracion
    );
  }
  
  crearMenu(configuracionMenus);
```
## NO UTILICES BANDERAS O FLAGS
Indican que esa función hace más de una cosa, y ya que las funciones no deben de hacer más de una cosa pues es recomendable no usarlas

❌ Ejemplo incorrecto:
```javascript
function crearFichero(nombre, temporal) {
    if (temporal) {
      fs.create(`./temporal/${nombre}`);
    } else {
      fs.create(nombre);
    }
  }
```
✅ Ejemplo correcto:
```javascript
function crearFichero(nombre) {
    fs.create(nombre);
  }
  
  function crearFicheroTemporal(nombre) {
    crearFichero(`./temporal/${nombre}`);
  }
```
## EVITA LOS EFECTOS SECUNDARIOS (PARTE 1)
No compartas variables no pasadas por parámetro dentro de la función. Siempre que quieras hacer algo es recomendable pasarle la variable a través de un parámetro y ya realizar el objetivo de la función

❌ Ejemplo incorrecto:
```javascript
let nombre = 'Ryan McDermott';

  function separarEnNombreYApellido() {
    nombre = nombre.split(' ');
  }

  separarEnNombreYApellido();

  console.log(nombre);
```
✅ Ejemplo correcto:
```javascript
 function separarEnNombreYApellido(nombre) {
    return nombre.split(' ');
  }
  
  const nombre = 'Ryan McDermott';
  const nuevoNombre = separarEnNombreYApellido(nombre);
  
  console.log(nombre);  
  console.log(nuevoNombre);
```

## EVITA LOS EFECTOS SECUNDARIOS (PARTE 2)
No es bueno escribir directamente en una variable global porque puede chocar con otra librería

❌ Ejemplo incorrecto:
```javascript
Array.prototype.diff = function diff(matrizDeComparación) {
    const hash = new Set(matrizDeComparación);
    return this.filter(elemento => !hash.has(elemento));
  };
```
✅ Ejemplo correcto:
```javascript
class SuperArray extends Array {
    diff(matrizDeComparación) {
      const hash = new Set(matrizDeComparación);
      return this.filter(elemento => !hash.has(elemento));
    }
  }
```
## DA PRIORIDAD A LA PROGRAMACIÓN FUNCIONAL EN VEZ DE LA PROGRAMACIÓN IMPERATIVA
Es recomendable usar la programación funcional porque te ahorra bastante código y se puede llegar a hacer más fácil

❌ Ejemplo incorrecto:
```javascript
const datosSalidaProgramadores = [
    {
      nombre: "Uncle Bobby",
      lineasDeCodigo: 500
    },
    {
      nombre: "Suzie Q",
      lineasDeCodigo: 1500
    },
    {
      nombre: "Jimmy Gosling",
      lineasDeCodigo: 150
    },
    {
      nombre: "Gracie Hopper",
      lineasDeCodigo: 1000
    }
  ];
  
  let salidaFinal = 0;
  
  for (let i = 0; i < datosSalidaProgramadores.length; i++) {
    salidaFinal += datosSalidaProgramadores[i].lineasDeCodigo;
  }
```
✅ Ejemplo correcto:
```javascript
 const datosSalidaProgramadores = [
    {
      nombre: "Uncle Bobby",
      lineasDeCodigo: 500
    },
    {
      nombre: "Suzie Q",
      lineasDeCodigo: 1500
    },
    {
      nombre: "Jimmy Gosling",
      lineasDeCodigo: 150
    },
    {
      nombre: "Gracie Hopper",
      lineasDeCodigo: 1000
    }
  ];
  
  const salidaFinal = datosSalidaProgramadores
    .map(salida => salida.lineasDeCodigo)
    .reduce((totalLineas, lineas) => totalLineas + lineas);
```

## ENCAPSULA LOS CONDICIONALES
Es recomendable que no pongas en los condicionales excesivo código y crear funciones para realizar dicha condición

❌ Ejemplo incorrecto:
```javascript
if (fsm.state === "cogiendoDatos" && estaVacio(listaNodos)) {
      // ...
    }
```
✅ Ejemplo correcto:
```javascript
function deberiaMostrarSpinner(fsm, listaNodos) {
      return fsm.state === "cogiendoDatos" && estaVacio(listaNodos);
    }
    
    if (deberiaMostrarSpinner(fsmInstance, listNodeInstance)) {
      // ...
    }
```
## EVITA CONDICIONALES NEGATIVOS
Es recomendable que siempre en las comprobaciones usemos condicionales positivos para evitar fallos posteriormente

❌ Ejemplo incorrecto:
```javascript
function noEstaElNodoPresente(node) {
      // ...
    }
    
    if (!noEstaElNodoPresente(node)) {
      // ...
    }
```

✅ Ejemplo correcto:
```javascript
function estaElNodoPresente(node) {
      // ...
    }
    
    if (estaElNodoPresente(node)) {
      // ...
    }
```

## EVITA CONDICIONALES
Para un mejor código hay que evitar tanto if como switch, esto parece complicado pero se debería de usar polimorfismo para conseguir lo mismo en la mayoría de los casos, esto se debe porque una función solo debería de hacer 1 cosa

❌ Ejemplo incorrecto:
```javascript
class Avion {
      // ...
      obtenerAlturaDeVuelo() {
        switch (this.tipo) {
          case "777":
            return this.cogerAlturaMaxima() - this.conseguirNumeroPasajeros();
          case "Air Force One":
            return this.cogerAlturaMaxima();
          case "Cessna":
            return this.cogerAlturaMaxima() - this.getFuelExpenditure();
        }
      }
    }
```

✅ Ejemplo correcto:
```javascript
class Avion {
      // ...
    }
    
    class Boeing777 extends Avion {
      // ...
      obtenerAlturaDeVuelo() {
        return this.cogerAlturaMaxima() - this.conseguirNumeroPasajeros();
      }
    }
    
    class AirForceOne extends Avion {
      // ...
      obtenerAlturaDeVuelo() {
        return this.cogerAlturaMaxima();
      }
    }
    
    class Cessna extends Avion {
      // ...
      obtenerAlturaDeVuelo() {
        return this.cogerAlturaMaxima() - this.getFuelExpenditure();
      }
    }
```

## EVITA EL CONTROL DE TIPOS (PARTE 1)
JavaScript al ser un lenguaje no tipado no hace falta especificar el tipo de argumento que vamos a recibir, es recomendable que nos aprovechemos de eso

❌ Ejemplo incorrecto:
```javascript
function viajarATexas(vehiculo) {
      if (vehiculo instanceof Bicicleta) {
        vehiculo.pedalear(this.ubicacionActual, new Localizacion("texas"));
      } else if (vehiculo instanceof Car) {
        vehiculo.conducir(this.ubicacionActual, new Localizacion("texas"));
      }
    }
```
✅ Ejemplo correcto:
```javascript
for (let i = 0; i < lista.length; i++) {
      // ...
    }
```
## BORRA CÓDIGO INÚTIL
Código que ya no uses porque lo has renderizado o lo has modificado a mejor, borra el antiguo que tengas.

❌ Ejemplo incorrecto:
```javascript
function antiguoModuloDePeticiones(url) {
      // ...
    }
    
    function nuevoModuloDePeticiones(url) {
      // ...
    }
    
    const peticion = nuevoModuloDePeticiones;
    calculadorDeInventario("manzanas", peticion, "www.inventory-awesome.io");
```
✅ Ejemplo correcto:
```javascript
function nuevoModuloDePeticiones(url) {
      // ...
    }
    
    const peticion = nuevoModuloDePeticiones;
    calculadorDeInventario("manzanas", peticion, "www.inventory-awesome.io");
```
⬆[Indice](#indice)⬆

# Objetos y estructuras de datos

## Utiliza setters y getters
Para acceder a las propiedades del objeto mejor usar los getters y setters antes que llamar a los atributos del objeto

❌ Ejemplo incorrecto:
```javascript
let nombre;
function nuevaPersonaMal(){
    
    return nombre;
}
let persona1=new nuevaPersonaMal()
persona1.nombre="Juan"
console.log(persona1)
```

✅ Ejemplo correcto:
```javascript
function nuevaPersonaBien(){
    let apellidos="";

    function getApellidos(){
        return apellidos;
    }
    function setApellidos(apellidosRecibidos){
        apellidos=apellidosRecibidos
    }
    return {
        getApellidos: getApellidos,
        setApellidos: setApellidos
    };
}

let persona2=new nuevaPersonaBien();
persona2.setApellidos("Martínez Lara")
console.log(persona2.getApellidos())
```

## Hacer que los objetos tengan atributos/métodos privados
A un objeto se accede mediante getters y setters no mediante sus atributos

❌ Ejemplo incorrecto:
```javascript
const Persona = function (nombre){
    this.nombre=nombre;
}

Persona.prototype.cogerNombre=function cogerNombre(){
    return this.nombre;
}

const persona=new Persona("Isaac Martínez");
console.log(persona.cogerNombre())
delete persona.nombre;
console.log(persona.cogerNombre())
```

✅ Ejemplo correcto:
```javascript
function nuevaPersona(nombre) {
    return {
      cogerNombre() {
        return nombre;
      }
    };
}

const persona2 = nuevaPersona("Pablo Emilio");
console.log(persona2.cogerNombre())
delete persona2.nombre;
console.log(persona2.cogerNombre())
```
⬆[Indice](#indice)⬆

# Clases

## Prioriza las clases de ES2015/ES6 antes que las funciones planas de ES5

Es muy complicado de conseguir que un código sea entendible y fácil de leer con herencia de clases, construcción y metodos típicos de clases con las clases de ES5. Si necesitas herencia (y de seguro, que no la necesitas) entonces, dale prioridad a las clases ES2015/ES6.

❌ Ejemplo incorrecto:

```javascript
const Persona = function(nombre,apellidos,edad){
    if(!(this instanceof Persona)) {
        throw new Error("Inicializa Persona con `new`");
    }

    this.nombre = nombre;
    this.apellidos = apellidos;
    this.edad = edad;
}
const Profesor = function (grupo,asignImpartida){
    if(!(this instanceof Profesor)) {
        throw new Error("Inicializa Profesor con `new`");
    }

    this.grupo = grupo;
    this.asignImpartida = asignImpartida;

};

Persona.prototype.mover = function mover(){};
Persona.call(this,nombre);

Profesor.prototype = Object.create(Persona.prototype);
Profesor.prototype.constructor = Profesor;

Profesor.prototype.mostrarAsignaturasImpartidas = function mostrarAsignaturasImpartidas(){};
```

### Explicacion:

En este ejemplo se esta poniendo en uso el modelo de clases ES5, esto no es correcto ya que el modelo ES5 hace que el codigo sea menos entendible
 y por lo menos facil de leer.



✅ Ejemplo correcto:


``` javascript

class Persona {

    constructor(nombre,apellidos,edad){
        this.nombre = nombre;
        this.apellidos = apellidos;
        this.edad = edad;
    }

    mover(){
        /*...*/
    }
}

class Profesor extends Persona{
    constructor(grupo,asignImpartida){
        super(nombre,apellidos,edad);
        this.grupo = grupo;
        this.asignImpartida = asignImpartida;
    }

    mostrarAsignaturasImpartidas(){
        /*...*/
    }
}
```

### Explicacion

Este ejemplo, por lo contrario, si esta implementado de forma correca ya que utilizamos las clases ES6 para aportar mayor legibilidad a nuestro código.


## Utiliza el anidación de funciones

Este es un patrón útil en Javascript y verás que muchas librerías como jQuery o Lodash lo usan. Permite que tu código sea expresivo y menos verboso. Por esa razón, utiliza las funciones anidadas y date cuenta de que tan limpio estará tu código. En las funciones de tu clase, sencillamente retorna this al final de cada una y con eso, tienes todo lo necesario pra poder anidar las llamadas a las funciones.

❌ Ejemplo incorrecto:  

```javascript
class Televisor {
    constructor(nombre,marca,precio,unidades,pulgadas){
        this.nombre = nombre;
        this.marca = marca;
        this.precio = precio;
        this.unidades = unidades;
        this.pulgadas = pulgadas;
    }

    introducirNombre(nombre){
        this.nombre = nombre;
    }

    introducirMarca(marca){
        this.marca = marca;
    }

    introducirPrecio(precio){
        this.precio = precio;
    }

    introducirPulgadas(pulgadas){
        this.pulgadas = pulgadas; 
    }

    introducirPrecio(precio){
        this.precio = precio
    }

    importe(){
        return this.precio * this.unidades;
    }

    guardarTelevisor(){
        console.log(this.nombre,this.marca,this.precio,this.pulgadas)
    }
}

const televisor = new Televisor("TV Samsung MP45","Samsung",300,2,40);
televisor.introducirPrecio(400);
televisor.guardarTelevisor();
televisor.importe();

```

### Explicacion

El anterior codigo no esta bien implementado porque no utiliza la anidacion de funciones.

✅ Ejemplo correcto:

```javascript
class Televisor {
    constructor(nombre,marca,precio,unidades,pulgadas){
        this.nombre = nombre;
        this.marca = marca;
        this.precio = precio;
        this.unidades = unidades;
        this.pulgadas = pulgadas;
    }

    introducirNombre(nombre){
        this.nombre = nombre;
        return this;
    }

    introducirMarca(marca){
        this.marca = marca;
        return this;
    }

    introducirPrecio(precio){
        this.precio = precio;
        return this;
    }

    introducirPulgadas(pulgadas){
        this.pulgadas = pulgadas;
        return this; 
    }

    introducirPrecio(precio){
        this.precio = precio;
        return this;
    }

    importe(){
        return this.precio * this.unidades;
    }

    guardarTelevisor(){
        console.log(this.nombre,this.marca,this.precio,this.pulgadas);
    }
}

const televisor = new Televisor("TV Samsung MP45","Samsung",300,2,40)
.televisor.introducirPrecio(400)
.televisor.guardarTelevisor()
.televisor.importe();
```

### Explicacion

En el anterior codigo se hace uso del anidamiento de funciones, logrando una mayor expresividad a nuestro código.

## Prioriza la composición en vez de la herecia

Hay muy buenas razones para usar tanto la herecia como la composición. El problema principal es que nuestra mente siempre tiende a la herencia como primera opción, pero deberíamos de pensar qué tan bien nos encaja la composición en ese caso particular porque en muchas ocasiones es lo más acertado.

❌ Ejemplo incorrecto:


``` javascript
class Consola{
    constructor(nombre,empresa,color,anioSalida,precio){
        this.nombre = nombre;
        this.empresa = empresa;
        this.color = color;
        this.anioSalida = anioSalida;
        this.precio = precio;
     }

}

class Videojuego extends Consola{
    constructor(listaVideojuegos,formato){
        super();
        this.listaVideojuegos = listaVideojuegos;
        this.formato = formato;
    }

}

```

### Explicacion

El anterior ejemplo esta mal porque se está aplicando un uso incorrecto de la herencia. 

Cuando hablamos de que una clase presenta una relacion 'tiene un', nos esta dejando a entender que en esa clase debe actuar el fenómeno de la composición y no el de la herencia.

Por otro lado, si una clase presenta una relacion 'es un' con otra clase, nos esta diciendo que en esas clases debemos aplicar la herencia.


✅ Ejemplo correcto:

``` javascript
class Consola {
    constructor(nombre, empresa, color, anioSalida, precio) {
      this.nombre = nombre;
      this.empresa = empresa;
      this.color = color;
      this.anioSalida = anioSalida;
      this.precio = precio;
    }
  }
  
  class Videojuego {
    constructor(listaVideojuegos, formato) {
      this.listaVideojuegos = listaVideojuegos;
      this.formato = formato;
    }
  }
  
  class ProductoElectronico {
    constructor(consola, videojuego) {
      this.consola = consola;
      this.videojuego = videojuego;
    }
  
    obtenerInfo() {
      console.log(`Consola: ${this.consola.nombre} - ${this.consola.empresa}`);
      console.log(`Videojuego: ${this.videojuego.listaVideojuegos} - ${this.videojuego.formato}`);
    }
  }
  
  const miConsola = new Consola('PlayStation', 'Sony', 'Negro', 2022, 499.99);
  const miVideojuego = new Videojuego(['Juego1', 'Juego2'], 'Digital');
  
  const miProductoElectronico = new ProductoElectronico(miConsola, miVideojuego);
  
  miProductoElectronico.obtenerInfo();
  ```

  ### Explicacion

  Este ejemplo si esta bien hecho porque aplica correctamente el fenómeno de la composición.
  
⬆[Indice](#indice)⬆

# Principios SOLID

## 1. Principio de Responsabilidad Única (Single Responsibility Principle - SRP)

Este principio establece que una clase debe tener una única responsabilidad sobre una parte de la funcionalidad del software.

❌ Ejemplo incorrecto:
```javascript
class Empleado {
  calcularSalario() {
    // lógica para calcular salario
  }

  generarReporte() {
    // lógica para generar un informe
  }
}
```
### Explicación:
En este ejemplo, la clase Empleado tiene dos responsabilidades: calcular el salario y generar un informe. Esto viola el SRP, ya que la clase debería tener una única responsabilidad.

✅ Ejemplo correcto:
```javascript
class Empleado {
  calcularSalario() {
    // lógica para calcular salario
  }
}

class GeneradorDeReportes {
  generarReporte(empleado) {
    // lógica para generar un informe basado en el empleado
  }
}
```

## 2. Principio Abierto/Cerrado (Open/Closed Principle - OCP)

Este principio establece que una entidad (clase, módulo, función, etc.) debe estar abierta para extensión pero cerrada para modificación.

❌ Ejemplo incorrecto:
```javascript
class Descuento {
  aplicarDescuento(cant, tipo) {
    if (tipo === 'estudiante') {
      return cant * 0.8;
    } else if (tipo === 'veterano') {
      return cant * 0.7;
    }
  }
}
```
### Explicación:
Este código viola el OCP porque si se desea agregar un nuevo tipo de descuento, se tendría que modificar la clase Descuento.

✅ Ejemplo correcto:
```javascript
class DescuentoEstudiante {
  aplicarDescuento(cant) {
    return cant * 0.8;
  }
}

class DescuentoVeterano {
  aplicarDescuento(cant) {
    return cant * 0.7;
  }
}
```

## 3. Principio de Sustitución de Liskov (Liskov Substitution Principle - LSP)

Este principio establece que los objetos de una superclase deben poder ser reemplazados por objetos de una subclase sin afectar la integridad del programa.

❌ Ejemplo incorrecto:
```javascript
class Ave {
  volar() {
    // lógica para volar
  }
}

class Pinguino extends Ave {
  volar() {
    throw new Error("Los pingüinos no pueden volar");
  }
}
```
### Explicación:
Aunque Pinguino es una subclase de Ave, viola el LSP porque no puede reemplazar completamente a un objeto de la superclase (Ave) sin causar errores (por la excepción Error).

✅ Ejemplo correcto:
```javascript
class Ave {
  volar() {
    // lógica para volar
  }
}

class Pinguino extends Ave {
  volar() {
    return "Los pingüinos no pueden volar";
  }
}
```

### Explicación:
En este ejemplo, Pinguino aún hereda de Ave, pero redefine el método volar para indicar que los pingüinos no pueden volar. Esto respeta el principio de sustitución de Liskov.

## 4. Principio de Segregación de Interfaces (Interface Segregation Principle - ISP)

Este principio establece que un objeto no necesita implementar interfaces que no necesariamente va a utilizar.

❌ Ejemplo incorrecto:
```javascript
class NavajaSuiza {
    atornillar(){}
    cortar(){}
    pedestal(){}
}

class HerramientasDeFuego extends NavajaSuiza {
    atornillar(){}
    cortar(){}
    pedestal(){}
}
```
### Explicación:
Este ejemplo viola el principio ISP ya que tenemos una clase llamada *HerramientasDeFuego* la cual hereda funciones del padre las cuales no utilizará.

✅ Ejemplo correcto:
```javascript
class NavajaSuiza {
    cortar(){}
}

class Herramientas extends NavajaSuiza {
    atornillar(){}
}

class HerramientasDeFuego extends NavajaSuiza {
    pedestal(){}
}
```

### Explicación
En este ejemplo, ya no se violaría el principio ISP ya que hemos creado subclases añadiendo funcionalidades específicas para cada una de ellas.

## 5. Principio de Inversión de Dependencias (Dependency Inversion Module - DIP)

Este principio establece que los módulos de alto nivel no pueden depender de los de bajo nivel ni viceversa, sino que ambos tienen que depender de abstracciones.

❌ Ejemplo incorrecto:
```javascript
class LadrilloRojo {
    especificiones() {}
}

class Casa {
    constructor() {
        this.ladrillo = new LadrilloRojo();
    }
}
```
### Explicación:
Este ejemplo viola el principio DIP ya que si por ejemplo quisiesemos nosotros construir una casa con ladrillos amarillos no podríamos ya que una casa depende solo de los ladrillos rojos.

✅ Ejemplo correcto:
```javascript
class Ladrillo {
    constructor(){}
    especificaciones(){}
}

class LadrilloAzul extends Ladrillo{
    color:azul;
}

class LadrilloRojo {
    color:rojo;
}

class Casa {
    constructor(ladrillo) {
        this.ladrillo = ladrillo;
    }
}
```

### Explicación
En este ejemplo, ya no se violaría el principio DIP ya que nosotros construiremos una casa con ladrillos, pero ya no especificamos qué ladrillos utilizaremos, utilizaremos el de nuestra mayor cnveniencia,
 
## Usa consistenemente la capitalización


❌ Ejemplo incorrecto:

```javascript
const salarioMensual = 1200;
const Salarioanual = 1200 * 12;

const LIBROS = ['Los juegos del hambre','El Señor de los anillos','El codigo da vinci'];
const autor = ['Suzanne Collins','J R R Tolkien','Dan Brown'];

function aniadirProductosAlmacen(){}
function Retirarproductosalmacen(){}

class empresa {}
class Empleado {}
```

✅ Ejemplo correcto:

```javascript
const salarioMensual = 1200;
const salarioAnual = 1200 * 12;

const libros = ['Los juegos del hambre','El Señor de los anillos','El codigo da vinci'];
const autor = ['Suzanne Collins','J R R Tolkien','Dan Brown'];

function aniadirProductosAlmacen(){}
function retirarProductosAlmacen(){}

class Empresa {}
class Empleado {}
```

## Funciones que llaman y funciones que son llamadas, deberían estar cerca

Si una función llama a otra, haz que esta función que va a ser llamada esté lo más cerca posible de la función que la llama. 


❌ Ejemplo incorrecto:

```javascript
class revisarPelicula{
    constructor(empleado) {
        this.empleado = empleado;
    }

    conseguirOpinionDelEquipoGrabacion(){
        const equipGrabacion = this.conseguirEquipoGrabacion()
    }

    ejecutarRevision(){
        this.conseguirOpinionDeLosCriticos()
        this.conseguirOpinionDelDirector()
        this.conseguirOpinionDelEquipoGrabacion()
    }

    conseguirOpinionDelDirector(){
        const director = this.conseguirDirector()
    }


    conseguirDirector(){
        return db.buscar(this.empleado,"Director");
    }

    conseguirEquipoGrabacion(){
        return db.buscar(this.empleado,"Director");
    }

    conseguirOpinionDeLosCriticos(){
        const criticos = this.conseguirCriticos()
    }
}

const revision1 = new revisarPelicula(empleado);
revision.ejecutarRevision();
```

### Explicacion
La estructura del codigo no posee un orden concreto.

✅ Ejemplo correcto:

```javascript
class revisarPelicula{
    constructor(empleado) {
        this.empleado = empleado;
    }

    ejecutarRevision(){
        this.conseguirOpinionDeLosCriticos()
        this.conseguirOpinionDelDirector()
        this.conseguirOpinionDelEquipoGrabacion()
    }

    conseguirOpinionDeLosCriticos(){
        const criticos = this.conseguirCriticos()
    }

    conseguirOpinionDelDirector(){
        const director = this.conseguirDirector()
    }

    conseguirOpinionDelEquipoGrabacion(){
        const equipGrabacion = this.conseguirEquipoGrabacion()
    }

    conseguirDirector(){
        return db.buscar(this.empleado,"Director");
    }

    conseguirEquipoGrabacion(){
        return db.buscar(this.empleado,"Director");
    }
}

const revision = new revisarPelicula(empleado);
revision.ejecutarRevision();
```

### Explicacion
La estructura del codigo si posee un orden concreto

# Concurrencia

## Usar promesas, no callbacks.
Las promesas son más fáciles de entender y de leer a comparación de los callbacks, por lo que se dice que los callbacks no son limpios (provocan niveles de identación)

❌ Ejemplo incorrecto:
```javascript
import { get } from "request";
import { writeFile } from "fs";

get(
  "https://en.wikipedia.org/wiki/Robert_Cecil_Martin",
  (requestErr, respuesta) => {
    if (requestErr) {
      console.error(requestErr);
    } else {
      writeFile("article.html", respuesta.body, writeErr => {
        if (writeErr) {
          console.error(writeErr);
        } else {
          console.log("File written");
        }
      });
    }
  }
);
```

✅ Ejemplo correcto:
```javascript
import { get } from "request";
import { writeFile } from "fs";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(respuesta => {
    return writeFile("article.html", respuesta);
  })
  .catch(err => {
    console.error(err);
  });
```

## Async/Await es incluso más limpio que las Promesas
Las promesas son mas límpias que los callbacks y el async/await mas limpio que las promesas. Por lo tanto conviene utilizar async/await. Lo que hace es llamar a la funcion definida como asincrona y esta espera en el await hasta que la promesa sea resuelta


❌ Ejemplo incorrecto:
```javascript
import { get } from "request";
import { writeFile } from "fs";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(respuesta => {
    return writeFile("article.html", respuesta);
  })
  .catch(err => {
    console.error(err);
  });
```

✅ Ejemplo correcto:
```javascript
import { get } from "request-promise";
import { writeFile } from "fs-promise";

async function escribirFichero() {
  try {
    const respuesta = await get(
      "https://en.wikipedia.org/wiki/Robert_Cecil_Martin"
    );
    await writeFile("article.html", respuesta);
    
  } catch (err) {
    console.error(err);
  }
}
```
⬆[Indice](#indice)⬆

# Manejo de errores

## No ignores los errores capturados
Si ignoras los errores que suceden durante la ejecución nos costará más ver cual es el fallo. Los errores ayudan mucho a visualizar de donde viene el fallo.

❌ Ejemplo incorrecto:
```javascript
try{
    lanzaError();
}catch(error){
    console.log()
}
```


✅ Ejemplo correcto:
```javascript
try{
    lanzaError();
}catch(error){
    console.log(error)
    //Envia un codigo de error de lo que a sucedido y hace una accion
    errorProducido(error);
}
```

## No ignores las promesas rechazadas
Lo mismo que no ignoramos los errores capturados no deberíamos de ignorar las promesas que no son resueltas.

❌ Ejemplo incorrecto:
```javascript
fetch("https://jsonplaceholder.typicode.com/todos")
  .then(datos => {
    lanzarError(datos);
  })
  .catch(error => {
    console.log(error);
  });
```

✅ Ejemplo correcto:
```javascript
fetch("https://jsonplaceholder.typicode.com/todos")
  .then(datos => {
    lanzarError(datos);
  })
  .catch(error => {
    console.log(error)
    //Envia un codigo de error de lo que a sucedido y hace una accion
    errorProducido(error);
  });
```
⬆[Indice](#indice)⬆

# Formato

## Usa consistenemente la capitalización


❌ Ejemplo incorrecto:

```javascript
const salarioMensual = 1200;
const Salarioanual = 1200 * 12;

const LIBROS = ['Los juegos del hambre','El Señor de los anillos','El codigo da vinci'];
const autor = ['Suzanne Collins','J R R Tolkien','Dan Brown'];

function aniadirProductosAlmacen(){}
function Retirarproductosalmacen(){}

class empresa {}
class Empleado {}
```

✅ Ejemplo correcto:

```javascript
const salarioMensual = 1200;
const salarioAnual = 1200 * 12;

const libros = ['Los juegos del hambre','El Señor de los anillos','El codigo da vinci'];
const autor = ['Suzanne Collins','J R R Tolkien','Dan Brown'];

function aniadirProductosAlmacen(){}
function retirarProductosAlmacen(){}

class Empresa {}
class Empleado {}
```

## Funciones que llaman y funciones que son llamadas, deberían estar cerca

Si una función llama a otra, haz que esta función que va a ser llamada esté lo más cerca posible de la función que la llama. 


❌ Ejemplo incorrecto:

```javascript
class revisarPelicula{
    constructor(empleado) {
        this.empleado = empleado;
    }

    conseguirOpinionDelEquipoGrabacion(){
        const equipGrabacion = this.conseguirEquipoGrabacion()
    }

    ejecutarRevision(){
        this.conseguirOpinionDeLosCriticos()
        this.conseguirOpinionDelDirector()
        this.conseguirOpinionDelEquipoGrabacion()
    }

    conseguirOpinionDelDirector(){
        const director = this.conseguirDirector()
    }


    conseguirDirector(){
        return db.buscar(this.empleado,"Director");
    }

    conseguirEquipoGrabacion(){
        return db.buscar(this.empleado,"Director");
    }

    conseguirOpinionDeLosCriticos(){
        const criticos = this.conseguirCriticos()
    }
}

const revision1 = new revisarPelicula(empleado);
revision.ejecutarRevision();
```

### Explicacion
La estructura del codigo no posee un orden concreto.

✅ Ejemplo correcto:

```javascript
class revisarPelicula{
    constructor(empleado) {
        this.empleado = empleado;
    }

    ejecutarRevision(){
        this.conseguirOpinionDeLosCriticos()
        this.conseguirOpinionDelDirector()
        this.conseguirOpinionDelEquipoGrabacion()
    }

    conseguirOpinionDeLosCriticos(){
        const criticos = this.conseguirCriticos()
    }

    conseguirOpinionDelDirector(){
        const director = this.conseguirDirector()
    }

    conseguirOpinionDelEquipoGrabacion(){
        const equipGrabacion = this.conseguirEquipoGrabacion()
    }

    conseguirDirector(){
        return db.buscar(this.empleado,"Director");
    }

    conseguirEquipoGrabacion(){
        return db.buscar(this.empleado,"Director");
    }
}

const revision = new revisarPelicula(empleado);
revision.ejecutarRevision();
```

### Explicacion
La estructura del codigo si posee un orden concreto

⬆[Indice](#indice)⬆

# Comentarios

## Comenta únicamente la lógica de negocio que es compleja
No hace falta comentar cada línea para saber lo que hace, comenta algo genérico y mas que suficente

❌ Ejemplo incorrecto:
```javascript
function changeProductUnitsMal(cod,unidadesACambiar){
    //Si se ha encontrado el codigo en el array
    let encontrado=false;
    //La posicion que devuelve en caso de que se encuentre
    let pos=0;
    //Bucle para buscar en el array el cod
    for(let i=0;i<this.arrayProductos.length;i++){
        if(this.arrayProductos[i].id==cod){
            //Significa que lo a encontrado
            encontrado=true;
            //La posicion que a encotrado
            pos=i;
        }
    }
    //Incrementa el valor que le hemos pasado a total
    let total=this.arrayProductos[pos].units+unidadesACambiar;
    //Si se a encontrado y el total es mayor que 0
    if(encontrado&&total>=0){
        //Asigna al array las nuevas unidades
        this.arrayProductos[pos].units=total;
        //Devuelve true como que se ha podido cambiar las unidades
        return true
    }else{
        //Devuelve false como que no se han cambiado las unidades
        return false;
    }
}
```


✅ Ejemplo correcto:
```javascript
function changeProductUnitsBien(cod,unidadesACambiar){
    let encontrado=false;
    let pos=0;
    //Asigna una posicion a pos
    for(let i=0;i<this.arrayProductos.length;i++){
        if(this.arrayProductos[i].id==cod){
            encontrado=true;
            pos=i;
        }
    }
    let total=this.arrayProductos[pos].units+unidadesACambiar;
    //Si se cambian las unidades en el array devuelve true sino false
    if(encontrado&&total>=0){
        this.arrayProductos[pos].units=total;
        return true
    }else{
        return false;
    }
}
```

## No dejes codigo comentado en tu repositorio
A veces nos olvidamos de borrar el codigo con el que estabamos haciendo pruebas y lo dejamos comentado. Revisemos el codigo cuando lo terminemos y eliminemos esas partes de código inutil.

❌ Ejemplo incorrecto:
```javascript
let num1=document.getElementById("numero1")
let num2=document.getElementById("numero2")
// let num3=document.getElementById("numero3")
// let num4=document.getElementById("numero4")
// let num5=document.getElementById("numero5")
```

✅ Ejemplo correcto:
```javascript
let num3=document.getElementById("numero3")
let num4=document.getElementById("numero4")
```

## No hagas un diario de comentarios
No tengas una agenda en tu código de lo que haces cada día y lo que te queda pendiente por hacer, esto no es una agenda.

❌ Ejemplo incorrecto:
```javascript
/*
    10-11-2023: Creamos objeto Producto y añadimos sus funciones
    11-11-2023: Creamos objeto Almacen y añadimos sus funciones
*/
const producto=new Producto();
const almacen=new Almace();
```

✅ Ejemplo correcto:
```javascript
const producto1=new Producto();
const almacen1=new Almace();
```
## Evita los marcadores de secciones
Suelen ser molestos y no tienen ninguna finalidad, para eso ya estan las variables que se describen por si solas

❌ Ejemplo incorrecto:
```javascript
/////////////////////////////////////////////////////
//////////////////Añadir Producto////////////////////
/////////////////////////////////////////////////////
function addProduct(nombre,precio,unidades){
    let producto= new Product(this.idCounter,nombre,precio,unidades);
    this.arrayProductos.push(producto);
    this.idCounter++;
    return producto;
}

/////////////////////////////////////////////////////
//////////////////Modificar Producto/////////////////
/////////////////////////////////////////////////////

function modificarProducto(id,nombre,precio,unidades){
    let posProducto=this.findProduct(id)
    if(posProducto!=false){
        console.log(posProducto)
        console.log(this.arrayProductos[posProducto])
        this.arrayProductos[posProducto].name=nombre;
        this.arrayProductos[posProducto].price=precio;
        this.arrayProductos[posProducto].units=unidades;
    }
}
```
✅ Ejemplo correcto:
```javascript
function addProduct(nombre,precio,unidades){
    let producto= new Product(this.idCounter,nombre,precio,unidades);
    this.arrayProductos.push(producto);
    this.idCounter++;
    return producto;
}

function modificarProducto(id,nombre,precio,unidades){
    let posProducto=this.findProduct(id)
    if(posProducto!=false){
        console.log(posProducto)
        console.log(this.arrayProductos[posProducto])
        this.arrayProductos[posProducto].name=nombre;
        this.arrayProductos[posProducto].price=precio;
        this.arrayProductos[posProducto].units=unidades;
    }
}
```
⬆[Indice](#indice)⬆
