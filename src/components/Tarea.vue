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
<<<<<<< Updated upstream
                        <div class="text-center">
                        <div v-if="loading" class="spinner-border text-success" role="status">
                          <span class="sr-only">Loading...</span>
                          </div>
                          </div>
                        <h5 v-if="listarea.length == 0">No hay laburo</h5>
                          <ul v-if="!loading" class="list-group">

                            <li
                              v-for="(tarea, index) of listarea" 
                              :key="index" 
                              class="list-group-item d-flex justify-content-between">
                            
                            <span 
                              class="cursor" 
                              v-bind:class="{'text-success' : tarea.estado}"
                              v-on:click="editartarea(tarea, tarea.id)">
                              <i v-bind:class="[ tarea.estado ? 'fas fa-clock' : 'far fa-circle']"></i>
                            </span>
                            {{tarea.nombre}}
                            <span class="text-danger cursor" v-on:click="eliminarTarea(tarea.id)">
                              <i class="fas fa-bars"></i>
                              </span>
=======
                        {{ listarea }}
                        <ul class="list-group">
                          <li class="list-group-item d-flex justify-content-around">
                            <span class="cursor" v-on:click="editarTarea(tarea, index)">
                              <i v-bind:class="[tarea.estado ? 'far fa-circle-check' : 'far fa-circle']" 
                              class="fa-solid fa-circle-check"></i>
                              <i class="far fa-circle"></i>
                            </span>
                            {{tarea.nombre}}
                            <span class="text-danger cursor">
                              <i class="far fa-circle"></i><i class="fa-solid fa-xmark"></i>
                              <i class="fa-duotone fa-circle-check"></i>
                            </span>
>>>>>>> Stashed changes
                          </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'tarea',
  data(){
    return {
      tarea: '',
      listarea: [],
      loading: false
    }
  },
  methods: {
    agregarTarea() {
      const tarea = {
        nombre: this.tarea,
        estado: false
      }
      /*this.listarea.push(tarea);*/
      this.loading = true;
      axios.post("https://localhost:44349/api/Tarea/", tarea)
      .then(response => {
        console.log(response);
        this.loading = false;
        this.obtenerTareas();
      }).catch(error => {
        console.error(error);
        this.loading = false;
      })
      this.tarea ='';
<<<<<<< Updated upstream
    },
    eliminarTarea(id){
      /*this.listarea.splice(index,1)*/
      axios.delete("https://localhost:44349/api/Tarea/" + id).then(response => {
        console.log(response);
        this.obtenerTareas();
        this.loading = false;
      }).catch(error => {
        console.log(error);
        this.loading = false;
      } )
    },
    editartarea(tarea,id){
      /*this.listarea[index].estado = !tarea.estado */
      this.loading = true;
      axios.put("https://localhost:44349/api/Tarea/" + id, tarea).then(()=>{
        this.obtenerTareas();
        this.loading = false
      }).catch(()  => this.loading = false)
    },
    obtenerTareas(){
      this.loading = true;
      axios.get("https://localhost:44349/api/Tarea/")
      .then(response => {
        console.log(response);
        this.listarea = response.data;
        this.loading = false;
      }).catch(() => this.loading = false)
=======
>>>>>>> Stashed changes
    }
  },
  created: function() {
    this.obtenerTareas();
  }
}
</script>

<style scoped>
.cursor{
  cursor: pointer;
}
</style>
