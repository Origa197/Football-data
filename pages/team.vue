    <!-- eslint-disable vue/no-parsing-error -->
    <template>    
      <v-app>
        <div class="teams">
    <v-card-title >
      <v-spacer></v-spacer>
      <v-text-field  
      v-model="name"
        append-icon="mdi-magnify"
        label="Поиск команды"
        single-line
        hide-details
      ></v-text-field>
    <v-data-table
    :headers="headers"
      :search="search"
      :items=" teams"      
      :items-per-page="10"
    ></v-data-table>
    
    </v-card-title>
    <v-container>
      <v-card>
    <v-card>
      <h1 class="subheading blue--text">Команды</h1>
      <div id="app">
        <v-container class="my-3" >
        <v-layout row wrap>      
          <v-flex v-for="item in teams" :key="item.name" xs12 sm6 md7 lg4> 
            <v-hover v-slot="{ hover }">
          <v-card  
          class="mx-auto"
        max-width="344"
        variant="outlined">
        <p class="mb-4"></p>
            <v-expand-transition>
              <div v-if="hover"><v-btn color="primary text-center" href="/score" target="_blank">Результаты матчей </v-btn></div>
            </v-expand-transition>
            <v-responsive class="pt-5 text-center text-h4 black--text grey" >
              {{ item.name }}
            </v-responsive>
            <v-card-text>
              <div class="mb-1 text-h5 blue--text" >
            <img :src="item.crest" height="100"  /> Основана в {{ item.founded }}</div>
              <div class="text-h6 mb-1">Краткое название: {{ item.shortName }}</div>
            
            </v-card-text >
        
            <v-card-action>
              
              <v-btn
            class="ma-2"
            variant="text"
            color="red-lighten-2"
          > <div class="text-h7 mb-1" href to="(`{item.website}`)">Страница команды</div></v-btn>
            </v-card-action>
          </v-card>
          
        </v-hover>
          </v-flex>
        </v-layout>
      </v-container>
      </div>
      
      <div class="text-center">
        <v-pagination
            v-model="currentPage"
            :length="3"
            total-visible="7"
            
      color="purple"
            @input="handlePageChange"
          ></v-pagination>
        </div>
      </v-card>
    </v-card>
    </v-container>
    </div>
    </v-app>
    </template>
      
    <script>
    export default {
      name: 'Teams',
        data() {
        return {
          headers: [],
          currentPage: 1,
          search: '',
          teams: [
            { text: 'Герб', value: 'crest', align: 'center' },
            { text: 'Название лиги', value: 'name' },
            { text: 'Год основания', value: 'founded'},
            { text: 'Короткое название', value: 'shortName'},
            { text: 'Адрес', value: 'address'},
            { text: 'Веб-сайт', value: 'website'},
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
          this.$axios.$get('api/teams/').then((res) => {
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