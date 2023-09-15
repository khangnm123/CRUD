<template>
        <div class="container">
                <h1 >About me</h1>
                <div class="wallper" v-if="index < userData.length" v-for="(item , index) in commentsToShow" :key="index">
                    <b-card
                     :title="userData[index].title"
                    :img-src="userData[index].image"
                   
                    img-alt="Image"
                    img-top
                    tag="article"
                    style="width: 100%;"
                    class="mb-2">
        <b-card-text>
          <p>{{ userData[index].content }}</p>
 
        </b-card-text>

        <b-button :href="'/' + userData[index].slug" class="btn" variant="outline-primary">Go somewhere</b-button>
      </b-card>
                </div>
                 <div v-if="commentsToShow < userData.length || userData.length > commentsToShow"> <!-- nếu 0 < chiều dài của mảng Userdata thì += 2 -->
        <button class="btn btn-primary" @click="commentsToShow += 2">show more reviews</button>
      </div>
        </div>
</template>

<style>
h1{
    text-align: center; 
font-weight: bold; 
font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
margin: 30px 0px;
}

</style>
<script>
const axios = require('axios');
import blog from '../../components/AddBlog/blog.vue';
export default {
    
    name: 'IndexPage',
    components: {
        blog
    },

    data() {
        return {
            blognew:'',
            search:'',
            userData: [],
            commentsToShow: 3, // xuất ra 3 phần tử
            totalComments: 0 // tổng là 0
        };
    },
    created() {
        this.getPost();
    },
    methods: {
        async getPost() {
            try {
                const response = await axios.get('http://localhost:8000/api/v1/users');
                this.userData = response.data.data;
                console.log(response.data.data);
            } catch (error) {
                console.error(error);
            }
        },
    },
      mounted() {
        this.totalComments = this.userData.length //duyệt chiều dài của mảng
        console.log(this.userData.length)
    }
};
</script>