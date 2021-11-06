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
                        <h5 v-if="listarea.length == 0">No hay laburo</h5>

                        <ul class="list-group">
                          <li v-for="(tarea,index) of listarea" :key="index" 
                          class="list-group-item d-flex justify-content-between">
                            <span class="cursor" v-bind:class="{'text-success' : tarea.estado}"
                            v-on:click="editartarea(tarea, index)">
                              <i v-bind:class="[ tarea.estado ? 'fas fa-clock' : 'far fa-circle']"></i>
                            </span>
                            {{tarea.nombre}}
                            <span class="text-danger cursor" v-on:click="elimitarTarea(index)">
                              <i class="fas fa-bars"></i>
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
    },
    elimitarTarea(index){
      this.listarea.splice(index,1)
    },
    editartarea(tarea,index){
      this.listarea[index].estado = !tarea.estado
    }
  }
}
</script>

<style scoped>
.cursor{
  cursor: pointer;
}
</style>
