<template>
  <div id="app">
    <form @submit.prevent="addBlog" style="display: flex; flex-direction: column; width: 350px;">
      <input type="text" name="title" v-model="title" placeholder="title">
      <input type="text" name="author" v-model="author" placeholder="author">
      <select name="label" id="label" v-model="label">
        <option value="math">Math</option>
        <option value="science">Science</option>
        <option value="programming">Programming</option>
      </select>
      <button type="submit">Submit</button>
    </form>

    <div style="margin-top: 15px;">
      <select name="filter" id="filter" v-model="filterBlog">
        <option value="" selected="selected" disabled>Filter Data</option>
        <option value="math">Math</option>
        <option value="science">Science</option>
        <option value="programming">Programming</option>
      </select>
      <button @click="clearFilter">clear filter</button>
      <div style="margin-top: 5px; background: salmon; width: 350px;" :key="blog.author" v-for="blog in sortedBlogs">
        <h5>{{ blog.title }}</h5>
        <p>@{{ blog.author }}</p>
        <span>label: {{ blog.label }}</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      blogs: [
        {
          title: 'ujang babad',
          author: 'asep saepudin',
          label: 'math'
        },
        {
          title: 'preman pensiun',
          author: 'budi',
          label: 'science'
        },
        {
          title: 'nisekoi',
          author: 'gorilla',
          label: 'programming'
        },
        {
          title: 'unit test',
          author: 'jest',
          label: 'programming'
        },
      ],
      title: '',
      author: '',
      label: '',
      filterBlog: '',
    }
  },
  methods: {
    addBlog(){
      this.blogs.push({
        title: this.title,
        author: this.author,
        label: this.label
      })
      console.log(this.blogs)
      this.title = '',
      this.author = '',
      this.label = ''
    },
    clearFilter(){
      this.filterBlog = ''
    }
  },
  computed: {
    sortedBlogs(){
      if(this.filterBlog){
        return this.blogs.filter(data => data.label.match(this.filterBlog))
      }else{
        return this.blogs
      }
    }
  }
}
</script>
