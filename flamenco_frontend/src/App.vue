<template>
    <div>
    <div class="form-row">
      <div class="col">
        <label for="txt_primernombre">Primer nombre:</label>
        <input type="text" id="txt_primernombre" name="txt_primernombre" aria-describedby="ayuda_primer_nombre" class="form-control" v-model="formData.primernombre" placeholder="Primer Nombre">
        <small id="ayuda_primer_nombre" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_fechanacimiento">Fecha de nacimiento:</label>
        <input type="text" id="txt_fechanacimiento" name="txt_fechanacimiento" aria-describedby="ayuda_fecha_nacimiento" class="form-control" v-model="formData.fechanacimiento" placeholder="Fecha de Nacimiento">
        <small id="ayuda_fecha_nacimiento" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_profesion">Profesión:</label>
        <input type="text" id="txt_profesion" name="txt_profesion" aria-describedby="ayuda_profesion" class="form-control" v-model="formData.profesion" placeholder="Profesión">
        <small id="ayuda_profesion" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_colorojos">Color de ojos:</label>
        <input type="text" id="txt_colorojos" name="txt_colorojos" aria-describedby="ayuda_color_ojos" class="form-control" v-model="formData.colorojos" placeholder="Color de Ojos">
        <small id="ayuda_color_ojos" class="form-text text-muted">Esta es una descripción del campo</small>
      </div>
      <div class="col">
        <label for="txt_segundonombre">Segundo nombre:</label>
        <input type="text" id="txt_segundonombre" name="txt_segundonombre" aria-describedby="ayuda_segundo_nombre" class="form-control" v-model="formData.segundonombre" placeholder="Segundo Nombre">
        <small id="ayuda_segundo_nombre" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_edad_anios">Edad (años):</label>
        <input type="number" id="txt_edad_anios" name="txt_edad_anios" aria-describedby="ayuda_edad_anios" class="form-control" v-model="formData.edad_anios" readonly>
        <small id="ayuda_edad_anios" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_estadofamiliar">Estado familiar:</label>
        <input type="text" id="txt_estadofamiliar" name="txt_estadofamiliar" aria-describedby="ayuda_estado_familiar" class="form-control" v-model="formData.estadofamiliar" placeholder="Estado Familiar">
        <small id="ayuda_estado_familiar" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_residencia">Dirección de residencia:</label>
        <input type="text" id="txt_residencia" name="txt_residencia" aria-describedby="ayuda_residencia" class="form-control" v-model="formData.residencia" placeholder="Dirección de residencia">
        <small id="ayuda_residencia" class="form-text text-muted">Esta es una descripción del campo</small>
      </div>
      <div class="col">
        <label for="txt_primerapellido">Primer apellido:</label>
        <input type="text" id="txt_primerapellido" name="txt_primerapellido" aria-describedby="ayuda_primer_apellido" class="form-control" v-model="formData.primerapellido" placeholder="Primer Apellido">
        <small id="ayuda_primer_apellido" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_peso">Peso (libras):</label>
        <input type="number" id="txt_peso" name="txt_peso" aria-describedby="ayuda_peso" class="form-control" v-model="formData.peso" placeholder="Peso">
        <small id="ayuda_peso" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_colorpiel">Color de piel:</label>
        <input type="text" id="txt_colorpiel" name="txt_colorpiel" aria-describedby="ayuda_color_piel" class="form-control" v-model="formData.colorpiel" placeholder="Color de piel">
        <small id="ayuda_color_piel" class="form-text text-muted">Esta es una descripción del campo</small>
      </div>
      <div class="col">
        <label for="txt_segundoapellido">Segundo apellido:</label>
        <input type="text" id="txt_segundoapellido" name="txt_segundoapellido" aria-describedby="ayuda_segundo_apellido" class="form-control" v-model="formData.segundoapellido" placeholder="Segundo Apellido">
        <small id="ayuda_segundo_apellido" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_estatura">Estatura (metros):</label>
        <input type="number" id="txt_estatura" name="txt_estatura" aria-describedby="ayuda_estatura" class="form-control" v-model="formData.estatura" placeholder="Estatura">
        <small id="ayuda_estatura" class="form-text text-muted">Esta es una descripción del campo</small>
        <br />
        <label for="txt_colorcabello">Color de cabello:</label>
        <input type="text" id="txt_colorcabello" name="txt_colorcabello" aria-describedby="ayuda_color_cabello" class="form-control" v-model="formData.colorcabello" placeholder="Color de cabello">
        <small id="ayuda_color_cabello" class="form-text text-muted">Esta es una descripción del campo</small>
      </div>
    </div>
    <button @click="obtenerDatos" class="btn btn-primary">Obtener datos</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data(){
    return{
      formData:{
      primernombre: "", 
      segundonombre: "", 
      primerapellido: "", 
      segundoapellido: "", 
      fechanacimiento: "", 
      estadofamiliar: "", 
      residencia: "", 
      profesion: "", 
      estatura: 0, 
      peso: 0, 
      colorpiel: "", 
      colorojos: "", 
      colorcabello: "",
      edad_anios: 0,
      edad_meses: 0,
      edad_dias: 0
      }
    }
  },
 methods:{
  async obtenerDatos(){
    try {
      const response = await axios.get('http://localhost:3000/usuario');
      this.formData = response.data;
      this.calcular_edad();
    } catch (error) {
      console.log('ERROR OBTENIENDO LOS DATOS:', error);
    }
  },
  calcular_edad(){
    const ahora = new Date();
    const objetoNacimiento =new Date(this.formData.fechanacimiento);

    let anios = ahora.getFullYear() - objetoNacimiento.getFullYear();
    let meses = ahora.getMonth() - objetoNacimiento.getMonth();
    let dias = ahora.getDate() - objetoNacimiento.getDate();

    if(dias < 0){
      meses--;
      const ultimosdiadelmesanterior = new Date(ahora.getFullYear(),ahora.getMonth(),0).getDate();
      dias = ultimosdiadelmesanterior+dias;
    }

    if (meses < 0) {
      anios--;
      meses=12 + meses;
      
    }

    this.formData.edad_anios = anios;
    this.formData.edad_meses = meses;
    this.formData.edad_dias = dias;
  }
 },
 mounted(){
  //opcionalmente se obtienen los datos cuando el componente es creado, sin necesidad de presionar el boton
  //this.obtenerDatos();

 }
}
</script>

<style>

</style>