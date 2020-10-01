<style lang="less">
html {
  background: #f6f6f6;
}
.el-input__inner {
  border-radius: 30px;
  background: #f7f7f7;
  font-size: 12px;
}
.fl {
  float: left;
}
.fr {
  float: right;
}
.search_box {
  height: 100px;
  li {
    float: left;
    font-size: 12px;
    padding: 5px 13px;
    background: #f0f2f5;
    border-radius: 3px;
    margin: 0 6px 10px 0;
    color: #686868;
  }
  li.red {
    color: #e93b3d;
  }
}
</style>
<template>
  <div class id="search" style="background:#fff;">
    <nav-bar class="home-nav-bar" style="border-bottom:1px solid #666;padding:5px 0 7px;">
      <div slot="left" @click="$router.go(-1)">&lt;</div>
      <div slot="center">
        <el-input v-model="input" placeholder="请输入内容"></el-input>
      </div>
      <div
        style="background:#E93B3D;font-size:12px;color:#fff;border-radius:5px;"
        slot="right"
        @click="toSearch"
      >搜索</div>
    </nav-bar>
    <div style="width:92%;padding:5% 4% 2%;" id="hidden">
      <div style="width:100%;padding:3px 15px 8px 0;font-size:15px;height:20px;">
        <span class="fl" style="color:#232326;">热门搜索</span>
        <span class="fr" style="color:#999;" @click="hiee">隐藏</span>
      </div>
      <ul class="search_box">
        <li class="red">
          <span>美的电饭煲</span>
        </li>
        <li class="red">
          <span>摄像头高清</span>
        </li>
        <li class="red">
          <span>泡茶壶</span>
        </li>
        <li>
          <span>户外登山鞋</span>
        </li>
        <li>
          <span>学习机</span>
        </li>
        <li>
          <span>儿童遥控飞机</span>
        </li>
        <li>
          <span>登山帽</span>
        </li>
        <li>
          <span>智能手表</span>
        </li>
        <li>
          <span>篮球</span>
        </li>
        <li>
          <span>法兰绒床垫</span>
        </li>
        <li>
          <span>按摩器</span>
        </li>
      </ul>
    </div>

    <div style="width:92%;padding:5% 4% 2%;display:none;" id="show">
      <div style="width:100%;padding:3px 15px 8px 0;font-size:15px;height:20px;">
        <span class="fl" style="color:#232326;">热门搜索</span>
        <span class="fr" style="color:#999;" @click="show">显示</span>
      </div>
      <ul class="search_box">
        <p style="font-size:12px;color:#999;line-height:50px;">已隐藏搜索发现</p>
      </ul>
    </div>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
export default {
  name: "Keywords",
  beforeRouteEnter(to, from, next) {
    //组件创建前调用的守卫
    next();
  },
  created() {
    // console.log(this);
    // console.log(this.$root);
    this.$root.$children[0].is_jd_TabBar = false; // 也可以在页面渲染的时候 改变is_jd_TabBar的值
  },
  data() {
    return {
      input: "",
    };
  },
  components: {
    NavBar,
  },
  computed: {},
  methods: {
    hiee(){
      document.querySelector("#hidden").style.display = "none";
      document.querySelector("#show").style.display = "block";
    },
    show(){
      document.querySelector("#hidden").style.display = "block";
      document.querySelector("#show").style.display = "none";
    },
    toSearch() {
      this.$router.push("/search");
    },
  },
  mounted() {
    // this.$root.$children[0].is_jd_TabBar = false
  },
  beforeRouteUpdate(to, from, next) {
    //路由改变。组件被复用。调用的守卫
    next();
  },
  beforeRouteLeave(to, from, next) {
    //组件导航离开，调用的守卫
    this.$root.$children[0].is_jd_TabBar = true;
    next();
  },
};
</script>
