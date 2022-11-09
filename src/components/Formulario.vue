<template>

  <section class="src-componentes-formulario-av">
    <div class="jumbotron">
      <h2>Componente FormularioAv</h2>
      <hr>
      <hr>
      <br>

  <vue-form :state="formState" @submit.prevent="enviar()">
    
        <!-- --------------------------- Campo Nombre ---------------------------- -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
            id="nombre"
            class="form-control"
            type="text" 
            v-model.trim="formData.nombre" 
            required 
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            name="nombre"
            autocomplete="off"
            no-espacios
          />
          <!-- Validación -->
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{nombreMinLength}} caracteres.
            </div>

            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo no debe superar los {{nombreMaxLength}} caracteres.
            </div>

            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no admite espacios intermedios.
            </div>
          </field-messages>
        </validate>
        <br>

        <!-- --------------------------- Campo Descripcion ---------------------------- -->
        <validate tag="div">
          <label for="descripcion">Descripcion</label>
          <input 
            id="descripcion"
            class="form-control"
            type="text" 
            v-model.trim="formData.descripcion" 
            required 
            name="descripcion"
            autocomplete="off"
          />
          <!-- cartel de validación -->
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          </field-messages>
        </validate>
        <br>
    
        <!-- --------------------------- Campo Importe ---------------------------- -->
        <validate tag="div">
          <label for="importe">importe</label>
          <input 
            id="importe"
            class="form-control"
            type="number" 
            v-model.number="formData.importe" 
            required 
            name="importe"
            autocomplete="off"
            :min="importeMin"
          />
          <!-- cartel de validación -->
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">
              El importe debe ser mayor que {{importeMin}}.
            </div>
          </field-messages>
        </validate>
        <br>
    
        <!-- -------------------------- Botón de envío ----------------------------- -->
        <button class="btn btn-success my-3" :disabled="formState.$invalid">Enviar</button>
      </vue-form>    
    </div>

    <div class="table-responsive">
  <br>
  <br>
  <table class="table table-dark">
    <tr>
      <th>Nombre</th>
      <th>Descripción</th>
      <th>Importe</th>
      <th>Fecha</th>
    </tr>

    <tr v-for="(ingreso, index) in ingresos" :key="index">
      <td>{{ ingreso.nombre }}</td>
      <td>{{ ingreso.descripcion }}</td>
      <td>{{ ingreso.importe }}</td>
      <td>{{ ingreso.fecha }}</td>
    </tr>

    <tr>
      <th>Suma Total</th>
    </tr>
    <tr>
      <td>$ {{importeTotal}}</td>
    </tr>
  </table>
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
        importeTotal: 0,
        formState : {},
        formData: this.getInitialData(),
        nombreMinLength: 3,
        nombreMaxLength: 15,
        importeMin: 0,

        ingresos: [
            {}
        ]
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre: null,
          descripcion: null,
          importe: null,
        }
      },
      enviar() {
        console.log({...this.formData})
        
        let ingreso = {nombre: this.formData.nombre, descripcion: this.formData.descripcion, importe: this.formData.importe}
        ingreso.fecha = new Date().toLocaleString()
        this.ingresos.push(ingreso)
        this.importeTotal += this.formData.importe
        this.formData = this.getInitialData()
        this.formState._reset()
      }
    },
    computed: {

    }
}

</script>

<style scoped lang="css">

</style>
