<template>
<div>
  <h1 class="display-4 text-center">Listado de tareas</h1>
  <hr>
        <div class="row">
            <div class="col-lg-8- offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="tarea"  class="form-control form-control-lg" placeholder="Agregar tarea...">  
                            <div class="input-group-append">
                                <button v-on:click="agregarTarea()" 
                                class="btn btn-success btn-lg">Agregar</button> 
                            </div>         
                        </div>
                        <br>
                        <div class="text-center">
                        <div v-if="loading" class="spinner-border text-success" role="status">
                          <span class="sr-only">Loading...</span>
                          </div>
                          </div>
                        <div class="text-center">
                         <h5 v-if="listarea.length == 0">No hay tareas pendientes.</h5>
                        </div>
                          <ul v-if="!loading" class="list-group">

                            <li
                              v-for="(tarea, index) of listarea" 
                              :key="index" 
                              class="list-group-item d-flex justify-content-between">
                            
                            <span 
                              class="cursor" 
                              v-bind:class="{'text-success' : tarea.estado}"
                              v-on:click="editartarea(tarea, tarea.id)">
                              <i v-bind:class="[ tarea.estado ? 'fa fa-check-circle' : 'far fa-circle']"></i>
                            </span>
                            {{tarea.nombre}}
                            <span class="text-danger cursor" v-on:click="eliminarTarea(tarea.id)">
                              <i class="fa fa-trash"></i>
                              </span>
                          </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <footer class="app-footer inverse" role="contentinfo">
          <div class="container">
            <p>
              <small>
                <a href="https://github.com/nicotuky/proyectareas">
                  <i class="fab fa-github"></i></a>
                  Design by Nicolás D. / Damian P.
                  </small>
              </p>
              </div>
              </footer>
</div>
</template>

<script>
import axios from 'axios';
const URL ="https://backend-tareas20211107113720.azurewebsites.net/api/Tarea/"
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
      axios.post(URL, tarea)
      .then(response => {
        console.log(response);
        this.loading = false;
        this.obtenerTareas();
      }).catch(error => {
        console.error(error);
        this.loading = false;
      })
      this.tarea ='';
    },
    eliminarTarea(id){
      /*this.listarea.splice(index,1)*/
      axios.delete(URL + id).then(response => {
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
      axios.put(URL + id, tarea).then(()=>{
        this.obtenerTareas();
        this.loading = false
      }).catch(()  => this.loading = false)
    },
    obtenerTareas(){
      this.loading = true;
      axios.get(URL)
      .then(response => {
        console.log(response);
        this.listarea = response.data;
        this.loading = false;
      }).catch(() => this.loading = false)
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
