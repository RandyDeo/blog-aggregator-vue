<template>
  <div class="app" :class="mode">

    <v-row>
      <v-col cols="2"></v-col>
      <v-col cols="2"><h3>Dark Mode</h3></v-col>
      <v-col cols="1"><Toggle :mode="mode" @toggle="toggle" /></v-col>
            
    </v-row>

    <v-row>
      <v-col cols="8" sm="12" md="8">
        <Post :post="post" v-for="post in posts" :key="post.id"/>
      </v-col>
      <v-col cols="4" sm="12" md="4">
        <v-subheader>Recommended Topics</v-subheader>
        <CategoryList :categories="categories" />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import Post from '../components/Post'
import Toggle from '/components/DarkToggle'

export default {
  components: { 
      Post,
      Toggle 
  },
  methods: {
    toggle () {
      if (this.mode === "dark"){
        this.mode = "light" 
      } else {
        this.mode = "dark"
      }
    }
  },
  computed: {
    posts() {
      return  this.$store.state.posts.list;
    },
    categories() {
      return this.$store.state.categories.list;
    }
  },
  created () {
    this.$store.dispatch('posts/loadPosts');
    this.$store.dispatch('categories/loadCategories');
  },
  data () {
    return {
      mode: 'light'
    }
  }
}
</script>

<style>

.app {
  background : #f3f3f3;
  color : #15202B;
  transition: background 0.3s ease-in-out;
}

.dark {
  background : #192734;
  color : #f3f3f3;
}

</style>