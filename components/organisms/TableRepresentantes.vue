<template>
  <v-data-table
    :headers="headers"
    :items="representantes"
    sort-by="calories"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Representantes</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="600px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              Novo
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.nome"
                      label="Nome"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.telefone"
                      label="Telefone"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.email"
                      label="E-mail"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.nascimento"
                      label="D/Nascimento"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.endereco"
                      label="Endereço"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.cidade"
                      label="Cidade"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.estado"
                      label="Estado"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    data: () => ({
      dialog: false,
      dialogDelete: false,
      headers: [
        {
          text: 'Tipo',
          align: 'start',
          sortable: false,
          value: 'tipo',
        },
        { text: 'Nome', value: 'nome' },
        { text: 'Telefone', value: 'telefone' },
        { text: 'E-mail', value: 'email' },
        { text: 'D/Nascimento', value: 'nascimento' },
        { text: 'Endereço', value: 'endereco' },
        { text: 'Cidade', value: 'cidade' },
        { text: 'Estado', value: 'estado' },
        { text: 'Ações', value: 'actions', sortable: false },
      ],
      representantes: [] as any,
      editedIndex: -1,
      editedItem:{
        nome:'',
        telefone:'',
        email:'',
        nascimento:'',
        endereco:'',
        cidade:'',
        estado:'',
      },
      defaultItem:{
        nome:'',
        telefone:'',
        email:'',
        nascimento:'',
        endereco:'',
        cidade:'',
        estado:'',
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === null? 'Novo Representante' : 'Editar Representante'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.representantes = [
          {
            nome: 'João Silva',
            telefone:'(88)99999-9999',
            email:'joao@hotmail.com',
            nascimento:'12/10/1999',
            cep:'6000000',
            endereco:'Rua Abc 12',
            cidade:'Fortaleza',
            estado:'CE',
            tipo:'Comercial'
          },
          {
            nome: 'Maria Silva',
            telefone:'(88)99999-9999',
            email:'maria@hotmail.com',
            nascimento:'12/10/1989',
            cep:'6000000',
            endereco:'Rua Abc 12',
            cidade:'Fortaleza',
            estado:'CE',
            tipo:'Financeiro'
          },
          {
            nome: 'Fulano Silva',
            telefone:'(88)99999-9999',
            email:'fulano@hotmail.com',
            nascimento:'12/10/1979',
            cep:'6000000',
            endereco:'Rua Abc 12',
            cidade:'Fortaleza',
            estado:'CE',
            tipo:'Sócio'
          },
        ]
      },
      close(){
        this.dialog = false
      },
      closeDelete(){
        this.dialogDelete = false
      },
      editItem(item){
        this.editedIndex = this.representantes.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },
      deleteItem (item) {
        this.editedIndex = this.representantes.indexOf(item)
        this.dialogDelete = true
      },
      save(){
        this.close()
      },
      deleteItemConfirm () {
        this.representantes.splice(this.editedIndex, 1)
        this.closeDelete()
      },
    },
  })
</script>

<style scoped>

</style>
