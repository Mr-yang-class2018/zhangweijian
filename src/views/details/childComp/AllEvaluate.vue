<style lang="less" scoped>
.pl_box {
  width: 100%;
  background: #fff;
  height: 130px;
  li {
    float: left;
    padding: 0 10px;
    margin: 0 12px 12px 0;
    background: #fcedeb;
    border-radius: 15px;
    height: 30px;
    line-height: 30px;
    font-size: 12px;
  }
}
.plall{

  li{
    text-align:left;
    padding:18px 0;
    border-bottom:1px solid #f6f6f6;
    font-size:12px;
  }
}
</style>
<template>
  <div id="AllEvaluate">
    <nav-bar class="pf-nav-bar" style="border-bottom:2px solid #f6f6f6;">
      <div slot="left" @click="$router.go(-1)">
        <i class="el-icon-arrow-left"></i>
      </div>
      <div slot="center">商品评价</div>
      <div slot="right">
        <el-dropdown trigger="click" @command="pushRouter">
          <span class="el-dropdown-link">
            <i class="el-icon-more"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item command="/home" icon="el-icon-s-home">首页</el-dropdown-item>
            <el-dropdown-item command="/category" divided icon="el-icon-menu">分类搜索</el-dropdown-item>
            <el-dropdown-item command="/shopCar" divided icon="el-icon-shopping-cart-2">购物车</el-dropdown-item>
            <el-dropdown-item command="/my" divided icon="el-icon-user">我的京东</el-dropdown-item>
            <el-dropdown-item command="/category" divided icon="el-icon-s-order">浏览记录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </nav-bar>
    <div style="padding:0 18px;height:auto;">
      <ul class="pl_box">
        <li>
          <span>全部(400+)</span>
        </li>
        <li>
          <span>最新</span>
        </li>
        <li>
          <span>好评(50+)</span>
        </li>
        <li>
          <span>中评(0)</span>
        </li>
        <li>
          <span>差评(0)</span>
        </li>
        <li>
          <span>视频晒单(0)</span>
        </li>
        <li>
          <span>有图(8)</span>
        </li>
        <li>
          <span>品质一流(2)</span>
        </li>
        <li>
          <span>简单清晰(1)</span>
        </li>
      </ul>
      <div style="background: #f7f7f7;width:100%;height:15px;"></div>

      <ul class="plall" style="height:100%;">
        <li v-for="(item,index) in allEvaluate" :key="index">
          <img style="border-radius:50%;float:left;" :src="path+item.headImg" alt="">
          <span style="line-height:30px;">{{item.username}}</span>
          <span>{{item.Highpraise}}</span>
          <span style="float:right;line-height:30px;">{{item.evaluationTime}}</span>
          <p style="margin:15px 0;">{{item.evaluationDetails}}</p>
          <img :src="path+item.evaluationImg" alt="">
          <span style="color:#999;">{{item.evaluationNorm}}：{{item.evaluationShop}}</span>
          <span style="float:right;color:#3985ff;">回复</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { getAllEvaluate } from "network/details";
import navBar from "components/common/navbar/NavBar";
export default {
  name: "AllEvaluate",
  data() {
    return {
      path: "http://106.12.85.17:8090/public/image/evaluate/",
      allEvaluate: [],
    };
  },
  components: {
    //组件
    navBar,
  },
  computed: {
    //计算
  },
  created() {
    //创建

    console.log(this.$route);
    console.log(this.$route.params.id);
    if (this.$route.params.id) {
      getAllEvaluate(this.$route.params.id).then((res) => {
        if (res.code != 200) return console.log("没取到值");
        this.allEvaluate = res.data;
      });
    }
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
    //事件
  },
  watch: {
    //监听
  },
};
</script>
