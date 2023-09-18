<!-- eslint-disable no-console -->
<template>
  <div>
    <v-data-table 
      :headers="headers"
      :items="filteredCompetitions"
      :items-per-page="15"
      class="elevation-4"
    >
      <template #top>
        <v-menu ref="menu" v-model="showMenu">
          <template #activator="{ on, attrs }">
            <v-text-field
              v-model="date"
              clearable
              label="Выберите дату начала"
              readonly
              v-bind="attrs"
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" class="mt-4"></v-date-picker>
        </v-menu>
      </template>
      <template #[`item.startDate`]="{ item }">
        {{ item.currentSeason.startDate | formatDate }}
      </template>

      <template #[`item.endDate`]="{ item }">
        {{ item.currentSeason.endDate | formatDate }}
      </template>

      <template #[`item.emblem`]="{ item }">
        <img :src="item.emblem" height="100" />
      </template>
    </v-data-table>
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
      competitions: [],
      score: [],
      date: '',
      showMenu: false,
      headers: [
        { text: 'Название лиги', value: 'name' },
        { text: 'Код лиги', value: 'code', align: 'center' },
        { text: 'Дата начала', value: 'startDate', align: 'center' },
        { text: 'Дата окончания', value: 'endDate', align: 'center' },
        { text: 'Флаг', value: 'emblem', align: 'center' },
        { text: 'Тип', value: 'type', align: 'center' },
      ],
    }
  },
  computed:{
    filteredCompetitions() {
      return this.date ? this.competitions.filter(comp => {
     console.log(comp);
     return new Date(comp.currentSeason?.startDate) > new Date(this.date)
       }) : this.competitions;
      }
    },
    
  mounted() {
    this.getData()
  },
  methods: {
    getData() {
      console.log('GetData')
      this.$axios.$get('api/competitions').then((res) => {
        this.competitions = res.competitions
      })
    },
  },
}
</script>