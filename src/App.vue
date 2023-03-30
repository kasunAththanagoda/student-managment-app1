<template>
  <v-app>
    <NavBar></NavBar>
    
    <v-main>
     <router-view></router-view>
    </v-main>
    <FooterBar></FooterBar>

  </v-app>
</template>

<script>
import NavBar from '@/components/NavBar'
import FooterBar from './components/FooterBar.vue';

export default {

    name: "App",
    data: () => ({
    //
    }),
    components:{
      NavBar,
      FooterBar
      

    }

    
};
</script>


