 <template>
        <div class="container">
            <h1>
                {{ listPost.title }}
            </h1>
            <p>
                {{  listPost.date }}
            </p>
            <p>
                {{ listPost.content_full }}
            </p>
            <p>
                {{ $route.params.id }}
            </p>
        </div>
</template>

<script>
export default {
    name: 'IndexPage',
    data() {
        return {
            detailPost: {
            "title": "",
            "content_full": "",
            "date":"" 
            }
           
        };
    },
    mounted() {
        this.getPost(this.$route.params.id);
    },
    methods: {
        async getPost(slug) {
            try {
                const axios = await import('axios');
                const response = await axios.get('http://localhost:8000/api/v1/users' + id);
                this.detailPost = response.data.data;
                console.log(this.$route.params.slug);
            } catch (error) {
                console.error(error);
            }
        },
    },
};
</script>
<style>
.cent {
    text-align: center;
    margin: 30px 0px;
}

h1 {
    font-weight: bold;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}</style>


<!-- 
 mounted() {
        this.getPost(this.$route.params.id);
    }, -->