<template>
<v-container grid-list-md text-xs-center>
  <v-layout row wrap>
      <v-flex>
        <v-card>
        <v-toolbar color="light-blue" dark>
            <v-toolbar-title>Adicionar uma nota</v-toolbar-title>

          </v-toolbar>
          <v-form ref="form" v-model="valid" lazy-validation class="pa-2">
            <v-text-field
              v-model="titulo"
              label="Titulo"
              required
            ></v-text-field>

            <v-text-field
              v-model="texto"
              label="Texto"
              required
            ></v-text-field>

            <v-btn
              color="success"
              class="mr-4"
              @click="add"
            >
              Adicionar nota
            </v-btn>
          </v-form>
        </v-card>
      </v-flex>
    </v-layout>

    <v-toolbar color="light-blue" dark>
      <v-toolbar-title>Notas</v-toolbar-title>

    </v-toolbar>

    <template v-for="(item, index) in items">
      <v-layout row wrap>
        <v-flex>
          <v-card>
            <v-list two-line>
                <v-list-tile>
                  <v-list-tile-content>
                    <v-list-tile-title v-html="item.titulo"></v-list-tile-title>
                    <v-list-tile-sub-title v-html="item.texto"></v-list-tile-sub-title>
                  </v-list-tile-content>
                  <v-list-tile-action>
                    <v-btn icon ripple @click="delete_nota(index)">
                      <v-icon color="red lighten-1">delete</v-icon>
                    </v-btn>
                  </v-list-tile-action>
                </v-list-tile>
            </v-list>
          </v-card>
        </v-flex>
      </v-layout>
    </template>
</v-container>
</template>

<script>
import AppApi from '~apijs'
export default {
  data () {
    return {
      titulo: '',
      texto: '',
      items: [
      ]
    }
  },
  mounted () {
    this.loading = true
    AppApi.list_notas().then(response => {
      const notas = response.data.notas
      this.items = notas
      this.loading = false
    })
  },
  methods: {
    add () {
      const data = {
        titulo: this.titulo,
        texto: this.texto,
      }
      AppApi.add_nota(data).then(response => {
        const nota = response.data
        this.items.push(nota)
        this.titulo = ''
        this.texto = ''
      })
    },
    delete_nota (id_nota){
      AppApi.delete_nota(id_nota).then(response => {
        const id = response.data;
        this.items.splice(id, 1);
      })
    }
  }
}
</script>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
