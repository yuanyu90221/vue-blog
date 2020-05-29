<template>
  <div class="home">
    <article v-for="art in articles" :key="art.id">
      <h3>{{art.title}}</h3>
       <i>{{ art.date }}</i>
       <span>{{art.content | subContent}}</span>
    </article>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
export default {
  name: 'Home',
  mounted () {
    const api = `https://us-central1-expressapi-8c039.cloudfunctions.net/app/article`;
    axios.get(api)
      .then(result=>{
        this.articles = result.data.data
      })
  },
  data( ) {
    return {
      articles: null
    }
  },
  filters: {
    subContent: (content) => {
      return content.substring(0, 150)
    }
  }
}
</script>
<style lang="scss" scoped>
  article {
    display: flex;
    padding-left: 2rem;
    justify-content: center;
    margin: 1rem;
    background-color: #dddddd;
    border-radius: 16px;
    flex-direction: column;
    align-items: flex-start;
    width: 80vw;
    height: 200px;
    i {
      color: #cccccc;
    }
  }
</style>