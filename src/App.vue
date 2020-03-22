<template>
  <v-app>
    <v-content>
      <v-container>
        <v-card>
          <v-card-title>
            Covid-19
            <v-spacer></v-spacer>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
          </v-card-title>
          <v-data-table
            :loading="!loaded"
            :loading-text="'Fetching data, please wait...'"
            :headers="headers"
            :items="items"
            :fixed-header="fixedHeader"
            :items-per-page="10"
            :search="search"
          ></v-data-table>
        </v-card>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      search: "",
      fixedHeader: true,
      loaded: false,
      headers: [
        {
          text: "Country",
          value: "country"
        },
        {
          text: "Cases",
          value: "cases"
        },
        {
          text: "Today Cases",
          value: "todayCases"
        },
        {
          text: "Deaths",
          value: "deaths"
        },
        {
          text: "Today Deaths",
          value: "todayDeaths"
        },
        {
          text: "Recovered",
          value: "recovered"
        },
        {
          text: "Critical",
          value: "critical"
        }
      ],
      items: []
    };
  },
  async mounted() {
    const { data } = await this.axios.get(
      "https://corona.lmao.ninja/countries/"
    );
    console.log(data);
    this.items = data;
    this.loaded=true
  }
};
</script>
