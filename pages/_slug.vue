<template>
        <div class="TitleContainer">
                <div class="single-content">
                        <h1 class="text-center" style="color: brown;">{{ title }}</h1>
                        <span>Ngày đăng: {{ date }}</span>
                        <hr>
                        <div class="single-content" v-html="content"></div>
                </div>
        </div>
</template>

<script>
const axios = require('axios')
export default {
        name: 'IndexPage',
        data() {
                return {
                        postList: null,
                        title: "",
                        date: "",
                        content: "",
                };
        },
        mounted() {
                this.getPost(this.$route.params.slug); // đoạn route khớp với phân đoạn thì giá trị được hiển thị bởi params.slug
        },
        methods: {
                async getPost(slug) {
                        try {
                                const response = await axios.get('http://localhost:8000/api/v1/users/' + slug);
                                const postData = response.data.data;

                                // Kiểm tra nếu có ít nhất một phần tử trong mảng
                                if (postData.length > 0) {
                                        const post = postData[0];
                                        this.title = post.title;
                                        this.date= post.date;
                                        this.content = post.content;
                                }
                                console.log(this.$route.params.slug);
                        } catch (error) {
                                console.error(error);
                        }
                },
        },
};
</script>

<style>
.TitleContainer {
        padding: 5rem 0px;
}
</style>