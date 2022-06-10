<template>

  <section class="src-components-respuestas">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <hr>
      <br>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(pregunta, index) in preguntas" :key="index">
            <td>{{pregunta.numero}}</td>
            <td>{{pregunta.respuestas}}</td>
          </tr>
        </table>
      </div>      

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
          preguntas : [ 
            { numero: 1, respuestas: ['c'] },
            { numero: 2, respuestas: ['c'] },
            { numero: 3, respuestas: ['b'] }
          ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-respuestas {

  }
</style>
