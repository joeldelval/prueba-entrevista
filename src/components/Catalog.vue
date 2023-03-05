<template>
  <v-container fluid>
    <v-row class="mx-auto ml-16 mr-16">
      <v-col v-for="card in fPaginator()" :key="card.id" cols="12" sm="6" md="4">
        <v-card class="mx-auto" >
          <v-img :src="'https://lh3.googleusercontent.com/p/AF1QipO1uVjaiiQpAMcPF38enjwwYF8OoFSYFd4TT0zg=s680-w680-h510'" height="200"></v-img>
          <v-card-title>{{ card.title }}</v-card-title>
          <v-card-text>{{ fTruncateBody(card.body) }} <span v-if="card.body.length > 110" class="ver-mas" @click="fShowModal">... ver más</span></v-card-text>
        </v-card>
        <v-dialog v-model="dModalActive">
          <v-card>
            <v-img :src="'https://lh3.googleusercontent.com/p/AF1QipO1uVjaiiQpAMcPF38enjwwYF8OoFSYFd4TT0zg=s680-w680-h510'" height="200"></v-img>
            <v-card-title>{{ card.title }}</v-card-title>
            <v-card-text>{{ card.body }}</v-card-text>
            <v-card-actions>
              <v-btn @click="dModalActive = false">Cerrar</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" class="text-center">
        <v-pagination v-model="dCurrentPage" :length="dNumPages" :total-visible="5"></v-pagination>
      </v-col>
    </v-row>
    
  </v-container>

</template>

<script>
export default {
  name: 'Catalog',
  props: {
    pData: {
      type: Object,
      required: true
    },
    pSearch: {
      type: String,
      required: false,
      default: ""
    }
  },
  data() {
    return {
      dPerPage: 6,
      dNumPages: 10,
      dCurrentPage: 1,
      dCards: [],
      dModalActive: false
    }
  },
  methods: {
    fPaginator() {
      const selectedElements = this.pData.filter(element => element.title.includes(this.pSearch)).slice(this.dCurrentPage -1, this.dCurrentPage + this.dPerPage -1);
      this.dNumPages = Math.floor(this.pData.filter(element => element.title.includes(this.pSearch)).length / 6)
      return selectedElements;
    },
    fTruncateBody(body) {
      return body.slice(0, 110);
    },
    fShowModal () {
      this.dModalActive = true
    }
  }
}
</script>