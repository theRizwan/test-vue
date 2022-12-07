<template>
  <div id="app">
    <v-app id="inspire">
      <v-container fluid>
        <v-row align="center">
          <v-col class="d-flex" cols="12" sm="6">
            <v-select v-model="venue" :items="venues" label="Venue (optional)" solo dense>
              <template #append-item>
                <div class="append">
                  <v-btn class="btn" @click.stop="dialog = true"><img class="image" v-bind:src="addImage" />Add
                    Venue</v-btn>
                </div>
              </template>
            </v-select>
          </v-col>
        </v-row>
        <v-dialog v-model="dialog" max-width="400">
          <v-card>
            <v-card-title class="text-h5">
              Add Venue
            </v-card-title>

            <v-card-text>
              <v-text-field v-model="newVenue" label="Enter Venue Name*" required :error="error"></v-text-field>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="dialog = false">
                Cancel
              </v-btn>

              <v-btn type="submit" color="green darken-1" text @click="addVenue">
                Submit
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-container>
    </v-app>
  </div>
</template>

<script lang='ts'>
import { defineComponent } from 'vue'


export default defineComponent({
  name: 'HelloWorld',

  data() {
    return {
      venues: ['SPA1', 'SPA2', 'SPA3'],
      addImage: require("../assets/add.png"),
      dialog: false,
      venue: '',
      newVenue: '',
      error: false,
    }
  },
  methods: {
    addVenue(e: any) {
      if (this.venues.includes(this.newVenue)) {
        this.error = true
      } else if (this.newVenue.trim()) {
        e.preventDefault();
        console.log(this.newVenue)
        this.venue = this.newVenue
        this.venues.push(this.newVenue)
        this.dialog = false
        this.error = false
      } else {
        this.error = true
      }
    }
  },
})
</script>
<style>
.image {
  height: 20px;
  width: 20px;
}

.btn {
  border: 2px solid white;
}
</style>