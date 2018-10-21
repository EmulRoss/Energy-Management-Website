<template>
  <div id="app">
    <b-navbar sticky="true" toggleable="md" type="dark" variant="dark">

      <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

      <b-navbar-brand href="#">Wits Energy Management</b-navbar-brand>

      <b-collapse is-nav id="nav_collapse">

        <b-nav-form>
          <b-button-group>
            <b-button :pressed= "true">Daily</b-button>
            <b-button :pressed= "false">Monthly</b-button>
            <b-button :pressed= "false">Yearly</b-button>
          </b-button-group>
        </b-nav-form>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">

          <b-nav-form>
            <b-button-group>
              <b-button :pressed= "false">Actuals</b-button>
              <b-button :pressed= "true">Deviation</b-button>
            </b-button-group>
          </b-nav-form>


          <b-nav-item-dropdown text="Entity Selection" right>
            <b-dropdown-item href="#">Braamfontein Campus</b-dropdown-item>
          </b-nav-item-dropdown>

          
        </b-navbar-nav>

      </b-collapse>
    </b-navbar>

    <!-- navbar-1.vue -->
    <!--<img src="./assets/logo.png">-->
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /*margin-top: 60px;*/
  height: 94vh;
}
</style>
