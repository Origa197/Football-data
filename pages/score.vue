  <!-- eslint-disable vue/no-duplicate-attributes -->
    <!-- eslint-disable no-console -->
    <template >
      <div> 
      <v-data-table
        :headers="headers"
        :item="matches"
        :items="filteredMatches"
        class="elevation-10"
      >
      <template #top>
          <v-menu ref="menu" v-model="showMenu">
            <template #activator="{ on, attrs }">
              <v-text-field
                v-model="date"
                clearable
                label="Выберите диапазон дат"
                prepend-icon="mdi-calendar"
                readonly
                v-bind="attrs"
                v-on="on"
              ></v-text-field>
            </template>
            <v-date-picker v-model="dates" class="mt-4" range> </v-date-picker>
          </v-menu>
        </template>
        
        <template #[`item.home`]="{ item }" >
          {{ item.score.fullTime.home }}
        </template>
        <template #[`item.away`]="{ item }">
          {{ item.score.fullTime.away }}
        </template>
        <template #[`item.shortName`]="{ item }">
          {{ item.homeTeam.shortName }}
        </template>
        <template #[`item.name`]="{ item }">
          {{ item.awayTeam.name }}
        </template>
        <template #[`item.endDate`]="{ item }">
          {{ item.currentSeason.endDate | formatDate }}
        </template>

        <template #[`item.crest`]="{ item }">
          <img :src="item.homeTeam.crest" height="150" />
          <img :src="item.awayTeam.crest" height="150" />
        </template>
        
      </v-data-table>
      <div class="text-center">
    
      </div>
    </div>
    
  </template>
  <script>
  export default {
    
    name: 'Competitions',
  filters: {
    formatDate: (d) => {
      const date = new Date(d)
      const options = { year: 'numeric', month: 'numeric', day: 'numeric' }
      return date.toLocaleString('ru-RU', options)
    },
  },
    
    data() {
      
      return {
        page: 1,
        matches: [],
        showMenu: false,
        headers: [
          { text: 'Дата и время начала', value: 'utcDate', align: 'center'},
          { text: 'Команда А', value: 'shortName', align: 'center' },         
          { text: 'Счет команда А', value: 'home', align: 'center'},              
          { text: 'Герб', value: 'crest', align: 'center'},        
          { text: 'Счет команды Б', value: 'away', align: 'center'}, 
          { text: 'Команда Б', value: 'name', align: 'center' },              
          { text: 'Статус', value: 'status', align: 'center'},  
        ],
      }
    },
    computed:{
      filteredMatches() {
        return this.date ? this.matches.filter(comp => {
      console.log(comp);
      return new Date(comp.currentSeason?.startDate) > new Date(this.date) 
        }) : this.matches;
        }
      
    },
    mounted() {
      this.getData()
    },
    methods: {
      getData() {
        console.log('GetData')
        this.$axios.$get('api/competitions/2016/matches').then((res) => {
          "X-Unfold-Goals: true"
          console.log(res)
          this.matches = res.matches
        })
      },
    }
  }
  </script>
