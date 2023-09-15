<template>

  <div class="container">
    <h1 style="text-align: center; font-weight: bold;" >Page Blog</h1>
    <!-- nhận props edit từ blog.vue -->
    <blog :edit="blognew" @save="clickAdd"/> 
    <input type="text" :v-model="search" placeholder="search title" class="form-control mr-sm-2"> 
    <!-- v-for in ra dữ liệu từ data -->
    <b-card no-body class="overflow-hidden mb-3" v-for="(item, index) in postListens" :key="index.id"> 
      <b-row no-gutters>
        <b-col md="2">
          <nuxt-link :to="'/' + item.slug">
            <b-card-img :src="item.image" alt="Image" class="thumbnail-first" id="img"></b-card-img>
          </nuxt-link>
        </b-col>
        <b-col md="10">
          <b-card-body :title="item.title" @click="navigateToPost(item.slug)" id="title">
            <b-card-text id="content" style="color: black;">
              {{ item.content }}
            </b-card-text>
          </b-card-body>
             <div class="butt_add">
                <button v-b-modal.modal-prevent-closing  class="btn btn-warning" @click="clickEdit(item)">
                    Edit
                </button>
                <button @click="clickDelete(item)" class="btn btn-danger">
                    Delete
                </button>
              </div>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>
  
<script>
import blog from '../components/AddBlog/blog.vue'
export default {
  name: 'IndexPage',
  components: {
    blog
  },
 
  data() {
    return {
      blognew:{}, //chứa 1 chuỗi mới
      search:'',
      postList: [],//mảng rổng 
    };
  },
 
  created() {
    this.getPost();
  },
  methods: {
    async getPost() {
      try {
        const axios = await import('axios');
        const response = await axios.get(`http://localhost:8000/api/v1/users`); //fetch dữ liệu
        this.postList = response.data.data;
      } catch (error) {
        console.log(error);
      }
    },
    navigateToPost(slug) {
      this.$router.push('/' + slug); //push qua truong _slug.vue
    },
    clickAdd(item) {
      let index = this.postList.findIndex((e) => e.id === item.id); // thêm phần tử
      if (index >= 0) {
        this.postList.splice(index , 1 , item) //spilce: thay thế 1 phần tử trong mảng thành phần tử khác 
      } else {
        this.postList.push(item)
      }
      return 
    },
    clickDelete(itemDelete) {
      console.log(itemDelete);
      for (let i = 0; i < this.postList.length; i++){ // xóa phần tử
        if (itemDelete.id === this.postList[i].id) {
            this.postList.splice(i , 1) //spilce: thay thế 1 phần tử trong mảng thành phần tử khác && đưa lên vị trí 1 
        }
      }
    },
    clickEdit(itemEdit) { // chỉnh sửa phần tử
      this.blognew = itemEdit;
    }
  },
  computed: {
    postListens() {
      return this.postList.filter(item => { // filter: Bộ lộc
       return item.title.toLowerCase().includes(this.search.toLowerCase()) // includes : dùng để xem một chuỗi ký tự có một ký tự hoặc 1 chuỗi nào đó hay không
      })
    }
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
}

#img {
  width: 150px;
  height: 150px;
}

#title {
  cursor: pointer;
  color: rgb(14, 99, 102);

}

#content {
  color: black;
}

#title:hover {
  cursor: pointer;
  color: rgb(185, 81, 81);
  animation: 0.3s;
}
</style>