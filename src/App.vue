<template>
  <div>
    <input type="text" v-model="newTache"/>
    <button @click="ajouterUneTach">Ajouter</button>
  </div> 
  <div>
    <label v-for="option in options" :key="option.id">
      <input type="radio" :value="option.id" v-model="picked" />
      <span>{{ option.name }}</span>
    </label>
  </div> 
  <ul>
    <TacheComponent v-for="(todo, index) in getTodos()" :key="index" :todo="todo" :index="index" @onChnageTachCheck="onChnageTachCheck" />
  </ul>
</template>

<script>
import TacheComponent from './components/TacheComponent.vue';
export default {
  name: 'App',
  components: {TacheComponent},
   methods: {
    ajouterUneTach() {
      if(this.newTache.length > 0){
        let idNewTach = this.todos.length + 1;
        this.todos.push({
          id:idNewTach,
          libelle: this.newTache,
          done:false
        })
        this.newTache = "";
      }
    },
    onChnageTachCheck: function(index){
      let currentTache = this.todos[index];
      this.todos[index].done = !currentTache.done;
    },
    getTodos: function(){
      let filtredList = this.todos.filter(e => e.done);
      return this.picked == 1 ? this.todos : filtredList;
    }
  },
  data(){
    return {
      picked: 1,
      options: [
        { 
          id:0,
          name: 'Les taches finies' 
        }, 
        { 
          id:1,
          name: 'Toutes les taches' 
        }
      ],
      newTache : "",
      todos : [
        {
          id:1,
          libelle:"Do something awesome!",
          done:false
        },
        {
          id:2,
          libelle:"Learn vue.js",
          done:false
        },
      ]
    }
  }
}
</script>

<style>
label {
  display: block;
}
</style>
