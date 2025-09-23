<template>
  <div class="home" v-loading="loading">
    <swiper id="swiperBox" v-bind:options="swiperOption" ref="mySwiper">
      <swiper-slide class="swiper-slide slide-one">
        <!-- 首页内容 -->
      </swiper-slide>
      
      <!-- 产品第一页 -->
      <swiper-slide class="swiper-slide slide-two">
        <div class="page">
          <h3>公司产品 ({{ currentPage }}/{{ totalPages }})</h3>
          <p>Company Products ({{ currentPage }}/{{ totalPages }})</p>
        </div>
        <ul class="case-item">
          <li
            v-for="(item,index) in currentPageCases"
            :key="index"
            :style="{ backgroundImage: 'url(' + item.Img + ')' }"
          >
            <router-link
              class="text-decoration"
              :to="{ name: 'casedetails', params: { id: item.Id }}"
            >
              <div class="case-item-hover">
                <p class="hover-title">{{item.Title}}</p>
                <div class="bottom"></div>
                <div class="more">
                  <span>MORE</span>
                </div>
              </div>
            </router-link>
          </li>
        </ul>
        <div class="pagination">
          <button @click="prevPage" :disabled="currentPage === 1">‹ 上一页</button>
          <span class="page-info">第 {{ currentPage }} 页，共 {{ totalPages }} 页</span>
          <button @click="nextPage" :disabled="currentPage === totalPages">下一页 ›</button>
        </div>
      </swiper-slide>
      
      <!-- 产品第二页 -->
      <swiper-slide class="swiper-slide slide-two">
        <div class="page">
          <h3>公司产品 ({{ currentPage }}/{{ totalPages }})</h3>
          <p>Company Products ({{ currentPage }}/{{ totalPages }})</p>
        </div>
        <ul class="case-item">
          <li
            v-for="(item,index) in currentPageCases"
            :key="index"
            :style="{ backgroundImage: 'url(' + item.Img + ')' }"
          >
            <router-link
              class="text-decoration"
              :to="{ name: 'casedetails', params: { id: item.Id }}"
            >
              <div class="case-item-hover">
                <p class="hover-title">{{item.Title}}</p>
                <div class="bottom"></div>
                <div class="more">
                  <span>MORE</span>
                </div>
              </div>
            </router-link>
          </li>
        </ul>
        <div class="pagination">
          <button @click="prevPage" :disabled="currentPage === 1">‹ 上一页</button>
          <span class="page-info">第 {{ currentPage }} 页，共 {{ totalPages }} 页</span>
          <button @click="nextPage" :disabled="currentPage === totalPages">下一页 ›</button>
        </div>
      </swiper-slide>
      
      <swiper-slide class="swiper-slide slide-three">
        <div class="page">
          <h3>最新资讯</h3>
          <p>Latest News</p>
        </div>
        <div class="news-content">
          <div class="news-content-item" v-for="(news,i) in newsList" :key="i">
            <div :style="'order: '+ (i%2==0 ? 1: 3)">
              <router-link
                class="text-decoration"
                :to="{ name: 'newsdetails', params: { id: news.Id }}"
              >
                <div class="item-img" :style="{ backgroundImage: 'url(' + news.Img + ')' }"></div>
              </router-link>
            </div>
            <div style="order: 2">
              <el-divider>
                <i class="el-icon-apple"></i>
              </el-divider>
            </div>
            <div class="item-content" :style="'order: '+ (i%2==0 ? 3: 1)">
              <h3>{{news.Title}}</h3>
              <p>{{news.Content}}</p>
              <span>{{news.CreateTime}}</span>
            </div>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>
 
<script>
import { swiper, swiperSlide } from "vue-awesome-swiper";

// 导入12张产品图片 - 你需要准备12张不同的图片
import product1 from '@/assets/img/product1.jpg'
import product2 from '@/assets/img/product1.jpg'
import product3 from '@/assets/img/product1.jpg'
import product4 from '@/assets/img/product1.jpg'
import product5 from '@/assets/img/product1.jpg'
import product6 from '@/assets/img/product1.jpg'
import product7 from '@/assets/img/product1.jpg'
import product8 from '@/assets/img/product1.jpg'
import product9 from '@/assets/img/product1.jpg'
import product10 from '@/assets/img/product1.jpg'
import product11 from '@/assets/img/product1.jpg'
import product12 from '@/assets/img/product1.jpg'

import news1 from '@/assets/img/product1.jpg'
import news2 from '@/assets/img/product1.jpg'
import news3 from '@/assets/img/product1.jpg'

export default {
  name: "HelloWorld",
  components: {
    swiper,
    swiperSlide
  },
  data() {
    return {
      loading: true,
      allCaseList: [], // 所有12张产品
      newsList: [],
      currentPage: 1, // 当前页码
      itemsPerPage: 6, // 每页显示6张
      swiperOption: {
        notNextTick: true,
        direction: "vertical",
        grabCursor: true,
        setWrapperSize: true,
        autoHeight: true,
        slidesPerView: 1,
        mousewheel: true,
        mousewheelControl: true,
        height: window.innerHeight - 60,
        resistanceRatio: 0,
        observeParents: true,
        on: {
          slideChange: () => {
            this.handleSlideChange();
          }
        }
      }
    };
  },
  created() {
    this.initLocalData();
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.swiper;
    },
    totalPages() {
      return Math.ceil(this.allCaseList.length / this.itemsPerPage);
    },
    currentPageCases() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.allCaseList.slice(start, end);
    }
  },
  methods: {
    initLocalData() {
      // 初始化12张产品数据
      this.allCaseList = [
        { Id: 1, Title: "产品一名称", Img: product1 },
        { Id: 2, Title: "产品二名称", Img: product2 },
        { Id: 3, Title: "产品三名称", Img: product3 },
        { Id: 4, Title: "产品四名称", Img: product4 },
        { Id: 5, Title: "产品五名称", Img: product5 },
        { Id: 6, Title: "产品六名称", Img: product6 },
        { Id: 7, Title: "产品七名称", Img: product7 },
        { Id: 8, Title: "产品八名称", Img: product8 },
        { Id: 9, Title: "产品九名称", Img: product9 },
        { Id: 10, Title: "产品十名称", Img: product10 },
        { Id: 11, Title: "产品十一名称", Img: product11 },
        { Id: 12, Title: "产品十二名称", Img: product12 }
      ];

      this.newsList = [
        {
          Id: 1,
          Title: "最新资讯标题一",
          Content: "这里是资讯内容的简要描述...",
          CreateTime: "2024-01-15",
          Img: news1
        },
        {
          Id: 2,
          Title: "最新资讯标题二",
          Content: "这里是资讯内容的简要描述...",
          CreateTime: "2024-01-14",
          Img: news2
        },
        {
          Id: 3,
          Title: "最新资讯标题三",
          Content: "这里是资讯内容的简要描述...",
          CreateTime: "2024-01-13",
          Img: news3
        }
      ];

      this.loading = false;
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
        // 切换到对应的swiper slide（产品页从索引1开始）
        this.swiper.slideTo(this.currentPage);
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
        this.swiper.slideTo(this.currentPage);
      }
    },
    handleSlideChange() {
      const activeIndex = this.swiper.activeIndex;
      // 如果切换到产品页（索引1和2），更新当前页码
      if (activeIndex === 1 || activeIndex === 2) {
        this.currentPage = activeIndex;
      }
    }
  },
  mounted() {
    // 注释掉原有的API请求，使用本地数据
  }
};
</script>
 
<style lang="scss" scoped>
.swiper-slide {
  font-size: 24px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;

  .page {
    text-align: center;
    height: 100px;
    overflow: hidden;
    h3,
    p {
      font-size: 40px;
      font-weight: 400;
      color: #fff;
    }
  }

  .slogan {
    text-align: center;
    font-size: 50px;
    color: #fff;
    padding: 30px 0;
  }
}

//经典案例
.case-item {
  width: 1100px;
  height: 500px;
  overflow: hidden;
  margin: 0 auto;
  margin-top: 30px;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  li {
    width: 330px;
    height: 250px;
    list-style: none;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    background-origin: content-box;
    margin: 5px;
    position: relative;
    overflow: hidden;

    &:hover {
      .case-item-hover {
        opacity: 1;
        transition: all 0.4s ease-in-out;
      }
    }
  }
}

//经典案例hover
.case-item-hover {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  opacity: 0;
  overflow: hidden;
  background-color: rgba(225, 56, 52, 0.7);

  .hover-title {
    height: 50px;
    color: #fff;
    font-size: 18px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    font-weight: 400;
    margin-top: 20px;
  }
  .bottom {
    border-bottom: 1px solid #fff;
    width: 60px;
    margin: 0 auto;
  }
  .more {
    width: 90px;
    padding: 5px 5px;
    margin: 0 auto;
    margin-top: 100px;
    border: 2px solid #fff;
    span {
      color: #fff;
      font-size: 20px;
    }
  }
}

// 分页样式
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
  gap: 20px;
  
  button {
    padding: 10px 20px;
    background: rgba(255, 255, 255, 0.2);
    border: 1px solid #fff;
    color: #fff;
    cursor: pointer;
    border-radius: 5px;
    font-size: 14px;
    transition: all 0.3s ease;
    
    &:disabled {
      opacity: 0.3;
      cursor: not-allowed;
    }
    
    &:hover:not(:disabled) {
      background: rgba(255, 255, 255, 0.4);
      transform: translateY(-2px);
    }
  }
  
  .page-info {
    color: #fff;
    font-size: 16px;
    font-weight: 500;
  }
}

.slide-one {
  background: url(../assets/img/home_top.jpg) no-repeat center;
  background-size: cover;
}
.slide-two {
  background: url(../assets/img/home_do.jpg) no-repeat center;
  background-size: cover;
}
.slide-three {
  background: url(../assets/img/home_anli.jpg) no-repeat center;
  background-size: cover;
}

//最新资讯
.news-content {
  width: 1240px;
  margin: 0 auto;
  margin-top: 40px;
  display: flex;
  justify-content: center;

  &-item {
    width: 400px;
    display: flex;
    flex-direction: column;

    .item-img {
      width: 360px;
      height: 230px;
      background-repeat: no-repeat;
      background-size: cover;
      background-position: center;
      background-origin: content-box;
      margin: 0 auto;
    }
    .el-divider {
      background-color: #fff;
      height: 3px;
      .el-divider__text {
        width: 20px;
        height: 20px;
        border-radius: 50%;
        padding: 0px;
        color: #fff;
      }
    }
    .item-content {
      width: 360px;
      height: 230px;
      margin: 0 auto;
      h3 {
        font-size: 22px;
        height: 30px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
      p {
        font-size: 15px;
        height: 80px;
        overflow: hidden;
        margin: 10px 0;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 4;
        -webkit-box-orient: vertical;
        white-space: normal !important;
        word-wrap: break-word;
      }
      span {
        display: block;
        font-size: 14px;
        text-align: end;
      }
      h3,
      p,
      span {
        color: #fff;
      }
    }
  }
}
</style>