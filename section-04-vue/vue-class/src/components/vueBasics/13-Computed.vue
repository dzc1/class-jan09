<!-- HTML HERE -->
<template>
  <h1>Computed Props</h1>
  <div id="breakdown">
    <h2>Breakdown de las computed properties</h2>
    <div id="sin-computed-property">
      <p>
        Author has published any books?,
        <span>{{
          author.books.length > 0
            ? "Yes, author has pusblished books"
            : "No, author has not published any books yet.... "
        }}</span>
      </p>
    </div>
    <div id="con-computed-property">
      <p>
        Author has published any books? <span>{{ pulishedBookMessage }}</span>
      </p>
    </div>
    <div id="funciones-vs-computed-properties">
      <h2>Funciones normales vs computed proprs</h2>
      <p>{{ calculateBooksRegularArrowFunc() }}</p>
    </div>
  </div>
  <hr />
  <h1>Getters & Setteres</h1>
  <!-- GETTERS-AND-SETTERS -->
  <div id="getters-setters">
    <div id="example-1-guitar-player">
      <!-- sin computed properties, mediante sabaApproach -->
      <p>
        Uno de mis guitarristas preferidos es: {{ firstNameExp }}
        {{ lastNameExp }}
      </p>
      <!-- con computed properties, mediante sabaApproach
      -->
      <p>
        Uno de mis guitarristas preferidos es: {{ favGuitarPlayerComputed }}
      </p>
    </div>
    <hr />
    <div id="example-2-fav-football-player">
      <p>{{ favFootballPlayer }}</p>
      <button @click="changeFootballPlayer">Change football player</button>
    </div>

    <div id="example-3-shopping-list">
      <!-- <p>Regular function total - {{ totalRegular() }}</p> -->
      <p>Computed function total - {{ total }}</p>
      <button @click="addItem">Add Item</button>

      <div class="shopping">
        <ul v-for="(articuloDeLista, index) in items" :key="index">
          <li>{{ articuloDeLista.title }} - {{ articuloDeLista.price }}</li>
        </ul>
      </div>
      <hr />
      <h4>Expensive Item List</h4>
      <div class="shopping">
        <ul v-for="(articuloDeLista, index) in expensiveItems" :key="index">
          <li>{{ articuloDeLista.title }} - {{ articuloDeLista.price }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<!-- JS HERE -->
<script setup>
import { ref, reactive, computed } from "vue";

// definir objeto con informacion
const author = reactive({
  name: "John Doe",
  books: [
    "Vue 2 - Advanced Guide",
    "Vue 3 - Basic Guide",
    "Vue 4 - The Mystery",
  ],
});

// definir variable que contenga logica COMPUTACIONAL para verificar si el autor tiene o no algun libro dentro del array :)
const pulishedBookMessage = computed(() => {
  return author.books.length > 0
    ? "Yes, author has pusblished books"
    : "No, author has not published any books yet.... ";
});

// -----
// -----
// -----
// -----
// -----
//Cach?? computarizado vs. Funciones-normales#
//Te habr??s dado cuenta de que podemos conseguir el mismo resultado invocando una funcion:
const calculateBooksRegularArrowFunc = () =>
  author.books.length > 0
    ? "Yes, author has pusblished books"
    : "No, author has not published any books yet.... ";

//En lugar de una propiedad computada, podemos definir la misma funci??n como un m??todo. Para el resultado final, los dos enfoques son de hecho exactamente los mismos. Sin embargo, la diferencia es que las propiedades computadas se almacenan en cach?? en funci??n de sus dependencias reactivas. Una propiedad computada s??lo se reevaluar?? cuando alguna de sus dependencias reactivas haya cambiado. Esto significa que mientras author.books no haya cambiado, un acceso m??ltiple a "pulishedBookMessage" devolver?? inmediatamente el resultado calculado anteriormente sin tener que volver a ejecutar la funci??n getter.

//En comparaci??n, una invocaci??n a un m??todo siempre ejecutar?? la funci??n cada vez que se produzca una nueva renderizaci??n.

// ??Por qu?? necesitamos el almacenamiento en cach??? Imaginemos que tenemos una costosa lista de propiedades computadas, que requiere recorrer un enorme array y hacer muchos c??lculos. Luego podemos tener otras propiedades computadas que a su vez dependen de la lista. Sin la cach??, estar??amos ejecutando el getter de la lista muchas m??s veces de las necesarias. En los casos en los que no se quiera almacenar en cach??, se puede utilizar una llamada a un m??todo.

// -----
// -----
// -----
// -----
// -----

// PROPIEDADES COMPUTADAS QUE NOS AYUDAN A ESCRIBIR
// PROPIEDADES COMPUTADAS EXPANSIVAS/EXPANDIDAS!
// Las propiedades computadas son, por defecto, de tipo getter. Si intenta asignar un nuevo valor a una propiedad computada, recibir?? una advertencia en tiempo de ejecuci??n. En los raros casos en los que necesites una propiedad computada "escribible", puedes crear una proporcionando tanto un getter como un setter:
const firstNameExp = ref("Gustavo");
const lastNameExp = ref("Cerati");

const favGuitarPlayerComputed = computed({
  // Syntax
  get() {
    return `${firstNameExp.value} ${lastNameExp.value}`;
  },
  set(miNuevoValor) {
    // estoy guardando los dos valores de los datos de el nombre+apellido dentro de un array, para poder aglomerar estos dos datos dentro de el paramtero "miNuevoValor"
    [firstNameExp.value, lastNameExp.value] = miNuevoValor;
  },
});

//------
//------
//------
//------
//------
//------
// Mejores pr??cticas#
// Los getters deben estar libres de efectos secundarios#
// Es importante recordar que las funciones getter computadas s??lo deben realizar c??lculos puros y estar libres de efectos secundarios. Por ejemplo, no hagas peticiones as??ncronas ni mutes el DOM dentro de un getter computado. Piensa en una propiedad computada como una descripci??n declarativa de c??mo derivar un valor basado en otros valores - su ??nica responsabilidad debe ser calcular y devolver ese valor.

//Evitar la mutaci??n del valor computado#
// El valor devuelto de una propiedad computada es un estado derivado. Piensa en ??l como una instant??nea temporal - cada vez que el estado fuente cambia, se crea una nueva instant??nea. No tiene sentido mutar una instant??nea, por lo que un valor de retorno computado debe ser tratado como de s??lo lectura y nunca ser mutado - en su lugar, actualiza el estado fuente del que depende para desencadenar nuevos c??lculos.

// -------
// -------
// -------
// -------
// -------
// -------
// -------
// -------
// -------
// -------

const playerName = ref("Ronaldinho");
const playerLastName = ref("De Assis Moreira");

// ESTA ES PARA VERIFICAR EL ERROR DE CONCOLA QUE NOS DA "Write operation failed: computed value is readonly"
const favFootballPlayer = computed(() => {
  return `${playerName.value} ${playerLastName.value}`;
});

const changeFootballPlayer = () => {
  // PRE FIX DE WARNING DE CONSOLA -
  //favFootballPlayer.value = "Lionel Messi";
  // POST FIX DE WARNING DE CONSOLA
  newFavoriteFootballPlayer.value = "Lionel Messi";
};

const newFavoriteFootballPlayer = computed({
  // sub metodo de recibir info
  get() {
    return `${playerName.value} ${playerLastName.value}`;
  },
  // sub metodo de settear info
  set(value) {
    const newName = value.split(" ");
    playerName.value = newName[0];
    playerLastName.value = newName[1];
  },
});

// -------
// -------
// -------
// -------
// -------
// -------
// -------
// -------
// -------

const items = ref([
  { id: 1, title: "TV", price: 100 },
  { id: 2, title: "Iphone", price: 600 },
  { id: 3, title: "Computer", price: 300 },
  { id: 4, title: "Monitor", price: 700 },
  { id: 5, title: "Mercadona", price: 100 },
]);

// Usando Funcion Regular
// const totalRegular = () => {
//   console.log(
//     "Total executed normally[regularfunction], cannot be used freely inside moustacheSyntax, that means we need to call the method completely"
//   );
//   return items.value.reduce((total, curr) => (total = total + curr.price), 0);
// };

// Computed Function
const total = computed(() => {
  console.log("Total Computed via Computed Property");
  return items.value.reduce((total, curr) => (total = total + curr.price), 0);
});

// Function para a??adir un item a a la lista
const addItem = () => {
  items.value.push({ id: 6, title: "Headphones", price: 200 });
};

const expensiveItems = computed(() =>
  items.value.filter((articuloAChequear) => articuloAChequear.price > 200)
);
</script>

<!-- CSS HERE -->
<style scoped>
h1 {
  font-size: 16px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

p {
  font-size: 2rem;
}

.shopping {
  padding: 0 2rem;
  border: 1px black solid;
}

li {
  font-size: 24px;
}
</style>

<!-- {{
    author.books.length > 0
      ? "Yes, author has pusblished books"
      : "No, author has not published any books yet.... "
  }} -->

<!-- SYNTAX & RULES -->
<!-- - Siempre nos importamos nuestras computedProperties mediante la importacion de la libreria de vue.
- como usar en script? podemos asignarsela a una variable o podemos declarar el metodo dentro de nuestro script. 
- computed() -->

<!-- Computed Properties - what are they ? -->
<!-- Las propiedades computadas en Vue.js son valores reactivos que se calculan en base a los valores de otros datos reactivos en tu componente. Se utilizan para obtener nuevos datos a partir de datos reactivos existentes, y pueden ser utilizados como cualquier otro dato en tu componente.
    
Las propiedades computadas se utilizan en Vue.js con diversos fines, incluyendo:

- Derivar datos que sean m??s complejos o formateados que los datos crudos.
- Proporcionar una forma m??s conveniente y reutilizable de acceder a datos que se utilizan con frecuencia.
- Mejorar el rendimiento al almacenar en cach?? el valor computado y solo volver a calcularlo cuando sus dependencias cambien.
- A??adir funcionalidad adicional, como filtrar o ordenar, a los datos que se muestran en tu componente.

Al utilizar propiedades computadas, puedes escribir c??digo m??s conciso, mantenible y eficiente, mientras sigues disfrutando de la reactividad y la simplicidad que brinda Vue.js.

ANALOGIA:
Las propiedades computadas en Vue.js se pueden comparar con un c??lculo que realiza una calculadora. Al igual que una calculadora, las propiedades computadas toman valores existentes (los n??meros que ingresas) y realizan un c??lculo con ellos (por ejemplo, la suma o el producto) para producir un nuevo valor (el resultado). En el caso de Vue.js, los valores existentes son los datos reactivos en tu componente, y la propiedad computada es el c??lculo que se realiza con ellos.

Adem??s, al igual que una calculadora, las propiedades computadas en Vue.js solo se recalculan cuando sus dependencias cambian. De esta manera, pueden mejorar el rendimiento al evitar recalculaciones innecesarias. 

EJEMPLO: 
Imagina que est??s mostrando una lista de precios pero que el usuario puede meter un c??digo de descuento. Puedes hacer una propiedad computada que sea el descuento y otra que sea el precio.
Cuando el descuento cambie, cambiar??n el resto de precios y el usuario lo ver?? en pantalla inmediatamente. 


IMPORTANTE
Cuando no usar propiedades computadas
Si su propiedad computada no contiene ninguna dependencia reactiva (una forma elegante de decir, si alg??n dato depende de esta propiedad computada para reflejarse en la UI), no tiene sentido que se compute.
-->
