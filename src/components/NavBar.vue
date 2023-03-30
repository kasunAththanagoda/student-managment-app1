<template>
  <div>
    <nav>
        <v-app-bar app class="indigo lighten-4">
            <v-toolbar-title >
                <span><router-link :to="{name:'home'}" class="nav-link black--text"> Managment System </router-link></span>
                <!-- <v-spacer></v-spacer> -->
                <span class="ml-4 black--text"><router-link :to="{name:'about'}" class="nav-link black--text">about</router-link></span>
            <span class="ml-4"><router-link :to="{name:'studentDetails'}" class="nav-link black--text">student details</router-link></span>
            </v-toolbar-title>
            
        </v-app-bar>
    </nav>
  </div>
</template>

<script>
export default {

}
</script>

\


<style scoped>
 .nav-link {
    text-decoration: none; /* remove underline */
    text-align: left; /* align left */
  }
</style>