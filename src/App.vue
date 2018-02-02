<template>  
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">{{ apptitle }}</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
    </nav>

    <img class="bird-img" src="./assets/prow-featured.jpg">
    <section class="jumbotron text-center" style="margin-bottom:0px;">
      <div class="container">
        <h1 class="jumbotron-heading">{{apptitle}}</h1>
        <p class="lead text-muted">Expresate libre. Enterate fácil.</p>        
      </div>
    </section>
    
    <div class="d-md-flex flex-md-equal w-100 my-md-3 pl-md-3">
      <div class="bg-dark mr-md-3 py-3 px-3 pt-md-5 px-md-5 text-center text-white overflow-hidden" style="flex:1;">
        <div class="my-3 py-3">
          <h2 class="display-5">Enterate</h2>
          <p class="lead">Echa un vistazo a las últimas publicaciones</p>
        </div>
        
        <div class="card mb-3" v-for="anuncio in anuncios" :key="anuncio._id">
          <div class="card-header">
            <strong>{{anuncio.autor.nombre}} {{ anuncio.autor.apellido }} ({{ anuncio.autor.email }})</strong>
            <span class="card-subtitle mr-2 text-muted">{{ anuncio.createdAt }}</span>
          </div>
          <div class="card-body">
            <p class="card-text">{{ anuncio.contenido }}</p>
          </div>
          <div class="card-footer text-muted">
            {{ anuncio.ubicacion }}
          </div>
        </div>
        
      </div>
      <div class="bg-light mr-md-3 pt-3 px-3 pt-md-5 px-md-5 text-center overflow-hidden" style="flex:1;">
        <div class="my-3 p-3">
          <h2 class="display-5">Expresate</h2>
          <p class="lead">Comunica tus ideas.</p>
        </div>
        <div>
          <form id="form">
            <div class="form-group row">
              <label for="usrlst" class ="col-sm-2 col-form-label">Autor:</label>
              <div class="col-sm-10">
                <select class="form-control" name="autor" id="usrlst" v-model="anuncio.autor">
                  <option v-for="autor in usuarios" :value="autor._id">
                    {{ autor.nombre }} {{ autor.apellido }} - <span class="text-muted">({{ autor.email }})</span>
                  </option>
                </select>
              </div>
            </div>
            
            <div class="form-group row">
              <label for="cntnttxt" class ="col-sm-2 col-form-label">Contenido:</label>
              <div class="col-sm-10">
                <textarea class="form-control" id="cntnttxt" name="contenido" v-model="anuncio.contenido" rows="4"></textarea>
              </div>
            </div>
            
            <div class="form-group row">
              <label for="lctninpt" class ="col-sm-2 col-form-label">Ubicación:</label>
              <div class="col-sm-10">
                <input type="text" class="form-control" id="lctninpt" name="ubicacion" v-model="anuncio.ubicacion"/>
              </div>
            </div>
            <button class="btn btn-dark" @click.prevent="create">Create</button>
          </form>
        </div>
        
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import config from "./config.json";

export default {
  name: 'TwitNow',
  data () {
    return {
      apptitle: 'TwitNow',
      anuncios: [],
      usuarios: [],
      anuncio: {
        contenido : '',
        autor:'',
        ubicacion : ''
      }
    }
  },
  created (){
    this._getUsuarios();
    this._getAnuncios();
  },
  
  methods: {
    _getAnuncios(){
      axios.get(`${config.baseURL}/anuncios`,{
        withCredentials: true
      })
      .then( response => {
        
        this.anuncios = response.data.data;
      })
    },
    _getUsuarios(){
      axios.get(`${config.baseURL}/usuarios`,{
        withCredentials: true
      })
      .then( response => {
        this.usuarios = response.data.data;
      })
    },
    
    create(){
      console.log("anuncio.autor = " + this.anuncio.autor + " - anuncio.contenido = " + this.anuncio.contenido);
      if (this.anuncio.autor.length > 0 && this.anuncio.contenido.length > 0 ){
        let payload = "";
        Object.keys(this.anuncio).forEach(key => {
          payload+=`${key}=${this.anuncio[key]}&`
        });
        
        axios.post(`${config.baseURL}/anuncios`, payload, {
          withCredentials: true,
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
            //'Content-Type': 'application/application/json'
          }
        })
        .then( response => {
          console.log("Se ejecuta getAnuncios");
          this._getAnuncios();
        })
      }
      
    }
  }
}
</script>

<style>

</style>
