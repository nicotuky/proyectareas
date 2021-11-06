<template>
<div>
  <h1 class="display-4 text-center">Listado de tareas</h1>
  <hr>
        <div class="row">
            <div class="col-lg-8- offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="tarea"  class="form-control form-control-lg" placeholder="Listado">  
                            <div class="input-group-append">
                                <button v-on:click="agregarTarea()" 
                                class="btn btn-success btn-lg">Agregar</button> 
                            </div>         
                        </div>
                        <br>
                        {{ listarea }}
                        <ul class="list-group">
                          <li class="list-group-item d-flex justify-content-around">
                            <span class="cursor">
                              <i class="far fa-circle"></i>
                            </span>
                            Estoy sintiendo los efectos de la masculinidad
                            <span class="text-danger cursor">
                              <i class="far fa-circle"></i><i class="fa-solid fa-xmark"></i>
                              <i class="fa-duotone fa-circle-check"></i>
                            </span>
                          </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
</div>
</template>

<script>
export default {
  name: 'tarea',
  data(){
    return {
      tarea: '',
      listarea: []
    }
  },
  methods: {
    agregarTarea() {
      const tarea = {
        nombre: this.tarea,
        estado: false
      }
      this.listarea.push(tarea);
      this.tarea ='';
    }
  }
}
</script>

<style scoped>
.cursor{
  cursor: pointer;
}
</style>
