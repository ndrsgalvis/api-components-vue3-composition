<script setup>
import { ref, computed, onMounted } from "vue";

import BlogPost from "./components/BlogPost.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./LoadingSpinner.vue";

  const posts = ref([]);
  const postXpage = 3;
  const start = ref(0);
  const end = ref(postXpage);
  const loading = ref(true);
  
  const favorito = ref('')
  const cambiarFavorito = (title) => {
    favorito.value = title
  }

  const next = () => {
    start.value = start.value + postXpage
    end.value = end.value + postXpage
  }
  const before = () => {
    start.value +=  - postXpage
    end.value += - postXpage
  }

  // onMounted(async()=>{
  //   try {
  //     const res = await fetch("https://jsonplaceholder.typicode.com/posts")
  //     posts.value = await res.json()
  //   } catch (error) {
  //     console.log(error)
  //   } finally{
  //     setTimeout(()=> {
  //       loading.value = false
  //     }, 1600)
  //   }
  // })

  // fetch("https://jsonplaceholder.typicode.com/posts")
  //   .then((res) => res.json())
  //   .then((data) => {
  //     posts.value = data
  //   })
  //   .catch((e)=> console.log(e))
  //   .finally( ()=> {
  //     setTimeout(()=> {
  //       loading.value = false
  //     }, 1600)
  //   });
    
  // forma correcta de hacerlo
    const fetchData = async() => {
      try {
      const res = await fetch("https://jsonplaceholder.typicode.com/posts")
      posts.value = await res.json()
      } catch (error) {
        console.log(error)
      } finally{
        setTimeout(()=> {
          loading.value = false
        }, 1600)
      }
    }

    fetchData()

  const maxLength = computed( ()=> posts.value.length)

</script>
<template>
  <LoadingSpinner v-if="loading"/>
  <div class="container" v-else>
    <h1> APP </h1>  
    <h3> Mi post favorito: {{favorito}} </h3> 
    <PaginatePost
      @next="next"
      @before="before"
      :start="start" 
      :end="end"
      :maxLength="maxLength"
      />
    <BlogPost
      v-for = "post in posts.slice(start, end)"
        :key="post.id"
        :id="post.id"
        :title="post.title"
        :body="post.body"
        :colorText="success"
        @cambiarFavorito="cambiarFavorito"
        />
  </div>
</template> 