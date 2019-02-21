<template>
  <div id="show-blogs" v-theme:column="'narrow'">
    <h1>博客总览</h1>
    <input type="text" placeholder="搜索" v-model="search">
    <div class="single-blog" v-for="(blog,index) in filteredBlogs" :key="index">
      <router-link :to="'/blog/' + blog.id">
        <h2 v-rainbow >{{blog.title | to-uppercase}}</h2>
      </router-link>
      <article>{{blog.content | snippet}}</article>
    </div>
  </div>
</template>
<script>
export default {
  name: "show-blogs",
  data() {
    return {
      blogs: [],
      search: ""
    };
  },
  created() {
    this.$http
    //   .get("http://jsonplaceholder.typicode.com/posts")
      .get("https://wd0238021847vitqyb.wilddogio.com/posts.json")
      .then(function(data) {
        return data.json();
        // this.blogs = data.body.slice(0, 10);
      })
      .then(function(data) {
        var blogsArray = [];
        for(var key in data) {
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
        // console.log(this.blogs)
      });
  },
  computed: {
    filteredBlogs: function() {
      return this.blogs.filter((blog) => {
        return blog.title.match(this.search);
      })
    }
  },
  filters: {
    // "to-uppercase": function(value) {
    //   return value.toUpperCase();
    // }
    toUppercase(value) {
      return value.toUpperCase();
    }
  },
  directives: {
    'rainbow': {
      bind(el, binding, vnode) {
        el.style.color = "#" + Math.random().toString(16).slice(2, 8);
      }
    }
  }
};
</script>
<style scoped>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}

.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
  border: 1px dotted #aaa;
}

#show-blogs a {
  color: #444;
  text-decoration: none;
}

input[type="text"] {
  padding: 8px;
  width: 100px;
  
}
</style>
