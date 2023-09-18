  <template>
  <div>
      <v-card v-for="[name, cls] in classes" :key="name" class="my-4">
        <div :class="[cls, 'pa-2']"  >{{ name }}</div>
        <div class="text-caption pa-2 bg-grey-lighten-4">
          <div class="text-grey">Актуальные новости только у нас</div>
          <div class="font-weight-medium"></div>
        </div>
        <div class="buttons">
        <v-btn href="/team">Команды</v-btn>
        <v-btn tag="a" href="/competitions" >Соревнования</v-btn>
      </div>
      </v-card>
      <v-carousel>
    <v-carousel-item
      src="https://sportishka.com/uploads/posts/2022-08/1660140895_39-sportishka-com-p-oboi-futbolnoe-pole-sport-krasivo-foto-46.jpg"
      cover
    ></v-carousel-item>

    <v-carousel-item
      src="https://i.pinimg.com/originals/98/34/66/983466ddf30a88bf189b1efa13c335f7.jpg"
      cover
    >
  </v-carousel-item>
    <v-carousel-item
      src="https://pngimg.com/uploads/football_player/football_player_PNG128.png"
      cover
    >
  </v-carousel-item>
  </v-carousel>
    </div>
  </template>
  <script>
  export default {
    name: 'IndexPage',data: () => ({
        classes: [
          ['Добро пожаловать на сайт футбольной статистики', 'text-h1'],

        ],
      }),
    }
  </script>
  <style scoped>
  .my-4 {
    background: url('../static/1234.png');
    background-size: center;
    height: 30vh;
  }
  </style>