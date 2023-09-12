<template>
  <!-- <div class="#">
    <div v-if="userData.length > 0">
      <div v-for="user in userData" :key="user.userId">
        <h1>{{ user.userId }}</h1>
        <p>{{ user.userName }}</p>
        <p>{{ user.dateofBirthday }}</p>
        <p>{{ user.Address }}</p>
      </div>
    </div>
    <div v-else>
      <p>Đang tải dữ liệu...</p>
    </div>
  </div> -->
  <div class="container">
    <div class="cent"><h1>Page Blog</h1></div>
      <div v-if="userData.length >0 ">
        <b-card no-body class="overflow-hidden mb"  v-for="(item , index) in userData" :key="index.id" >
      <b-row no-gutters>
        <b-col md="2">
          <NuxtLink :to="'/' + item.id"> <b-card-img :src=" item.image" alt="Image" class="thumbnail-list"></b-card-img></NuxtLink>
         
        </b-col>
        <b-col md="10">
          <b-card-body :title="item.title">
            <b-card-text>
                {{ item.content}}
            </b-card-text>
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
      </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      userData: []
    };
  },
  created() {
    this.getPost();
  },
  methods: {
    async getPost() {
      try {
        const axios = await import('axios');
        const response = await axios.get('http://localhost:8000/api/v1/users');
        this.userData = response.data.data;
        console.log(response.data.data);
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
<style>
    .cent{
      text-align: center;
      margin: 30px 0px;
    }
    h1{
      font-weight: bold;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
</style>