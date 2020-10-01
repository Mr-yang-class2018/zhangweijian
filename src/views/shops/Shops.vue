<style lang="less" scoped>
.dp_head {
  width: 100%;
  height: 120px;
  .fl {
    float: left;
    width: 100%;
    img {
      width: 55px;
      height: 55px;
      float: left;
      margin: 10px;
      background: #fff;
      border-radius: 8px;
    }
    div {
      float: left;
      width: 160px;
      padding-top: 20px;
      font-size: 16px;
      color: #fff;
      span {
        font-size: 12px;
        color: #eee;
        background: red;
        float: left;
        padding: 1px;
        margin-top: 5px;
      }
    }
    .dp_sc {
      width: 80px;
      margin: 0 10px;
      .sc {
        float: right;
        width: 60px;
        height: 30px;
        border-radius: 10px;
        background: #e93b3d;
        color: #fff;
        border: none;
      }
      p {
        font-size: 12px;
        margin-top: 4px;
        float: right;
      }
    }
    .nav_s {
      width: 0;
      span {
        color: #000;
        background: none;
        font-size: 16px;
        float: left;
        margin-left: 10px;
      }
    }
  }

  .nav {
    float: left;
    width: 100%;
    input {
      float: left;
      width: 20%;
      height: 30px;
      border-radius: 20px;
      border: none;
      margin-top: 5px;
      margin-left: 10px;
    }
    ul {
      width: 70%;
      padding-top: 10px;
      height: 30px;
      line-height: 30px;
      padding-left: 20px;
      float: left;
      li {
        float: left;
        width: 50px;
        color: #fff;
        font-weight: 700;
      }
    }
  }
}
.el-tabs__item.is-active {
  color: #fff;
}
.yezq {
  margin: 0 auto;
  width: 96%;
  background: #fff;
  border-radius: 12px;
  height: auto;
  ul.lb {
    width: 92%;
    padding: 10px 4%;
    margin: 0 auto;
    height: 240px;
    float: none;
    li {
      float: left;
      width: 62px;
      margin: 5px 10px;
      img {
        width: 100%;
      }
      span {
        color: #333;
        font-size: 14px;
      }
    }
  }
}
.oBox {
  width: 100%;
  height: 126px;
  div {
    float: left;
  }
}
.nav_box{
  li{
    float:left;
    width:75px;
    padding-top:10px;
    color:#666;
    img{
      width:20px;
    }
    p{
      font-size:12px;

    }
  }
}
</style>
<template>
  <div class="Store">
    <div
      style="position:fixed;top:0;left:0;background-image: linear-gradient(#000,#fff);width:100%;height:250px;z-index:-1;opacity:0.6;"
    ></div>
    <img
      style="position:fixed;top:0;left:0;width:100%;height:auto;z-index:-2;"
      src="../../assets/img/shops1.jpg"
      alt
    />

    <div class="dp_head">
      <div class="fl">
        <img src="../../assets/img/head1.png" alt />
        <div class=":title">
          接力出版社自营店铺&gt;
          <span>自营</span>
        </div>
        <div class="dp_sc">
          <button class="sc">收藏</button>
          <p>2.5万人收藏</p>
        </div>
        <div class="nav_s">
          <el-dropdown trigger="click" style="width:30px;">
            <span class="el-dropdown-link">
              <i class="el-icon-more-outline el-icon-more"></i>
            </span>
            <el-dropdown-menu slot="dropdown" class="dropdown">
              <el-dropdown-item command="/home">首页</el-dropdown-item>
              <el-dropdown-item command="/keywords">分类搜索</el-dropdown-item>
              <el-dropdown-item command="/profile">我的京东</el-dropdown-item>
              <el-dropdown-item command="/profile" disabled>浏览记录</el-dropdown-item>
              <el-dropdown-item command="/profile" divided>我的关注</el-dropdown-item>
              <el-dropdown-item command="/profile" divided>分享</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
      </div>

      <div class="nav">
        <input
          type="text"
          placeholder="搜商品"
          style="text-align:center;position:relative;z-index:10;"
          @click="keywords"
        />
        <el-tabs v-model="activeName" @tab-click="handleClick" style="color:#fff;">
          <el-tab-pane label="精选" name="one">
            <div class="yezq">
              <ul class="lb">
                <li>
                  <img src="../../assets/img/yezq1.png" alt />
                  <span>幼儿启蒙</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq2.png" alt />
                  <span>动漫卡通</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq3.png" alt />
                  <span>绘本图画</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq4.png" alt />
                  <span>益智游戏</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq5.png" alt />
                  <span>科普百科</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq6.png" alt />
                  <span>儿童文学</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq7.png" alt />
                  <span>励志成长</span>
                </li>
                <li>
                  <img src="../../assets/img/yezq8.png" alt />
                  <span>育儿教育</span>
                </li>
              </ul>
              <div class="oBox">
                <div style="width:128px;">
                  <img src="../../assets/img/yezq9.png" alt />
                  <img src="../../assets/img/yezq10.png" alt />
                </div>
                <div style="width:85px;margin:0 8px;">
                  <img src="../../assets/img/yezq11.png" alt />
                </div>
                <div style="width:128px;">
                  <img src="../../assets/img/yezq12.png" alt />
                  <img src="../../assets/img/yezq13.png" alt />
                </div>
              </div>
              <div class="ktdm_box">
                <div>
                  <img style="width:100%;height:58px;" src="../../assets/img/ktdm10.webp" alt />
                  <ul style="width:100%;padding:0;height:90%;float:none;margin:5% 0;">
                    <li
                      style="width:104px;border:1px solid #eee;height:165px;margin:5px;font-size:12px;text-align:left;"
                      v-for="(item,index) in dt"
                      :key="index"
                      class="fl"
                    >
                      <img style="width:100%;height:auto;margin:0;" :src="path+item.img_cover" alt />
                      <p style="color:#888;width:100%;height:30px;overflow:hidden;"
                      >{{item.name}}</p>
                      <p style="color:#FE645C">￥{{item.money_old}}</p>
                    </li>
                  </ul>
                </div>
              </div>
              <div style="width:100%;padding:10px 0;margin-bottom:60px;">
                <img style="width:100%;" src="../../assets/img/haoping.webp" alt="">
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="商品" name="two">
            <el-tabs v-model="active_Name" @tab-click="morenClick">
              <el-tab-pane label="默认" name="one1">默认</el-tab-pane>
              <el-tab-pane label="销量" name="two1">销量</el-tab-pane>
              <el-tab-pane label="价格" name="three1">价格</el-tab-pane>
              <el-tab-pane label="上新" name="four1">上新</el-tab-pane>
              <el-tab-pane label="京东物流" name="five1">京东物流</el-tab-pane>
            </el-tabs>
          </el-tab-pane>
          <el-tab-pane label="新品" name="three">
            <div style="background:#f7f7f7;height:1250px;width:354px;padding:0 10px;">
              <div style="width:100%;">
                <p style="color:#999;padding:20px 0 5px;height:18px;font-size:12px;">08月28日上新</p>
                <div
                  style="width:165px;height:260px;background:#fff;border-radius:5px;text-align:left;padding:0 5px;"
                >
                  <div>
                    <img style="width:100%;" src="../../assets/img/xp1.webp" alt />
                  </div>
                  <div style="margin:10px 0;font-size:12px;line-height:20px;color:#333;">
                    <span style="color:black;">远行的少年（一个女孩的励志、奋斗故事）</span>
                  </div>
                  <div>
                    <p style="color:#e93b3d;font-weight:bold;">￥27.00</p>
                  </div>
                </div>
              </div>

              <div style="width:100%;">
                <p style="color:#999;padding:20px 0 5px;height:18px;font-size:12px;">08月27日上新</p>
                <div
                  style="width:165px;height:260px;background:#fff;border-radius:5px;text-align:left;padding:0 5px;"
                >
                  <div>
                    <img style="width:100%;" src="../../assets/img/xp2.webp" alt />
                  </div>
                  <div style="margin:10px 0;font-size:12px;line-height:20px;color:#333;">
                    <span style="color:black;">205号教室（日本著名儿童文学作家大石真经典作品）</span>
                  </div>
                  <div>
                    <p style="color:#e93b3d;font-weight:bold;">￥18.80</p>
                  </div>
                </div>
              </div>

              <div style="width:100%;">
                <p style="color:#999;padding:20px 0 5px;height:18px;font-size:12px;">08月26日上新</p>
                <div
                  style="width:165px;height:260px;background:#fff;border-radius:5px;text-align:left;padding:0 5px;"
                >
                  <div>
                    <img style="width:100%;" src="../../assets/img/xp3.webp" alt />
                  </div>
                  <div style="margin:10px 0;font-size:12px;line-height:20px;color:#333;">
                    <span style="color:black;">给孩子的艺术创想:手的造型培养(套装共4册）</span>
                  </div>
                  <div>
                    <p style="color:#e93b3d;font-weight:bold;">￥34.60</p>
                  </div>
                </div>
              </div>

              <div style="width:100%;">
                <p style="color:#999;padding:20px 0 5px;height:18px;font-size:12px;">08月24日上新</p>
                <div
                  style="width:165px;height:260px;background:#fff;border-radius:5px;text-align:left;padding:0 5px;"
                >
                  <div>
                    <img style="width:100%;" src="../../assets/img/xp4.webp" alt />
                  </div>
                  <div style="margin:10px 0;font-size:12px;line-height:20px;color:#333;">
                    <span
                      style="color:black;display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
        overflow: hidden;"
                    >I SPY视觉大发现：哈哈屋·怪物加工场+奇趣谜·奥秘谷+圣诞惊奇·校园迷宫（套装共3册）</span>
                  </div>
                  <div>
                    <p style="color:#e93b3d;font-weight:bold;">￥44.60</p>
                  </div>
                </div>
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="动态" name="four">
            <div
              style="width:96%;background:#eee;height:400px;text-align:left;padding:4% 2%;border-radius:12px;"
            >
              <span style="font-size:12px;color:#333;">本店热销，欢迎选购</span>
              <ul style="width:100%;padding:0;height:90%;float:none;margin:5% 0;">
                <li
                  style="width:30%;margin:1.5%"
                  v-for="(item,index) in dt"
                  :key="index"
                  class="fl"
                >
                  <img style="width:100%;height:auto;margin:0;" :src="path+item.img_cover" alt />
                </li>
              </ul>
            </div>
            <div style="width:100%;color:#999;font-size:12px;line-height:42px;">没有更多动态了</div>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>



    <div style="width:100%;height:49px;background:#fff;position:fixed;bottom:0;">
      <ul class="nav_box">
        <li>
          <img src="../../assets/img/nav1.png" alt="">
          <p>首页</p>
        </li>
        <li>
          <img src="../../assets/img/nav2.png" alt="">
          <p>全部商品</p>
        </li>
        <li>
          <img src="../../assets/img/nav3.png" alt="">
          <p>活动</p>
        </li>
        <li>
          <img src="../../assets/img/nav4.png" alt="">
          <p>商品分类</p>
        </li>
        <li>
          <img src="../../assets/img/nav5.png" alt="">
          <p style="margin-top:2.5px;">联系客服</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// import NavBar from "components/common/navbar/NavBar";
// import Scroll from "components/contents/scroll/Scroll";
import { get_goods } from "network/details";
export default {
  name: "Shops",
  data() {
    return {
      activeName: "one",
      active_Name: 'one1',
      path: "http://106.12.85.17:8090/public/image/goods/",
    };
  },
  components: {
    //组件
    // NavBar
    // Scroll
  },
  computed: {},
  created() {
    this.get_goods();
  },
  activated() {
    //激活
  },
  deactivated() {
    //未激活
  },
  mounted() {
    //渲染
  },
  methods: {
    get_goods() {
      get_goods().then((res) => {
        console.log(res);
        this.dt = res.data.slice(10, 19);
        console.log(this.dt);
      });
    },
    handleClick(tab, event) {
      console.log(tab, event);
    },
    morenClick(tab, event) {
      console.log(tab, event);
    },
    keywords() {
      this.$router.push("/keywords");
    },
  },
  watch: {
    //监听
  },
};
</script>