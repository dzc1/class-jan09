<template>
  <header class="center">
    <h1>Slots</h1>
    <br />
    <h2>Is for sloths</h2>
    <br />
    <img
      class="sloth"
      src="https://www.rainforest-alliance.org/wp-content/uploads/2021/06/three-toed-sloth-teaser-1.jpg.optimal.jpg"
      alt="sloth"
    />
    <br />
  </header>
  <br />
  <!-- Aquí haremos la llamada como se ha hecho toda la vida de Dios, simplemente ponemos un tag y hacemos que un style que está en otro lado le afecte. No es lo mejor que se puede hacer, pero se suele hacer. -->
  <button class="fancy-btn center">
    Soy un simple boton - sin depender de un slot
  </button>

  <br />
  <!-- Aquí insertaremos el slot. Básicamente lo que escribamos dentro del tag (en este caso lo que hemos escrito es "Soy un slot/h") se pondrá donde hayamos puesto <slot/> dentro del componente. -->
  <FancyButton class="center">
    Contenido inyectado a traves de un slot como componente
  </FancyButton>

  <!-- Aquí otro ejemplo para que se vea más claro -->
  <slothers> Los perezosos molan </slothers>

  <!-- Podemos inyectar HTML a los slots, no solo texto. Fíjate como el flex cambia su comportamiento en función a si lo introducido es texto plano o un elemento <p> -->
  <slothers>
    <p>Los perezosos molan</p>
  </slothers>

  <!-- Por último, podemos añadir clases de estilo sobre los slots y sobre el componente. Tal y como lo haríamos normalmente. -->
  <slothers>
    <p class="center">Los perezosos molan</p>
  </slothers>
</template>

<script setup>
import FancyButton from "./FancyButton.vue";
import slothers from "./Slothers.vue";

//El slot es un "hueco". Este hueco se rellena con lo que hay entre los tags. Como vemos en la línea 9. Ese Click me! busca dentro del componente el tag <slot/> y se inserta donde quiera que esté dicho tag.
</script>

<style>
.center {
  text-align: center;
}
.sloth {
  width: 200px;
  height: 200px;
}
</style>
