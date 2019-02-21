<template>
    <div id="single-blog">
        <h1>
            {{blog.title}}
        </h1>
        <article>
            {{blog.content}}
        </article>
        <p>作者: {{blog.author}}</p>
        <p>分类：</p>
        <ul>
            <li v-for="category in blog.categories" :key="category">
                {{category}}
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    name: 'single-blog',
    data() {
        return {
            id: this.$route.params.id,
            blog: {}
        }
    },
    created() {
        // this.$http.get("../../static/post.json")
        this.$http.get("https://wd0238021847vitqyb.wilddogio.com/posts/" + this.id + ".json")
        .then(function(data) {
            // console.log(data)
            return data.json();
            // for(var i = 0; i < data.body.length; i++) {
            //     if(data.body[i].id == this.id) {
            //         this.blog = data.body[i];
            //         break;
            //     }
            // }
        })
        .then(function(data) {
            this.blog = data;
        })
    },
}
</script>
<style scoped>
    #single-blog {
        max-width: 960px;
        margin: 0 auto;
        padding: 20px;
        background: #eee;
        border: 1px dotted #aaa;
    }
</style>