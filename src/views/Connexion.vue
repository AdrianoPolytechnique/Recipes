<template>
  <v-container class="px-0">
    <v-layout class="mx-0 mt-4" row justify-space-around>
      <v-flex xs10 md8>
        
          <v-card class="pa-5 pt-1">
            <v-card-title :class="[color+'--text','text-center','text-h4']">Connexion</v-card-title>
            <v-text-field
                  label="Adresse email"
                  :rules="emailRules"
                  v-model="mail"
                  outlined
                  :class="color+'--text'"
                ></v-text-field>

                <v-text-field
                  label="Mot de passe"
                  :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
                  :type="show ? 'text' : 'password'"
                  counter
                  @click:append="show = !show"
                  :rules="mdpRules"
                  v-model="motdepasse"
                  outlined
                ></v-text-field>

                <v-card-actions>
                  <v-layout row justify-space-around wrap>
                    
                    <v-flex xs8 md4 text-center>
                      <v-btn text @click="connexion"  class="align-center text-center">
                        <v-icon left>login</v-icon>
                        <div>Connexion</div>
                      </v-btn>
                    </v-flex>
                    
                    <v-flex text-center class="mt-4 mt-md-0" xs10 md6>
                      <v-btn text router to="/oublie"><v-icon left>mood_bad</v-icon>Mot de passe oublié ?
                      </v-btn>
                    </v-flex>
                   
                  </v-layout>
                </v-card-actions>
          </v-card>
        
      </v-flex>
    </v-layout>
    <v-snackbar v-model="snackOpen">Identifiant ou mot de passe incorrect</v-snackbar>
  </v-container>
</template>

<script>
import all from '../fb';
const auth = all.auth;
export default {
  data() {
    return {
      show: false,
      emailRules: [
        (v) => !!v || "E-mail requit",
        (v) => /^[\w-.]+@[\w-]+\.[a-zA-Z]+(\.[a-zA-Z]+)?$/.test(v) || "E-mail must be valid",
      ],
      mdpRules: [
        (v) => !!v || "Mot de passe requit",
        (v) => v.length > 6 || "Mot de passe trop court",
      ],
      mail: "",
      motdepasse: "",
      snackOpen:false,
      
    };
  },
  computed:{
    color(){return this.$store.getters.color},
  },
  methods: {
    connexion() {
      
      auth.signInWithEmailAndPassword(this.mail,this.motdepasse)
      .then(credentials=>{
      this.$store.commit('setUid',credentials.user.uid);
      this.$router.push('/mesrecettes')
      }).catch((err)=>{this.snackOpen=true;console.log(err);})
    },
  },
};

</script>

<style scoped>

</style>