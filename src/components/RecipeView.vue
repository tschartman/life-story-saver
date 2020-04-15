<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
       <h2>Skip the life story...</h2>
      </v-col>
      <v-col cols="12" class="mx-auto">
        <v-form
          ref="form"
          v-model="valid"
        >
          <v-text-field
            v-model="url"
            label="Recipe Url"
            :rules="urlRules"
            required
          ></v-text-field>
          <v-btn :disabled="!url" @click="submit">get the</v-btn>
        </v-form>
      </v-col>
      <v-col cols="12">
       <h2 class="display-1">Recipe</h2>
      </v-col>
      <v-col cols="12" sm="6">
        <h3 v-if="ingredients.length > 0" class="headline">Ingredients:</h3>
        <v-container style="max-height: 600px;overflow-y-auto"
        class="hide overflow-y-auto">
          <div class="py-1" v-for="(ingredient, index) in ingredients" v-bind:key="index">
            <h4>{{ingredient}}</h4>
          </div>
        </v-container>
        </v-col>
        <v-col style="max-height: 600px;"
        class="hide overflow-y-auto" cols="12" sm="6">
          <h3 v-if="directions.length > 0" class="headline">Directions:</h3>
          <v-container style="max-height: 600px;overflow-y-auto"
          class="hide overflow-y-auto">
          <div class="py-3" v-for="(direction, index) in directions" v-bind:key="index">
            <h4>{{direction}}</h4>
          </div>
          </v-container>
        </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      ingredients: Array,
      directions: Array,
      method: Function
    },
    data: () => ({
     valid: true,
     url: "",
     urlRules: [
       v => !!v || 'Url is required',
     ],
    }),
    methods: {
      submit(){
        this.$emit('scrapeWeb', this.url)
      }
    }
  }
</script>
<style scoped>
.hide::-webkit-scrollbar {
  display: none;
}

/* Hide scrollbar for IE and Edge */
.hide {
  -ms-overflow-style: none;
}
</style>