<template>
  <div class="home">
    <v-layout>
      <v-flex xs12>
        <v-card>
          <v-row>
            <v-date-picker
              v-model="date"
              full-width
              locale="es-cl"
              :min="min"
              :max="max"
              @change="getDollar(date)"
            ></v-date-picker>
          </v-row>
        </v-card>
        <v-card color="error" dark>
          <v-card-text class="display-1 text-sm-center"
            >{{ valor }}
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import { mapMutations } from "vuex";

var moment = require("moment");

export default {
  name: "home",
  components: {},
  data() {
    return {
      date: new Date().toISOString().substr(0, 10),
      min: "1984",
      max: new Date().toISOString().substr(0, 10),
      valor: null
    };
  },
  methods: {
    //SE SEPARA CON COMA
    ...mapMutations(["showLoader", "hideLoader"]),
    //SE SEPARA METODOS CON COMAS
    async getDollar(day) {
      let formatDate = moment(day).format("DD-MM-YYYY");

      try {
        //INICIAR LOADER
        this.showLoader({
          titulo: "Accediendo a información",
          color: "secondary"
        });

        let data = await axios.get(
          `https://mindicador.cl/api/dolar/${formatDate}`
        );
        console.log(data.data);

        if (data.data.serie.length > 0) {
          this.valor = await data.data.serie[0].valor;
        } else {
          this.valor = "Sin resultados";
        }

        //OCULTAR LOADER
        this.hideLoader();
      } catch (error) {
        console.log(error);
      }
    }
  },
  created() {
    this.getDollar(this.date);
  }
};
</script>
