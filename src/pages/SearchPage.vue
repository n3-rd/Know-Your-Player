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
        v-on:keyup.enter="searchPlayer"
      />

      <div class="container">
        <div class="row">
          <div
            v-for="player in players"
            :key="player.idPlayer"
            class="players q-pa-md q-mt-md col-xs-12 col-lg-4 col-xl-3 col-md-6 col-sm-12"
            rounded
          >
            <q-card class="my-card">
              <div v-if="player.strCutout">
                <q-img :src="player.strCutout">
                  <div class="absolute-bottom text-h6 player-name">
                    {{ player.strPlayer }}
                  </div>
                </q-img>
              </div>

              <div v-if="!player.strCutout">
                <q-img :src="player.strThumb">
                  <div class="absolute-bottom text-h6 player-name">
                    {{ player.strPlayer }}
                  </div>
                </q-img>
              </div>

              <q-popup-proxy>
                <div class="full-width">
                  <q-banner>
                    <template v-slot:avatar>
                      <q-card class="my-card">
                        <q-img :src="player.strThumb">
                          <div class="absolute-bottom text-h6 player-name">
                            {{ player.strPlayer }}
                          </div>
                        </q-img>

                        <q-card-section class="poppins-medium">
                          <div class="row">
                            <div class="col-xs-6">
                              <b>Sport:</b> {{ player.strSport }} <br />
                            </div>
                            <div class="col-xs-6">
                              <b>Position:</b> {{ player.strPosition }} <br />
                            </div>
                            <div class="col-xs-6">
                              <b>Club:</b> {{ player.strTeam }} <br />
                            </div>
                            <div class="col-xs-6">
                              <b>Born:</b> {{ player.dateBorn }} <br />
                            </div>
                            <div class="col-xs-6">
                              <b>Nationality:</b> {{ player.strNationality }}
                              <br />
                            </div>
                            <div class="col-xs-6">
                              <b>Gender:</b> {{ player.strGender }} <br />
                            </div>
                            <div class="col-xs-6">
                              <b>Height:</b> {{ player.strHeight }} <br />
                            </div>
                          </div>

                          <q-expansion-item
                            expand-separator
                            icon="about"
                            label="about"
                          >
                            <q-card>
                              <q-card-section>
                                {{ player.strDescriptionEN }}
                              </q-card-section>
                            </q-card>
                          </q-expansion-item>
                        </q-card-section>
                      </q-card>
                    </template>
                  </q-banner>
                </div>
              </q-popup-proxy>

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
  </div>
</template>

<script>
export default {
  name: "SearchPage",
  data() {
    return {
      text: "",
      players: [],
      playerPopup: false,
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

<style lang="scss">
.my-card {
  width: 80vw;
}
</style>
