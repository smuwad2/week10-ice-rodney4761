<script>
    // Import BlogPost component
    import BlogPost from './subcomponents/BlogPost2.vue';

  import axios from 'axios'
    export default {
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname=='localhost')
                    return 'http://localhost:3000' 
                else {
                    const codespace_host = window.location.hostname.replace('5173', '3000')
                    return `https://${codespace_host}`;
                }
            }
        },
        
        created() { // created is a hook that executes as soon as Vue instance is created
            axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
        },
        methods: {
            deletePost(id) {
                axios.get(`${this.baseUrl}/deletePost`, {
                    params: {
                        id: id
                    }
                })
                .then(response => {
                    // this gets the data, which is an array
                    console.log(response.data)
                    this.posts = this.posts.filter(post=>post.id!=id)
                })
                .catch(error => {
                    console.error(error)
                })
                
            }
        },
        components: {
            BlogPost
        }   
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <BlogPost v-for="post in posts"
    :entry=post.entry
    :subject=post.subject
    :mood=post.mood
    :key=post.id>
        <button class="btn btn-primary" @click="deletePost(post.id)">Delete</button>
    </BlogPost>
</template>
