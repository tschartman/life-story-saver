<template>
  <v-app>
    <v-content>
      <RecipeView @scrapeWeb="scrapeWeb" :ingredients="ingredients" :directions="directions" />
    </v-content>
  </v-app>
</template>

<script>
import RecipeView from './components/RecipeView';
import axios from 'axios';
export default {
  name: 'App',

  components: {
    RecipeView,
  },

  data: () => ({
    ingredients: [],
    directions: []
  }),
  methods: {
    async scrapeWeb(url){
      const webData = await axios.post("https://recipe-parser-api.herokuapp.com/recipe", {url: url});
      if(webData.status === 200){
        this.ingredients = webData.data.ingredients;
        this.directions = webData.data.directions;
      }
      console.log(this.ingredients)
    }
  }
};
</script>
