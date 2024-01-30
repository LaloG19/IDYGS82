<script setup lang="ts">
  import { ref, onMounted, watch } from 'vue';
  import type { Ref } from 'vue';

  const name: Ref<string> = ref('');
  const surname: Ref<string> = ref('');
  const age: Ref<number> = ref(0);
  const Generos: Ref<string[]> = ref(['Masculino', 'Femenino', 'Otro']);
  const Genero: Ref<string> = ref('');
  const generoMode: Ref<boolean> = ref(true);

  const generoChange = () => {
    generoMode.value = !generoMode.value;
    Genero.value = '';
  }
  const Envio = () => {
    if (!valName()) {
      alert("Nombre no valido");
      return;
    }else if (!valSurname()) {
      alert("Apellido no valido");
      return;
    }else if (!valAge()) {
      alert("Edad no valida");
      return;
    }else if (Genero.value === '') {
      alert("Genero no valido");
      return;
    }else{
      console.log(" \n [Nombre]: " + name.value, " \n [Apellido]: " + surname.value, "\n [Edad]: " + age.value, "\n [Genero]: " + Genero.value);
      alert("Nuevo registro, bienvenido: " + name.value + " " + surname.value);
      name.value = '';
      surname.value = '';
      age.value = 0;
      Genero.value = '';
    }
  }
  const valName = () =>{
    if (name.value.length >= 5 && name.value.length <= 18) {
      return true;
    } else {
      return false;
    }
  
  }
  const valSurname = () =>{
    if (surname.value != '' && surname.value.length >= 0 && surname.value != name.value) {
      return true;
    } else {
      return false;
    }
  }
  const valAge = () =>{
    if (age.value >= 0 && age.value <= 60) {
      return true;
    } else {
      return false;
    }
  }
  watch(Genero, (newValue) => {
    if (newValue === 'Otro') {
      generoMode.value = false;
      Genero.value = '';
    }
  })
</script>

<template>
  <div class="restricciones">
    <p> Restricciones: </p>
    <ul>
      <li>
        El nombre debe tener entre 5 y 18 caracteres.
      </li>
      <li>
        El apellido no puede estar vacio, ni ser igual al nombre.
      </li>
      <li>
        La edad debe estar entre 0 y 60 años.
      </li>
      <li>
        El genero debe ser Masculino, Femenino u Otro.
      </li>
    </ul>
  </div>
  <fieldset class="formulario">
    <label for="Nombre"> Nombre: </label>
    <input type="text" id="Nombre" placeholder="Nombre" v-model="name">
    <label for="Apellido"> Apellido: </label>
    <input type="text" id="Apellido" placeholder="Apellido" v-model="surname">
    <label for="Edad"> Edad: </label>
    <input type="number" id="Edad" placeholder="Edad" min="0" max="60" v-model="age">
    <label for="Genero"> Genero: </label>

    <select name="Genero" id="Genero" v-if="generoMode" v-model="Genero">
      <option v-for="(items, index) in Generos" :key="index" > {{  items }}</option>
    </select>

    <input type="text" id="Genero" v-else="!generoMode" v-model="Genero">
    <button @click="generoChange" v-if="!generoMode"> Cancelar </button>

    <button @click="Envio"> Enviar </button>
  </fieldset>

</template>

<style scoped>

</style>