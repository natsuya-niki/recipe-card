<template>
  <div class="samaple__conntents">
    <div style="margin-top: 20px">
      <h1>1週間の献立</h1>
    </div>
    <v-container class="grey lighten-5 mb-6">
      <v-row no-gutters>
        <v-col v-for="calendar in recipe_calendar" :key="calendar.date">
          <v-card class="pa-2" outlined tile> {{ calendar.date }} </v-card>
        </v-col>
      </v-row>
      <v-row no-gutters>
        <v-col v-for="calendar in recipe_calendar" :key="calendar.date">
          <v-card class="pa-1" outlined tile>
            <draggable
              v-model="calendar.recipes"
              :options="{ group: 'recipe' }"
            >
              <template v-for="recipe in calendar.recipes">
                <v-card
                  :key="recipe.id"
                  :loading="loading"
                  class="ma-1"
                  max-width="200"
                >
                  <template slot="progress">
                    <v-progress-linear
                      color="deep-purple"
                      height="10"
                      indeterminate
                    ></v-progress-linear>
                  </template>

                  <v-img
                    height="250"
                    src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
                  ></v-img>

                  <v-card-title>{{ recipe.title }}</v-card-title>

                  <v-card-text>
                    <v-row align="center" class="mx-0">
                      <v-rating
                        :value="4.5"
                        color="amber"
                        dense
                        half-increments
                        readonly
                        size="14"
                      ></v-rating>

                      <div class="grey--text ml-4">4.5 (413)</div>
                    </v-row>

                    <div class="my-4 subtitle-1">材料</div>

                    <div>{{ recipe.ingredient }}</div>
                  </v-card-text>

                  <v-divider class="mx-4"></v-divider>
                </v-card>
              </template>
            </draggable>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
    <div style="margin-top: 20px">
      <v-layout row wrap style="width: 100%; color: #dd0000">
        <v-flex v-for="elm in arrayList" :key="elm.id">
          <draggable
            v-model="arrayList"
            :options="{
              group: {
                name: 'recipe',
                pull: 'clone',
                put: false,
              },
              sort: false,
            }"
            :clone="handleClone"
          >
            <template>
              <v-card :loading="loading" class="ma-2" max-width="300">
                <template slot="progress">
                  <v-progress-linear
                    color="deep-purple"
                    height="10"
                    indeterminate
                  ></v-progress-linear>
                </template>

                <v-img
                  height="250"
                  src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
                ></v-img>

                <v-card-title>{{ elm.title }}</v-card-title>

                <v-card-text>
                  <v-row align="center" class="mx-0">
                    <v-rating
                      :value="4.5"
                      color="amber"
                      dense
                      half-increments
                      readonly
                      size="14"
                    ></v-rating>

                    <div class="grey--text ml-4">4.5 (413)</div>
                  </v-row>

                  <div class="my-4 subtitle-1">材料</div>

                  <div>{{ elm.ingredient }}</div>
                </v-card-text>

                <v-divider class="mx-4"></v-divider>
              </v-card>
            </template>
          </draggable>
        </v-flex>
      </v-layout>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  components: { draggable },
  data: () => ({
    loading: false,
    arrayList: [
      {
        id: 1,
        title: 'ラーメンの味噌煮',
        ingredient: '・チャルメラ<br />・そば',
      },
      {
        id: 2,
        title: '素麺の醤油煮',
        ingredient: '・チキンラーメン<br />・砂糖',
      },
      { id: 3, title: '焼きそばの塩麹炒め', ingredient: '・GooTa<br />・お湯' },
      {
        id: 4,
        title: '4焼きそばの塩麹炒め',
        ingredient: '・GooTa<br />・お湯',
      },
      {
        id: 5,
        title: '5焼きそばの塩麹炒め',
        ingredient: '・GooTa<br />・お湯',
      },
      {
        id: 6,
        title: '6焼きそばの塩麹炒め',
        ingredient: '・GooTa<br />・お湯',
      },
      {
        id: 7,
        title: '7焼きそばの塩麹炒め',
        ingredient: '・GooTa<br />・お湯',
      },
    ],
    recipe_calendar: [
      {
        date: '2021/02/15',
        recipes: [
          {
            id: 1,
            title: '登録済み',
            ingredient: 'そば',
          },
        ],
      },
      {
        date: '2021/02/16',
        recipes: [],
      },
      {
        date: '2021/02/17',
        recipes: [],
      },
      {
        date: '2021/02/18',
        recipes: [],
      },
      {
        date: '2021/02/19',
        recipes: [],
      },
      {
        date: '2021/02/20',
        recipes: [],
      },
      {
        date: '2021/02/21',
        recipes: [],
      },
    ],
  }),

  methods: {
    reserve() {
      this.loading = true

      setTimeout(() => (this.loading = false), 2000)
    },
    handleClone(item) {
      // Create a fresh copy of item
      const cloneMe = JSON.parse(JSON.stringify(item))

      console.log(cloneMe)
      console.log(item.id)

      this.$delete(cloneMe, item.id)

      return cloneMe
    },
  },
}
</script>
<style>
.samaple__conntents {
  margin: 0 auto;
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
