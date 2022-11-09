<template>

<div class="table-responsive">
  <br>
  <br>
  <table class="table table-light">
    <tr>
      <th>Pregunta</th>
      <th>Enunciado</th>
      <th>Respuesta</th>
    </tr>

    <tr v-for="(pregunta, index) in preguntas" :key="index">
      <td>{{ pregunta.pregunta }}</td>
      <td>{{ pregunta.enunciado }}</td>
      <td>{{ pregunta.respuesta }}</td>
    </tr>
  </table>
</div>

</template>

<script>

  export default  {
    name: 'src-components-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
        preguntas: [
            { pregunta: 'Pregunta 1',  enunciado: 'Como es la forma correcta para registrar un evento de click en Vue.js?', respuesta: 'd) v-on:click'},
            { pregunta: 'Pregunta 2',  enunciado: 'El modificador trim recorta...', respuesta: 'c) Los espacios adelante y atrás en una entrada de texto'},
            { pregunta: 'Pregunta 3',  enunciado: '¿Cuál de estas directivas se utiliza para modificar estilos a través de Vue.js?', respuesta: 'e) :style'}
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

</style>
