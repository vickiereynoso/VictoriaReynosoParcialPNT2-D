<template>

  <section class="src-components-formulario">
        <div class="jumbotron">
      <hr>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
       
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
          type="text" 
          id="nombre" 
          no-espacios 
          name="nombre" 
          class="form-control"
          v-model.trim="formData.nombre" 
          required minlength="3" 
          maxlength="15" 
          autocomplete="off" 
          >
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido.</div>

            <div slot="minlength" class="alert alert-danger mt-1">Este campo debe poseer al menos 3 caracteres.</div>

            <div v-if="formData.nombre && (formData.nombre.length == 15)" class="alert alert-danger mt-1">Este campo debe poseer como máximo 15 caracteres.</div>

            <div slot="no-espacios" class="alert alert-danger mt-1">No se permiten espacios intermedios en este campo.</div>
          </field-messages>

        </validate>

        <br>

        <validate tag="div">
          <label for="apellido">Apellido</label>
          <input 
          type="text" 
          id="apellido"
          name="apellido"  
          class="form-control"
          v-model.trim="formData.apellido"
          required minlength="3" 
          maxlength="15" 
          autocomplete="off"
          
          > 
          
          <field-messages name="apellido" show="$dirty"> 

            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido.
            </div>

            <div slot="minlength" class="alert alert-danger mt-1">Este campo debe poseer al menos 3 caracteres.</div>

            <div v-if="formData.apellido && (formData.apellido.length == 15)" class="alert alert-danger mt-1">Este campo debe poseer como máximo 15 caracteres.</div>

            <div slot="no-espacios" class="alert alert-danger mt-1">No se permiten espacios intermedios en este campo.</div>

          </field-messages>
        </validate>


        <validate tag="div">
          <label for="nota">Nota</label>
          <input 
          type="number" 
          id="nota" 
          v-model.number="formData.nota" 
          required name="nota" 
          autocomplete="off" 
          class="form-control" />
    
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio.</div>
          </field-messages>
        </validate>

        <br>
        
        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>
      <hr>




     
      <h2>Historial de Notas</h2>
      <hr>

      <div v-if="alumnos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>Nota</th>
          </tr>
          <tr v-for="(alumno,index) in alumnos" :key="index">
            <td>{{ alumno.nombre }}</td>
            <td>{{ alumno.apellido }}</td>
            <td>{{ alumno.nota }}</td>
          </tr>
          <tr :style="{color: getPromedio().color}">
            <td></td>
            <th>PROMEDIO</th>
            <th>{{ getPromedio().total }}</th>
            <td></td>
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger">No hay alumnos ingresados</h4>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        alumnos : [],
        promedio: null
      }
    },
    methods: {
getInitialData() {
        return {
          nombre : null,
          apellido: null,
          nota: null
        }
      },
      enviar() {
         let alumno = {...this.formData}
        
        this.alumnos.push(alumno)

        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      getPromedio() {
        let total = 0
        this.alumnos.forEach(alumno => {
          total += alumno.nota
        });
      

        let color = ''
        if((total>=0) && (total<4)) color = 'red'
        else if((total>=4) && (total<6)) color = 'yellow'
        else if((total>=7) && (total<10)) color = 'green'
        return {
          total,
          color
        }
      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-formulario {

  }
</style>
