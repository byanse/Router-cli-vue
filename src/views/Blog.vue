<template>
  <Titulo texto="Titulo de mi blog" />
  <!-- <button @click="consumirApi">Consumir Api</button> -->
  <div v-for="item in arrayBlog" :key="item.id">
    <router-link :to="`/blog/${item.id}`">
      {{ item.title }}
    </router-link>
  </div>
</template>

<script>
import Titulo from '../components/Titulo';

export default {
  components: {
    Titulo,
  },
  data() {
    return {
      arrayBlog: [],
    };
  },
  methods: {
    async consumirApi() {
      try {
        const data = await fetch('https://jsonplaceholder.typicode.com/posts');
        const array = await data.json();
        console.log(array);
        this.arrayBlog = array;
      } catch (error) {
        console.log(error);
      }
    },
  },
  /* recibe una funcion directamente, se ejecuta antes de que se pinte el template */
  created() {
    this.consumirApi();
  },
};
</script>

<style></style>
