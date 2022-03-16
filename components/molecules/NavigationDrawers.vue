<template>
  <v-navigation-drawer v-model="drawer" app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
            DashBoard
          </v-list-item-title>
          <v-list-item-subtitle>
            Portal Fornecedor
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    props:{
      drawer:{
        type:Boolean,
        default: false
      }
    },
    data(){
      return{
        items: [
          { title: 'Dashboard', icon: 'mdi-view-dashboard', to:'/' },
          { title: 'Fornecedor', icon: 'mdi-account-multiple', to:'/fornecedores' },
          { title: 'Representantes', icon: 'mdi-briefcase', to:'/representantes' },
          { title: 'Configurações', icon: 'mdi-cog-outline', to:'#' },
        ],
      }
    }
  })
</script>

<style scoped>

</style>
