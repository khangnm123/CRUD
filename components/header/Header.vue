<template>
   <div>
     <nav class="navbar navbar-expand-lg navbar-light bg-light" style="background-color: #e3f2fd;">
    <a class="navbar-brand" href="#"><img src="../../assets/css/image/pngwing.com.png" alt="" style="width: 100%; height: 20px;"></a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <a class="nav-link" href="/">Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/about">Blog</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            Landing Page
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="#">Action</a>
            <a class="dropdown-item" href="#">Another action</a>
            <div class="dropdown-divider"></div>
            <a class="dropdown-item" href="#">Something else here</a>
          </div>
        </li>
      </ul>
      <form class="form-inline my-2 my-lg-0">
        <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-primary my-2 my-sm-0" type="submit">Search</button>
      </form>
    </div>
  </nav>
  <div class="carousel">
       
      <div v-for="(item , index) in userData" class="slide" :key="index">
        <img :src="item.image" alt="">
      </div>
        
  </div>
    <div class='carousel-controls'>
        <button class='carousel-controls__button' @click="previous">&#60;</button>
        <button class='carousel-controls__buttons' @click="next">&#62;</button>
      </div>
      
    </div>
</template>

<script>
const axios = require('axios');
export default {
  name: 'IndexPage',
  data() {
    return {
      userData: [{
        image:"https://vieclamcongtynhat.com/files/job-cover/hcm_600_customer_service_cho_cong_ty_it_hang_dau_cua_nhat_20220601145305.png"
      },
        {
        image:"https://i.ytimg.com/vi/fRM6VEjmNq4/maxresdefault.jpg"
        },
        {
          image: "https://images.fpt.shop/unsafe/filters:quality(5)/fptshop.com.vn/Uploads/images/tin-tuc/145501/Originals/WiXwAxYJh7TPwgaCThExnL.png"
        },
        {
        image:"https://file.hstatic.net/200000722513/article/gearvn-man-hinh-laptop-bi-dom-sang-1_f022715ed9aa4335bfd8fceb32891db5_master.jpg"
        },
        {
        image:"https://i.ytimg.com/vi/QnXRctg-1H0/maxresdefault.jpg"
        },
        {
        image:"https://images7.alphacoders.com/690/thumb-1920-690863.png"
      }
      ],
    };
  },
  methods: {
       next() {
      const first = this.userData.shift();// xóa phần tử ở vị trí đầu
      this.userData = this.userData.concat(first);
    },
    	previous() {
      const last = this.userData.pop(); //xóa phần tử ở vị trí cuối
      this.userData = [last].concat(this.userData);
    }
  }
 
  }
</script>

<style>
  .carousel-controls{
 display: flex;
    justify-content: space-between;
    position: relative;
    bottom: 430px;
  }
  img{
    width: 100%;
    height: 700px;
    background-size: cover;
    background-position: center;
  }
  
.carousel {
  display: flex;
  justify-content: space-between;
  align-items: center;
  overflow: hidden;
}

.slide {
  flex: 0 0 100%;
  display: flex;
  justify-content: space-around;
  padding: 50px 0;
  transition: all .3s;
  margin: 20px 0;
}

.carousel-controls__button {
  cursor: pointer;
  background: tomato;
  border: 0;
  color: #fff;
  border-radius: 3px;
  padding: 5px 10px;
  font-size: 18px;
}
.carousel-controls__buttons {
  cursor: pointer;
  background: tomato;
  border: 0;
  color: #fff;
  border-radius: 3px;
  padding: 5px 10px;
  font-size: 18px;
  left: 10px;
}
.carousel-controls__buttons:hover{
  transform: scale(1.1);
}
.carousel-controls__button:hover{
  transform: scale(1.1);
}

/* GO TO NEXT SLIDE */
.carousel-controls__button,
.carousel-controls__buttons {
  transition: transform 0.5s ease-in-out;
}
.carousel-controls__buttons {
 transition: transform 0.5s ease-in-out;
}
.carousel-controls__button {
  transform: translate(100%);
}
.carousel-controls__buttons {
  transform: translate(-100%);
}

/* GO TO PREVIOUS SLIDE */
.slide-prev-enter-active,
.slide-prev-leave-active {
  transition: transform 0.5s ease-in-out;
}
.slide-prev-enter {
  transform: translate(-100%);
}
.slide-prev-leave-to {
  transform: translate(100%);
}

</style>

