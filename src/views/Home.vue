<template>
  <div class="home">
    <v-layout>
      <v-flex xs12>
        <v-card>
          <v-row>
            <v-date-picker v-model="date" full-width></v-date-picker>
          </v-row>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-sm-center">
            650 - {{ date }}
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "home",
  components: {},
  data() {
    return {
      date: ""
    };
  }
};
</script>
