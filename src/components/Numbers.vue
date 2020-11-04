<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">

      </v-col>
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          corona numbers
        </h1>
      </v-col>

    </v-row>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card
            class="mx-auto"
            max-width="344"
        >
          <v-card-text>
            <v-container>
              <v-row>
                <v-col>
                  <p class="display-1 text--primary">basel</p>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <p>confirmed cases</p>
                  <p style="font-size: large" class="font-weight-bold">{{ today.ncumul_conf }}(<span v-if="difference.confirmedCases === 0">{{ difference.confirmedCases }}</span><span v-if="difference.confirmedCases > 0" class="red--text">+{{ difference.confirmedCases }}</span>)</p>
                </v-col>
                <v-col>
                  <p>curent hospitalised</p>
                  <p style="font-size: large" class="font-weight-bold">{{ today.ncumul_hosp }}(<span v-if="difference.hospitalized < 0" class="green--text">-{{ difference.hospitalized }}</span><span v-if="difference.hospitalized > 0" class="red--text">+{{ difference.hospitalized }}</span>)</p>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <p>current in icu</p>
                  <p style="font-size: large" class="font-weight-bold">{{ today.ncumul_ICU }}(<span v-if="difference.currentICU < 0" class="green--text">-{{ difference.currentICU }}</span><span v-if="difference.currentICU > 0" class="red--text">+{{ difference.currentICU }}</span><span v-if="difference.currentICU === 0">0</span>)</p>
                </v-col>
                <v-col>
                  <p>deceased</p>
                  <p style="font-size: large" class="font-weight-bold">{{ today.ncumul_deceased }}(<span v-if="difference.deceased < 0" class="green--text">-{{ difference.deceased }}</span><span v-if="difference.deceased > 0" class="red--text">+{{ difference.deceased }}</span><span v-if="difference.deceased === 0">0</span>)</p>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <div class="font-weight-light grey--text">
              {{ today.date }}
            </div>

            <v-spacer></v-spacer>

            <v-btn
                text
                color="primary"
                :href="today.source"
            >
              quelle
            </v-btn>
          </v-card-actions>

        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import json from './data.json'

  export default {
    name: 'HelloWorld',

    data(){
      return{
        myJson: json,
        today: null,
        yesterday: null,
        difference: null,
        datum: null,
        confirmedCases: null,
        currentICU: null,
        deceased: null,
        hospitalized: null
      }
    },
    created() {
      this.today = json.data[json.data.length-1]
      this.yesterday = json.data[json.data.length-2]
      this.changeHelper(this.today, this.yesterday)
    },
    methods:  {
      changeHelper(newDate, oldDate) {
        this.difference = {
          "confirmedCases": newDate.ncumul_conf - oldDate.ncumul_conf,
          "hospitalized": newDate.ncumul_hosp - oldDate.ncumul_hosp,
          "currentICU": newDate.ncumul_ICU - oldDate.ncumul_ICU,
          "deceased": newDate.ncumul_deceased - oldDate.ncumul_deceased
        }
      }
  }
  }
</script>
