<!-- ¿Qué son los events?
Son, literalmente, eventos. Algo que sucede y provoca una reacción. 

¿Para qué sirven?
Para que tú, como programador, reacciones a algo que ha sucedido. 

Un ejemplo. 
Que el usuario haga click en un elemento del HTML y como consecuencia le aparezca un mensaje.  -->

<!-- HTML HERE -->

<!-- Una situación muy común cuando se monta una aplicación es que querremos ser capaces de ejecutar JavaScript después de un evento en el DOM (click, submit, etc.). -->
<!-- Hay dos tipos de manejadores de eventos (handlers), los inline y pasarlos como funcines :) . -->

<!-- SYNTAX  -->

<!-- directivo
v-on

shorthand directivo 
@ -->

<!-- V-ON === trabajar con eventos en VUE  -->

<template>
  <section>
    <!-- Ejemlo de evento click con logica directa dentro del template! -->
    <div class="event-buttons">
      <button v-on:click="countInLine++">
        Suma +1 - usando directivo completo
      </button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-buttons">
      <button v-on:click="countMinusOne">
        Resta -1 - usando directivo completo pero apuntando a una funcion en vez
        de tener logica en linea
      </button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-buttons">
      <button @click="countInLine++">Suma +1 - usando el shortHand</button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-buttons">
      <button @click="countMinusOne">
        Resta -1 - usando el shortHand + apuntando a una funcion en vez de tener
        logica en linea
      </button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-buttons">
      <button @dblclick="countOneDouble">
        Suma +1 - usando el shortHand + dblclick
      </button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-buttons">
      <button @mouseenter="countOneDouble">
        Suma +1 - usando el shortHand + mouseenter event
      </button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-buttons">
      <button @mouseleave="countOneDouble">
        Suma +1 - usando el shortHand + mouseleave event
      </button>
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputOne">Using @click event on an input</label>
      <input type="text" id="inputone" @click="countPlusOne" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputTwo">Using @input event on an input</label>
      <input type="text" id="inputTwo" @input="countPlusOne" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputThree">Using @keydown event on an input</label>
      <input type="text" id="inputThree" @keydown="countPlusOne" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputFour">Using @keyUp event on an input</label>
      <input type="text" id="inputFour" @keyup="countPlusOne" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputFive">Using @keypress event on an input</label>
      <input type="text" id="inputFive" @keypress.space="countInLine++" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputSix">Using @keydown.tab event on an input</label>
      <input type="text" id="inputFive" @keydown.tab="countInLine++" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="event-inputs">
      <label for="inputSix">Using @keydown.delete event on an input</label>
      <input type="text" id="inputFive" @keydown.delete="countInLine++" />
      <p>La Cuenta actual es: {{ countInLine }}</p>
    </div>

    <div class="function-with-events">
      <!-- INSERT CONTEXT LATER -->
      <!-- Ejemplo de un evento que asociamos una funcion chicos que acepte un paramtero que nos diga hola dentro de una alerta, aca refrescamos un poco de js :) -->
      <button @click="holaClase('Hola chicos')">Dile hola a la consola</button>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="function-with-events">
      <button @click="holaClaseTwo">
        Escribe tu nombre y el navegador te dira hola :)
      </button>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <!-- Formulario con @submit dentro opening del form element -->
    <div class="forms">
      <h1>Form one</h1>
      <form @submit.prevent="handleSubmit">
        <div class="form-labels">
          <label for="name">Name:</label>
          <input type="text" id="name" />
        </div>
        <div class="form-labels">
          <label for="lastName">Last Name:</label>
          <input type="text" id="lastName" />
        </div>
        <input type="submit" value="Submit" />
      </form>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <!-- Formulario con @submit fuera opening del form element -->
    <div class="forms">
      <h1>Form two</h1>
      <form @submit="handleSubmit">
        <div class="form-labels">
          <label for="name">Name:</label>
          <input type="text" id="name" />
        </div>
        <div class="form-labels">
          <label for="lastName">Last Name:</label>
          <input type="text" id="lastName" />
        </div>
        <input type="submit" @click.prevent value="Submit" />
      </form>
    </div>
    <!-- INSERT CONTEXT LATER -->
    <div class="class-example">
      <label for="multiple-visa">Do you have multplie citizenship?</label>
      <div class="checkbox"></div>
      <input
        type="checkbox"
        id="multiple-visa"
        @click="showHideExtraVisaElements"
      />

      <div v-if="showExtraVisa">
        <label for="visa">Enter Citizenship</label>
        <input type="text" id="visa" />
      </div>
    </div>
  </section>

  <!-- CUSTOM EVENTS -->
  <!-- Aunque es muy útil tener eventos nativos de Vue.js incorporados para hacer frente a los sucesos del día a día, a menudo se da el caso de que tenemos que hacer frente a cosas personalizadas que suceden fuera del ámbito de estos. Cuando esto sucede, podemos utilizar los custom events (eventos personalizados) como una forma de que nuestros componentes se comuniquen entre sí. Los eventos personalizados permiten que un componente hijo envíe un evento a un componente padre y que éste actúe sobre el evento. -->
  <EventEmit
    @sayHelloCl="miFuncion"
    @sayHelloDbl="miFuncion"
    @sayHelloMouse="miFuncion"
    @emitInsideFunction="miFuncion"
    @emitInsideFunctionThatHoldsInfo="viewCountInfoFromChildComp"
  />
  <h1>NEW VALUE IS {{ newValueFromParent }}</h1>
</template>

<!-- JS HERE -->
<script setup>
import { ref, reactive } from "vue";
import EventEmit from "./9-EventEmits.vue";
let changeNumber = ref(2);

let newValueFromParent = ref(0);

const miFuncion = () => {
  alert("Hello");
};
const viewCountInfoFromChildComp = (informacionDeMiEmit) => {
  // console.log(informacionDeMiEmit);
  let a = informacionDeMiEmit;
  let totalValue = changeNumber.value * a;
  console.log(totalValue);
  newValueFromParent.value += totalValue;
};

// const reactiveExampleVar = reactive({
//     name: "Diego",
//     age: 31
// })

const countInLine = ref(0);
const countMinusOne = () => {
  console.log(countInLine.value);
  countInLine.value--;
  //console.log(reactiveExampleVar.name);
  //console.log(reactiveExampleVar.age);
};
const countPlusOne = () => {
  console.log(countInLine.value);
  countInLine.value++;
  //console.log(reactiveExampleVar.name);
  //console.log(reactiveExampleVar.age);
};
// AL SER UNA FUNCION ASOCIADA A UN EVENTO TENEMOS ACCESO A LOS PARAMETROS DEL EVENTO -  SIEMPRE Y CUANDO, DEFINAMOS UN PARAMTERO INICIAL DENTRO DE LOS () DE LA FUNCION, QUE EN ESTE CASO SE LLAMA "countOneDouble".

// MIREMOS LA CONSOLA - PORQUE ESTAMOS REGISTRANDO EL PARAMETRO "EVENTO" DENTRO DE LA FUNCION linea 101
const countOneDouble = (elEventoDePablo) => {
  console.log(elEventoDePablo); // ESTOOOOOOOOOOO
  // console.log("Hey, I have been double clicked!");
  // console.log("Hey I have been mouse-entered");
  console.log("Hey I have been mouse-left");
  countInLine.value++;
};

// CLASS VISA EXAMPLE
const showExtraVisa = ref(false);
const showHideExtraVisaElements = () => {
  //showExtraVisa.value = true;
  console.log((showExtraVisa.value = !showExtraVisa.value));
};

// FUNCION ++ PARAMETROS
const holaClase = (stringDeRecibida) => {
  alert(stringDeRecibida);
};
// FUNCION ++ PARAMETROS ++ ALERTAS
const holaClaseTwo = (verParametrosEventoCLick) => {
  console.log(verParametrosEventoCLick);
  const userName = prompt("Escribe tu nombre:");
  alert(`Hola, ${userName}`);

  setTimeout(() => console.log(`Hola, ${userName}`), 2000);
};
// FUNCION DE FORM - 1
const handleSubmit = (evento) => {
  //evento.preventDefault();
  console.log("form enviado");
};

// CUSTOM EVENTS
// UUSING EMITS ON CHILD COMPONENT
// CHILD COMPONENT ON THIS EXAMPLE === EventEmit

// const miFuncion = () => {
//   alert("Hello");
// };
</script>

<!-- CSS HERE -->
<style>
.forms {
  padding: 1rem 0;
}
p {
  font-size: 2em;
}
button {
  margin: 1 2rem;
  height: 64px;
  background: rgb(69, 69, 241, 0.8);
  border: none;
  color: white;
  font-size: 1.5em;
}

.event-inputs,
.event-buttons,
.event-mouse,
.form-labels,
.script-dependant-logic,
.function-with-events {
  display: flex;
  flex-direction: column;
  height: 100%;
  padding: 2rem 0;
}
.event-inputs label {
  margin: 0 0 1rem 0;
}

label,
input {
  font-size: 2em;
}

.form-labels button {
  width: 100%;
}
/* .class-example .checkbox{
    width: 100px;
    height: 100px;
    background: white;;
}
input[type=checkbox]{
    visibility: hidden;

} */
</style>
