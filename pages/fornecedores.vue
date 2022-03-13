<template>
    <v-container>
      <v-card max-width="900" class="my-12">
        <v-alert
        border="left"
        colored-border
        type="info"
        elevation="2"
      >
        Adicione um e-mail para poder cadastrar um fornecedor
      </v-alert>
      </v-card>
      <v-row>
      <v-col cols="6">
        <v-text-field
            v-model="email"
            :rules="[rules.required, rules.email]"
            label="E-mail"
          ></v-text-field>
          <v-btn
            depressed
            color="primary"
            class="mt-4"
          >
            Enviar
          </v-btn>
        </v-col>
      </v-col>
    </v-row>
    </v-container>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    layout:'dashboard',
    data(){
      return{
        email:'',
        rules: {
          required: value => !!value || 'E-mail é obrigatório.',
          counter: value => value.length <= 20 || 'Max 20 characters',
          email: value => {
            const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
            return pattern.test(value) || 'Formato de e-mail inválido.'
          },
        },
      }
    }
  })
</script>

<style scoped>

</style>
