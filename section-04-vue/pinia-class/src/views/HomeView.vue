<script setup>
import { ref, computed } from "vue";
import { useCounterStore } from "../stores/counter";

// LOGIC FROM THIS COMPONENT
const countOnHomeView = ref(0);
const incrementOnHomeView = () => countOnHomeView.value++;
const decrementOnHomeView = () => countOnHomeView.value--;

// LOGIC FROM STORE

// approach #0001 - recibiendo toda la info de la tienda dentro de 1 var
const counterLogic = useCounterStore();
console.log(counterLogic);
// approach #0002 -
const nameFromCounter = useCounterStore().myName;
console.log(nameFromCounter);
let myCoolName = nameFromCounter;
myCoolName += ` es un gran programador`;
console.log(myCoolName);

// approach #0003 - same way just diff info/dataSrc
const doubleCount = useCounterStore().doubleCount;
</script>

<template>
  <div id="data-coming-from-this-component">
    <h4>Counter using logic from this component</h4>
    <p>{{ countOnHomeView }}</p>
    <div>
      <button @click="decrementOnHomeView">Decrease</button>
      <button @click="incrementOnHomeView">Increase</button>
    </div>
  </div>
  <hr />
  <div id="data-coming-from-store">
    <div id="store-data-passed-as-method-within-template">
      <h6>The double count is currently at - {{ doubleCount }}</h6>
      <h4>Counter from store</h4>
      <!-- Manera 1 - apuntando directo a la variable dentro del import en el template -->
      <p>{{ useCounterStore().count }}</p>
      <p>{{ useCounterStore().myName }}</p>
      <div>
        <button @click="useCounterStore().decrement">Decrease</button>
        <button @click="useCounterStore().increment">Increase</button>
      </div>
    </div>
    <div id="store-data-passed-inside-variable-in-the-script-tag">
      <h4>
        Counter from store - storing the useCounterStore inside a variable
      </h4>
      <!-- Manera 1 - apuntando directo a la variable dentro del import en el template -->
      <p>{{ counterLogic.count }}</p>
      <p>{{ counterLogic.myName }}</p>
      <div>
        <button @click="counterLogic.decrement">Decrease</button>
        <button @click="counterLogic.increment">Increase</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
#data-coming-from-this-component,
#data-coming-from-store {
  padding: 2rem;
  border: 1px solid green;
  margin: 2rem 0;
}
</style>

<!-- Que son las tiendas-de-estado-de-datos === state management library? 
Una biblioteca de gesti??n de estado en el desarrollo front-end es una biblioteca de software dise??ada para ayudar a gestionar el estado de una aplicaci??n de manera consistente, predecible y organizada. Proporciona un lugar centralizado para almacenar los datos que impulsan la aplicaci??n, que luego se utiliza para impulsar el comportamiento y renderizar la UI. 

La biblioteca de gesti??n de estado proporciona mecanismos para actualizar el estado, responder a los cambios en el estado y hacerlo disponible en diferentes partes de la aplicaci??n de manera eficiente y conveniente. Esto ayuda a garantizar que la aplicaci??n se comporte de manera consistente, incluso a medida que crece en complejidad, y que los datos se compartan y manipulen de manera predecible y organizada.


Que es pinia ? 
Pinia es una biblioteca de gesti??n de estado para Vue.js. Es un enfoque alternativo a la gesti??n de estado que se integra directamente con Vue.js y brinda una soluci??n para la gesti??n de estado en aplicaciones Vue.js de manera simple, organizada y eficiente. Pinia proporciona una tienda centralizada para almacenar los datos que impulsan la aplicaci??n, que luego se utiliza para impulsar el comportamiento y renderizar la UI.

Porque son efectivas ?  
Las tiendas de Pinia son efectivas en Vue.js porque permiten a los desarrolladores administrar interacciones y cambios complejos de estado de una manera centralizada y previsible. Al usar las tiendas de Pinia, los desarrolladores pueden evitar problemas como mutaciones de estado, actualizaciones m??ltiples de componentes y comunicaci??n de componente a componente.

Ejemplo: 
Un ejemplo de la vida real de c??mo las tiendas de Pinia pueden ayudar en el proceso de desarrollo en Vue.js es creando una tienda para administrar el estado de autenticaci??n de usuario. Esta tienda puede contener informaci??n sobre el usuario actual y su estado de autenticaci??n, y se puede usar para actualizar la UI y administrar acciones relacionadas con la autenticaci??n en m??ltiples componentes de la aplicaci??n.

Analogia: 
Una tienda de Pinia en Vue.js se puede pensar como un "cerebro" centralizado para administrar el estado de una aplicaci??n de Vue.js. Al igual que un cerebro humano recibe y procesa informaci??n de los sentidos y coordina acciones en todo el cuerpo, una tienda de Pinia recibe actualizaciones de los componentes y administra el estado de la aplicaci??n de una manera coordinada y previsible.

PORQUE NOS BENEFICIAN LAS TIENDAS EN VUE.JS ?
Se necesita un sistema de tienda centralizado cuando se desarrolla en Vue.js por varias razones:

- Mantenibilidad: Tener una tienda centralizada facilita el mantenimiento y la depuraci??n del estado de una aplicaci??n de Vue.js, ya que todos los cambios de estado e interacciones se pueden rastrear en un solo lugar.

- Predictibilidad: Las tiendas centralizadas hacen que la gesti??n de estado sea m??s previsible permitiendo a los desarrolladores administrar interacciones y cambios de estado de una manera estructurada y bien definida.

- Reutilizaci??n: Las tiendas centralizadas se pueden reutilizar en m??ltiples componentes en una aplicaci??n de Vue.js, reduciendo la cantidad de c??digo redundante y haciendo m??s f??cil la gesti??n de interacciones complejas de estado.

- Mejora de desempe??o: Las tiendas centralizadas pueden mejorar el desempe??o de una aplicaci??n de Vue.js reduciendo el n??mero de renderizados y actualizaciones que deben realizarse. Al usar una tienda centralizada, los componentes se pueden actualizar de una manera m??s eficiente, reduciendo la cantidad de trabajo que el navegador debe realizar.

- Mejor escalabilidad: Las tiendas centralizadas facilitan la escalabilidad de una aplicaci??n de Vue.js permitiendo a los desarrolladores administrar el estado de sus aplicaciones de una manera modular y organizada. Esto facilita la adici??n de nuevas caracter??sticas, componentes y funcionalidad a una aplicaci??n a medida que crece.

En general, un sistema de tienda centralizado es un componente clave del desarrollo web moderno y brinda importantes beneficuentos para los desarrolladores de Vue.js, incluyendo mejoras en mantenibilidad, predictibilidad, reutilizaci??n, desempe??o y escalabilidad.


DIFF ENTRE PROPS-EMITS y STATE MANAGEMENT LIBRARIES 


Props y $emit son mecanismos b??sicos de comunicaci??n en Vue.js que permiten que los componentes padres se comuniquen con los componentes hijos y viceversa. Por otro lado, Pinia es una biblioteca de gesti??n de estado para Vue.js que proporciona un sistema de tienda centralizado para gestionar el estado de una aplicaci??n. Aqu?? est??n las principales diferencias entre el uso de props y $emit y el uso de Pinia:

- Centralizaci??n: Pinia proporciona una tienda centralizada para gestionar el estado de una aplicaci??n, mientras que props y $emit se utilizan para comunicarse entre componentes individuales. Esto significa que con Pinia, tiene una ??nica fuente de verdad para el estado de su aplicaci??n, mientras que con props y $emit, debe gestionar los cambios y las interacciones de estado en una base componente por componente.

- Escalabilidad: Pinia hace que sea m??s f??cil escalar una aplicaci??n a medida que crece, ya que puede gestionar las interacciones y los cambios de estado de una manera bien definida y centralizada. Por otro lado, el uso de props y $emit puede volverse m??s dif??cil de gestionar a medida que una aplicaci??n crece y se vuelve m??s compleja.

- Depuraci??n: Pinia hace que sea m??s f??cil depurar una aplicaci??n, ya que puede realizar un seguimiento de todos los cambios y las interacciones de estado en un solo lugar. Por otro lado, al usar props y $emit, es posible que tenga que buscar los cambios y las interacciones de estado en m??ltiples componentes, lo que dificulta la depuraci??n.

- Reutilizaci??n: Pinia hace que sea m??s f??cil reutilizar el estado en m??ltiples componentes, ya que el estado puede ser gestionado de manera centralizada. Por otro lado, al usar props y $emit, debe gestionar los cambios y las interacciones de estado en una base componente por componente, lo que dificulta la reutilizaci??n.

- Rendimiento: Pinia puede mejorar el rendimiento de una aplicaci??n reduciendo el n??mero de re-representaciones y actualizaciones que deben realizarse. Por otro lado, el uso de props y $emit puede llevar a un aumento en las re-representaciones y actualizaciones, lo que puede afectar negativamente el rendimiento.

En conclusi??n, Pinia proporciona un sistema de tienda centralizado para gestionar el estado de una aplicaci??n, mientras que props y $emit se utilizan para comunicarse entre componentes individuales. Pinia ofrece varios beneficuentos sobre props y $emit, incluyendo mejoras en la mantenibilidad, la previsibilidad, la reutilizaci??n, el rendimiento y la escalabilidad. -->
