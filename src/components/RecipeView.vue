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
       <h2>Recipe</h2>
      </v-col>

      <v-col cols="6">
      <div v-if="ingredients.length > 0">
        <h3>Ingredients:</h3>
        <div class="py-1" v-for="(ingredient, index) in ingredients" v-bind:key="index">
          <h4>{{ingredient}}</h4>
        </div>
      </div>
      </v-col>
      <v-col cols="6">
      <div v-if="directions.length > 0">
        <h3>Directions:</h3>
        <div class="py-3" v-for="(direction, index) in directions" v-bind:key="index">
          <h4>{{direction}}</h4>
        </div>
      </div>
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
