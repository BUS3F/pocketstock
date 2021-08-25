<template>
  <v-dialog
    content-class="elevation-0"
    v-model="dialogtipo"
    max-width="20rem"
    persistent
  >
    <v-card v-on:keyup.enter="submit()" class="cont-card" elevation="2">
      <v-toolbar light flat>
        <v-btn icon color="dark" @click="onClose">
          <v-icon> mdi-close </v-icon>
        </v-btn>
        <v-toolbar-title>Crear tipo</v-toolbar-title>
      </v-toolbar>
      <v-row>
        <v-col sm="6" md="12" lx="13">
          <v-text-field
            v-model="name"
            :counter="10"
            label="Nombre tipo"
            required
          ></v-text-field>
        </v-col>
      </v-row>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="grey darken-2" @click="clear" outlined> Limpiar </v-btn>
        <v-btn
          color="yellow darken-2"
          class="mr-4"
          v-on:click="submit"
          outlined
        >
          Guardar tipo
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
  import { postTipos } from "@/api/tipos.js";
  import store from "@/store";

  export default {
    name: "creartipo",
    props: {
      dialogtipo: { dafault: false },
    } /*data de llegado de componente padre creacion*/,
    data: () => ({
      name: "",
    }),

    methods: {
      onClose() {
        /*Envia parametro de cierre a componente creación*/
        this.$emit("update:dialogtipo", false);
      },
      submit() {
        //this.$emit("dialogFromChild", false);
        store.commit("setsuccess", false); //para resetear el valor de la notificion en una nueva entrada
        store.commit("setdanger", false);
        let enviar = {
          name_tipo: this.name,
        };
        postTipos(enviar);
        this.clear();
      },
      clear() {
        this.name = "";
      },
    },
  };
</script>

<style scoped>
  .cont-card {
    padding: 1rem;
  }
</style>