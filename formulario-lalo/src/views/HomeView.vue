  <!--     <label for="Nombre"> Nombre: </label>
      <input type="text" id="Nombre" placeholder="Nombre" v-model="name">
      <label for="Apellido"> Apellido: </label>
      <input type="text" id="Apellido" placeholder="Apellido" v-model="surname">
      <label for="Edad"> Edad: </label>
      <input type="number" id="Edad" placeholder="Edad" min="0" max="60" v-model="age">
      <label for="Genero"> Genero: </label> -->

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
  <div class="contenedorPadre">

    <h1> Formulario - Lalo </h1>

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

      <div class="textInputWrapper">
        <input placeholder="Nombre" type="text" class="textInput">
      </div>
      <div class="textInputWrapper">
        <input placeholder="Apellidos" type="text" class="textInput">
      </div>
      <div class="textInputWrapper">
        <input placeholder="Edad" type="number" class="textInput">
      </div>
      <select name="Genero" id="Genero" v-if="generoMode" v-model="Genero" class="selectGender">
        <option v-for="(items, index) in Generos" :key="index" > {{  items }}</option>
      </select>

      <div class="textInputWrapper">
        <input type="text" id="Genero" v-if="!generoMode" v-model="Genero" placeholder="Genero" class="textInput">
      </div>

      <button class="btn cube cube-hover minibutton" type="button" @click="generoChange" v-if="!generoMode"> <!-- BTVolver -->
        <div class="bg-top">
          <div class="bg-inner"></div>
        </div>
        <div class="bg-right">
          <div class="bg-inner"></div>
        </div>
        <div class="bg">
          <div class="bg-inner"></div>
        </div>
        <div class="text">Volver</div>
      </button>

      <button class="btn cube cube-hover" type="button" @click="Envio">     <!-- BTEnviar -->
        <div class="bg-top">
          <div class="bg-inner"></div>
        </div>
        <div class="bg-right">
          <div class="bg-inner"></div>
        </div>
        <div class="bg">
          <div class="bg-inner"></div>
        </div>
        <div class="text"> Envíar </div>
      </button>

    </fieldset>

    
    <div class="rating">
      <form class="rating-form">
        <label for="super-happy" class="lb">
          <input type="radio" name="rating" class="super-happy" id="super-happy" value="super-happy">
          <svg class="svg" viewBox="0 0 24 24"><path d="M12,17.5C14.33,17.5 16.3,16.04 17.11,14H6.89C7.69,16.04 9.67,17.5 12,17.5M8.5,11A1.5,1.5 0 0,0 10,9.5A1.5,1.5 0 0,0 8.5,8A1.5,1.5 0 0,0 7,9.5A1.5,1.5 0 0,0 8.5,11M15.5,11A1.5,1.5 0 0,0 17,9.5A1.5,1.5 0 0,0 15.5,8A1.5,1.5 0 0,0 14,9.5A1.5,1.5 0 0,0 15.5,11M12,20A8,8 0 0,1 4,12A8,8 0 0,1 12,4A8,8 0 0,1 20,12A8,8 0 0,1 12,20M12,2C6.47,2 2,6.5 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2Z"></path></svg>
        </label>
        <label for="neutral" class="lb">
          <input type="radio" name="rating" class="neutral" id="neutral" value="neutral">
          <svg class="svg" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" width="100%" height="100%" viewBox="0 0 24 24"><path d="M8.5,11A1.5,1.5 0 0,1 7,9.5A1.5,1.5 0 0,1 8.5,8A1.5,1.5 0 0,1 10,9.5A1.5,1.5 0 0,1 8.5,11M15.5,11A1.5,1.5 0 0,1 14,9.5A1.5,1.5 0 0,1 15.5,8A1.5,1.5 0 0,1 17,9.5A1.5,1.5 0 0,1 15.5,11M12,20A8,8 0 0,0 20,12A8,8 0 0,0 12,4A8,8 0 0,0 4,12A8,8 0 0,0 12,20M12,2A10,10 0 0,1 22,12A10,10 0 0,1 12,22C6.47,22 2,17.5 2,12A10,10 0 0,1 12,2M9,14H15A1,1 0 0,1 16,15A1,1 0 0,1 15,16H9A1,1 0 0,1 8,15A1,1 0 0,1 9,14Z"></path></svg>
        </label>
        <label for="super-sad" class="lb">
          <input type="radio" name="rating" class="super-sad" id="super-sad" value="super-sad">
          <svg class="svg" viewBox="0 0 24 24"><path d="M12,2C6.47,2 2,6.47 2,12C2,17.53 6.47,22 12,22A10,10 0 0,0 22,12C22,6.47 17.5,2 12,2M12,20A8,8 0 0,1 4,12A8,8 0 0,1 12,4A8,8 0 0,1 20,12A8,8 0 0,1 12,20M16.18,7.76L15.12,8.82L14.06,7.76L13,8.82L14.06,9.88L13,10.94L14.06,12L15.12,10.94L16.18,12L17.24,10.94L16.18,9.88L17.24,8.82L16.18,7.76M7.82,12L8.88,10.94L9.94,12L11,10.94L9.94,9.88L11,8.82L9.94,7.76L8.88,8.82L7.82,7.76L6.76,8.82L7.82,9.88L6.76,10.94L7.82,12M12,14C9.67,14 7.69,15.46 6.89,17.5H17.11C16.31,15.46 14.33,14 12,14Z"></path></svg>
        </label>
      </form>
    </div>


  </div>
</template>

<style scoped>
@import '../assets/boton.css';

h1{
  text-align: center;
  width: 100%;
  display: inline;
}
.restricciones {
  text-align: start;
  width: 100%;
  margin-top: 1rem;
  margin-bottom: 1rem;
}
.formulario {
  width: 100%;
  margin: auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.minibutton{
  margin-top: 1rem;
  margin-bottom: 2rem;
}

.selectGender{
  width: 100%;
  color: rgba(255, 255, 255, 0.582);
  background-color: rgba(255, 255, 255, 0.082);
  height: 36px;
  border: none;
  border-radius: 5px 5px 0px 0px;
  margin-top: 0.75rem;
}
option{
  color: rgba(255, 255, 255, 0.582);
  background-color: rgba(255, 255, 255, 0.082);
  height: 36px;
}
</style>