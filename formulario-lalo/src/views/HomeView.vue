<script setup lang="ts">
  import { ref, onMounted, watch } from 'vue';
  import type { Ref } from 'vue';

  const name: Ref<string> = ref('');
  const surname: Ref<string> = ref('');
  const age: Ref<number> = ref(100);
  const Generos: Ref<string[]> = ref(['Masculino', 'Femenino', 'Otro']);
  const Genero: Ref<string> = ref('');
  const generoMode: Ref<boolean> = ref(true);

  const errores: Ref<number> = ref(0);

  const generoChange = () => {
    generoMode.value = !generoMode.value;
    Genero.value = '';
  }
  const Envio = () => {
    if (!valName()) {
      errores.value++;
      alert("Nombre no valido. \n Errores: " + errores.value);
      console.log(name.value.length);
      return;
    }else if (!valSurname()) {
      errores.value++;
      alert("Apellido no valido. \n Errores: " + errores.value);
      console.log(surname.value.length);
      return;
    }else if (!valAge()) {
      errores.value++;
      alert("Edad no valida. \n Errores: " + errores.value);
      console.log(age.value);
      return;
    }else if (Genero.value === '' || Genero.value === ' ' || Genero.value === null || Genero.value === undefined) {
      errores.value++;
      alert("Genero no valido. \n Errores: " + errores.value);
      console.log(Genero.value);
      return;
    }else{
      if (errores.value > 0) {
        errores.value = 0;
      }

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
    if (age.value >= 0 && age.value <= 60 && age.value != null && age.value != undefined) {
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
        <input placeholder="Nombre" type="text" class="textInput" v-model="name">
      </div>
      <div class="textInputWrapper">
        <input placeholder="Apellidos" type="text" class="textInput" v-model="surname">
      </div>
      <div class="textInputWrapper">
        <input placeholder="Edad" type="number" class="textInput" v-model="age">
      </div>
      <select name="Genero" id="Genero" v-if="generoMode" v-model="Genero" class="selectGender">
        <option v-for="(items, index) in Generos" :key="index" class="opcs"> {{  items }}</option>
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
  border-radius: 1.5rem;
  padding: 1rem;
  background-color: rgba(115, 235, 189, 0.068);
}
.formulario {
  width: 100%;
  margin: auto;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 1.5rem;
  border: 1px solid rgba(115, 235, 189, 0.24);
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
  color: rgba(255, 255, 255, 0.582) !important;
  background-color: rgb(37, 37, 37) !important;
  height: 36px;
}
.opcs{
  color: rgba(255, 255, 255, 0.582);
  background-color: rgba(255, 255, 255, 0.082);
  height: 36px; 
}
</style>