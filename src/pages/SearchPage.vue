<template>
  <div>
    <div class="q-pa-md">
      <q-input
        rounded
        outlined
        v-model="text"
        label="Player Name"
        color="brand"
        dark
      />

      <q-btn
        unelevated
        rounded
        color="brand"
        label="Search Player"
        class="full-width q-mt-md q-pa-md"
        @click="searchPlayer"
      />

      <div class="row">
        <div
          v-for="player in players"
          :key="player.idPlayer"
          class="players full-width q-pa-md q-mt-md col-sm-12 col-lg-4 col-xl-3 col-md-6"
          rounded
        >
          <q-card class="my-card">
            <q-img :src="player.strThumb">
              <div class="absolute-bottom text-h6 player-name">
                {{ player.strPlayer }}
              </div>
            </q-img>

            <q-card-section class="poppins-medium">
              Position: {{ player.strPosition }} <br />
              Club: {{ player.strTeam }} <br />
              Born: {{ player.dateBorn }} <br />
            </q-card-section>
          </q-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchPage",
  data() {
    return {
      text: "",
      players: [],
    };
  },
  methods: {
    searchPlayer() {
      console.log(this.text);
      fetch(
        `https://www.thesportsdb.com/api/v1/json/2/searchplayers.php?p=${this.text}`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          this.players = data.player;
        });
    },
  },
};
</script>
