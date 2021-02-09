<template>
  <div class="samaple__conntents">
    <div style="margin-top: 20px">
      <h1>1週間の献立</h1>
    </div>
    <div style="margin-top: 20px">
      <div style="width: 50%; margin-left: 25%; color: #dd0000">
        <draggable v-model="arrayList">
          <div v-for="elm in arrayList" :key="elm.id">
            <template>
              <v-card :loading="loading" class="mx-auto my-12" max-width="300">
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
          </div>
        </draggable>
      </div>
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
    ],
  }),

  methods: {
    reserve() {
      this.loading = true

      setTimeout(() => (this.loading = false), 2000)
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
