  <!-- eslint-disable vue/no-parsing-error -->
  <template>
    
    <v-app>
      <div class="teams">
  <v-card-title>
    <v-spacer></v-spacer>
    <v-text-field
      v-model="search"
      append-icon="mdi-magnify"
      label="Поиск команды"
      single-line
      hide-details
    ></v-text-field>
  </v-card-title>
  <v-data-table
  :headers="headers"
    :search="search"
    :items=" teams"      
    :items-per-page="5"
  ></v-data-table>
  <v-card>
    <h1 class="subheading blue--text">Команды</h1>
    <v-container class="my-3" >
      <v-layout row wrap>
        <v-flex v-for="item in teams" :key="item.name" xs16 sm6 md4 lg3> 
          <v-hover v-slot="{ hover }">
        <v-card  
        class="mx-auto"
      max-width="344"
      variant="outlined">
      <p class="mb-4"></p>
          <v-expand-transition>
            <div v-if="hover"><v-btn color="primary text-center" href="/score" target="_blank">Результаты матчей </v-btn></div>
          </v-expand-transition>
          <v-responsive class="pt-5 text-center text-h4 black--text grey">
            {{ item.name }}
          </v-responsive>
          <v-card-text>
            <div class="text-overline mb-1 text-center" >
          <img :src="item.crest" height="150" /></div>
            <div class="text-h3 mb-1 text-center">{{ item.founded }}</div>
            <div class="text-h4 mb-1 text-center">{{ item.clubColors }}</div>
          </v-card-text >   
          <v-card-action>
          </v-card-action>
        </v-card>
      </v-hover>
        </v-flex>
      </v-layout>
    </v-container>
    <div class="text-center">
      </div>
    </v-card>
  </div>
  </v-app>
  </template>
    
  <script>
  export default {
    name: 'Teams',
      data() {
      return {
        headers: [],
        search: '',
        teams: [
          { text: 'Герб', value: 'crest', align: 'center' },
          { text: 'Название лиги', value: 'name' },
          { text: 'Год основания', value: 'founded'},
          { text: 'Год основания', value: 'clubColors'}
        ],
      }
    },

    mounted() {
  this.$nextTick(function () {
    this.getData()
  })
  },
    methods: {
      handlePageChange(value) {
        this.currentPage = value;
      },
      getData() {
        console.log('Ok')
        this.$axios.$get('api/competitions/WC/teams/').then((res) => {
          console.log(res)
          this.teams = res.teams
        })
      },
    },
  }

  </script>
<style scoped>
.my-3 {
  background: url('../static//field11.jpg');
  background-size: center;
  height: 100vh;
}
</style>