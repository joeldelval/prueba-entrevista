<template>
  <v-app-bar color="accent-4" class="pt-4 pb-2" dark>
    <v-text-field v-model="dSearch" style="width: 200px;" append-icon="mdi-magnify" label="Introduce tu búsqueda"></v-text-field>
  </v-app-bar>
</template>

<script>
  export default {
    name: 'TopBar',
    data: () => ({
      dSearch: ''
    }),
    watch: {
      dSearch () {
        this.$emit('search', this.dSearch)
      }
    }
  }
</script>
