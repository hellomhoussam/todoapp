<template>
    <li>
      <input type="checkbox" :value="todo.done" @change="onChnageTachCheck"/>
      <span :style="[todo.done ? {'text-decoration': 'line-through' } : {'text-decoration': 'none'}]">{{todo.libelle}}</span>
    </li>
</template>

<script>

export default {
  name: 'TacheComponent',
  props: ["todo", "index"],
  methods:{
    onChnageTachCheck: function(){
        this.$emit("onChnageTachCheck", this.index);
    }
  }
}


</script>

<style>

</style>
