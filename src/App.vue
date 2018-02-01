<template>  
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">{{ apptitle }}</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
    </nav>

    <img src="./assets/prow-featured.jpg">    
    <section class="jumbotron text-center" style="margin-bottom:0px;">
      <div class="container">
        <h1 class="jumbotron-heading">{{apptitle}}</h1>
        <p class="lead text-muted">Expresate libre. Enterate fácil.</p>        
      </div>
    </section>
    
    <div class="d-md-flex flex-md-equal w-100 my-md-3 pl-md-3">
      <div class="bg-dark mr-md-3 pt-3 px-3 pt-md-5 px-md-5 text-center text-white overflow-hidden" style="flex:1;">
        <div class="my-3 py-3">
          <h2 class="display-5">Enterate</h2>
          <p class="lead">Echa un vistazo a las últimas publicaciones</p>
        </div>

        <div class="container">
          <div class="row">
            <div class="bg-light col-md-12">
              <p>Autor          
              </p>
              <p>12/03/07</p>
            </div>
          </div>
          <div class="row">
            <div>
              <p>contenido bla bla bla</p>

            </div>
            
          </div>
        </div>
      </div>
      <div class="bg-light mr-md-3 pt-3 px-3 pt-md-5 px-md-5 text-center overflow-hidden" style="flex:1;">
        <div class="my-3 p-3">
          <h2 class="display-5">Another headline</h2>
          <p class="lead">And an even wittier subheading.</p>
        </div>
        <div class="bg-dark box-shadow mx-auto" style="width: 80%; height: 300px; border-radius: 21px 21px 0 0;"></div>
      </div>
    </div>
    
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TwitNow',
  data () {
    return {
      apptitle: 'TwitNow'
    }
  }
}
</script>

<style>

</style>
