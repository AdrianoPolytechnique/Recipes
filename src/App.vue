<template>
  <v-app>
    <v-app-bar
      app
      :color="color"
      dark
    >
      <div class="d-flex align-center">
        <a>
        <img
          
          class="shrink mr-2"
          contain
          src="./assets/toque.png"
          transition="scale-transition"
          width="40"
          @click="toggle"
        />
        </a>
        <a> <span @click="to_presentation" color="white" class="text-md-h5 white--text text-xs-subtitle-1">Les carnets d'Adriano</span></a>
      </div>
      
      <div class="compteur text-caption text-md-body-1">comptent {{nombreDeRecettes}} recettes</div>
    </v-app-bar>
    <Drawer/>    
    
    <v-main class="indigo lighten-5">
      <router-view></router-view>
    </v-main> 
  </v-app>
</template>

<script>
import Drawer from '@/components/Navbar.vue'

export default {
  name: 'App',

  components: {
    Drawer
  },

  data(){
    return{
     
    }
  },
  computed:{
    color(){return this.$store.getters.color},
    nombreDeRecettes(){return this.$store.getters.compteur;}
  },
  methods:{
    toggle(){
      this.$store.commit("toggle_drawer")
    },
    to_presentation(){
      if (this.$store.state.drawer_sortie){this.$store.commit("toggle_drawer")}
      this.$router.push("/mesrecettes");
    }
  }
};
</script>

<style  scoped>
.v-main{
  background-color: cyan;
}
.compteur{
  margin-top:5px;
  margin-left: min(10px,5%);
}
</style>