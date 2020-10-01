<style lang="less">
html {
  background: #f6f6f6;
}
#myPaygo {
  background: #fff;
}
#myPaygo .search_box {
  width: 92%;
  padding: 10px 4%;
  border-bottom: 1px solid #f6f6f6;
  input {
    width: 94%;
    outline: none;
    height: 30px;
    background: #f7f7f7;
    border-radius: 20px;
    border: none;
    padding-left: 6%;
    line-height: 30px;
    font-size: 14px;
  }
}
.el-tabs__header {
  margin: 0;
}
.el-tabs__nav {
  width: 100%;
}
.el-tabs__item {
  width: 25%;
}
.el-tabs__item.is-active {
  color: red;
}
.el-tabs__active-bar {
  position: absolute;
  bottom: 0;
  left: 0;
  height: 2px;
  background-color: red;
  z-index: 1;
  transition: transform 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
  list-style: none;
}
.el-tabs--top .el-tabs__item.is-top:nth-child(2) {
  padding-left: 20px;
}
.el-tabs--top .el-tabs__item.is-top:last-child {
  padding-right: 20px;
}
</style>

<template>
  <div id="myPaygo">
    <nav-bar class="pf-nav-bar" style="border-bottom:1px solid #f6f6f6;">
      <div slot="left" @click="$router.go(-1)">
        <i class="el-icon-arrow-left"></i>
      </div>
      <div slot="center">我的订单</div>
      <div slot="right">
        <el-dropdown trigger="click">
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
    <div class="search_box">
      <input type="text" placeholder="商品名称/商品编号/订单编号" />
    </div>
    <el-tabs v-model="activeName">
      <el-tab-pane label="全部" name="one">
        <div v-if="aa" style="height:100%;background:#f6f6f6;padding:4%;">
          <div
            v-for="(allUser,index) in allU"
            :key="index" :data="allUser.id"
            style="background:#fff;border-radius:8px;padding:10px;margin-bottom:20px;"
          >
            <div v-for="(item,index) in all" :key="index"  class="order_header">
              <div style="height:26px;line-height:26px;color:#999;font-size:16px">
                <span style="float:left;margin-right:5px;">JD</span>
                <span style="float:left;color:#333;">{{item.shop_name}}</span>
                <span
                  style="float:right;width:15px;height:15px;border-left:1px solid #999;padding-left:5px;margin-top:6px;"
                >
                  <img style="width:100%;" src="../../assets/img/sc.png" alt />
                </span>
                <span style="float:right;font-size:14px;margin-right:10px;">已取消</span>
              </div>
              <div style="padding:8px 0 0;height:75px;text-align:left;">
                <img style="wdith:75px;height:75px;float:left;" :src="path+item.img_cover" alt />
                <div style="font-size: 14px;color: #333;line-height: 21px;margin-top:15px;">
                  <span>{{item.goods_name}}</span>
                </div>
              </div>
              <div
                style="padding:6px 0 6px 20%;width:80%;color:#999;font-size:14px;text-align:right;border-bottom:1px solid #f6f6f6;"
              >
                <span style="font-size:12px;margin-right:5px;">共{{item.num}}件商品</span>
                <span>应支付金额：</span>
                <span style="color:#151515;">¥{{item.money_now}}</span>
              </div>
              <div style="padding-top:10px;width:100%;text-align:right;font-size:14px;height:30px;">
                <span
                  style="height:30px;display:inline-block;width:82px;text-align:center;line-height:30px;color: #333;border: 1px solid #ccc;margin-right:10px;border-radius:15px;"
                >看相似</span>
                <span
                  style="color: #f2270c;border: 1px solid #f2270c;height:30px;display:inline-block;width:82px;text-align:center;line-height:30px;border-radius:15px;"
                >再次购买</span>
              </div>
            </div>
          </div>
          <div style="font-size: 14px;color: #999;line-height: 21px;margin: 12px 0;">
            <span>已经没有更多订单了</span>
          </div>
        </div>
      </el-tab-pane>
      <el-tab-pane label="待付款" name="two" v-if="aa">
        <div v-if="allU1.state!=1" style="height:100%;background:#f6f6f6;padding:4%;">
          <div
            v-for="(allUser1,index) in allU1"
            :key="index"
            style="background:#fff;border-radius:8px;padding:10px;margin-bottom:20px;"
          >
            <div v-for="(item,index) in all1" :key="index" class="order_header">
              <div style="height:26px;line-height:26px;color:#999;font-size:16px">
                <span style="float:left;margin-right:5px;">JD</span>
                <span style="float:left;color:#333;">{{item.shop_name}}</span>
                <span style="float:right;font-size:14px;margin-right:10px;color:#e93b3d;">待支付</span>
              </div>
              <div style="padding:8px 0 0;height:75px;text-align:left;">
                <img style="wdith:75px;height:75px;float:left;" :src="path+item.img_cover" alt />
                <div style="font-size: 14px;color: #333;line-height: 21px;margin-top:15px;">
                  <span>{{item.goods_name}}</span>
                </div>
              </div>
              <div
                style="padding:6px 0 6px 20%;width:80%;color:#999;font-size:14px;text-align:right;border-bottom:1px solid #f6f6f6;"
              >
                <span style="font-size:12px;margin-right:5px;">共{{item.num}}件商品</span>
                <span>应支付金额：</span>
                <span style="color:#151515;">¥ {{item.money_now}}</span>
              </div>
              <div style="padding-top:10px;width:100%;text-align:right;font-size:14px;height:30px;">
                <span
                  style="color: #f2270c;border: 1px solid #f2270c;height:30px;display:inline-block;width:82px;text-align:center;line-height:30px;border-radius:15px;"
                >去支付</span>
              </div>
            </div>
          </div>
          <div style="font-size: 14px;color: #999;line-height: 21px;margin: 12px 0;">
            <span>已经没有更多订单了</span>
          </div>
        </div>
        <div v-else style="padding:100px 10px 15px;background:#f6f6f6;">
          <div>
            <img style="width:25%;border-radius:50%;" src="../../assets/img/dd_null.png" alt />
          </div>
          <div>
            <p style="margin-top:15px;color:#666;font-size:16px;">您暂时没有相关订单 !</p>
          </div>
        </div>
      </el-tab-pane>
      <el-tab-pane label="待收货" name="three" v-if="aa">
        <div v-if="allU2.state!=2" style="height:100%;background:#f6f6f6;padding:4%;">
          <div
            v-for="(allUser2,index) in allU2"
            :key="index"
            style="background:#fff;border-radius:8px;padding:10px;margin-bottom:20px;"
          >
            <div v-for="(item,index) in all2" :key="index" class="order_header">
              <div style="height:26px;line-height:26px;color:#999;font-size:16px">
                <span style="float:left;margin-right:5px;">JD</span>
                <span style="float:left;color:#333;">{{item.shop_name}}</span>
                <span style="float:right;font-size:14px;margin-right:10px;color:#e93b3d;">待收货</span>
              </div>
              <div style="padding:8px 0 0;height:75px;text-align:left;">
                <img style="wdith:75px;height:75px;float:left;" :src="path+item.img_cover" alt />
                <div style="font-size: 14px;color: #333;line-height: 21px;margin-top:15px;">
                  <span>{{item.goods_name}}</span>
                </div>
              </div>
              <div
                style="padding:6px 0 6px 20%;width:80%;color:#999;font-size:14px;text-align:right;border-bottom:1px solid #f6f6f6;"
              >
                <span style="font-size:12px;margin-right:5px;">共{{item.num}}件商品</span>
                <span>应支付金额：</span>
                <span style="color:#151515;">¥ {{item.money_now}}</span>
              </div>
              <div style="padding-top:10px;width:100%;text-align:right;font-size:14px;height:30px;">
                <span
                  style="color: #f2270c;border: 1px solid #f2270c;height:30px;display:inline-block;width:82px;text-align:center;line-height:30px;border-radius:15px;"
                  @click="getState"
                >确认收货</span>
              </div>
            </div>
          </div>
          <div style="font-size: 14px;color: #999;line-height: 21px;margin: 12px 0;">
            <span>已经没有更多订单了</span>
          </div>
        </div>
        <div v-else style="padding:100px 10px 15px;background:#f6f6f6;">
          <div>
            <img style="width:25%;border-radius:50%;" src="../../assets/img/dd_null.png" alt />
          </div>
          <div>
            <p style="margin-top:15px;color:#666;font-size:16px;">您暂时没有相关订单 !</p>
          </div>
        </div>
      </el-tab-pane>
      <el-tab-pane label="已完成" name="four" v-if="aa">
        <div v-if="allU3.state!=3" style="height:100%;background:#f6f6f6;padding:4%;">
          <div
            v-for="(allUser3,index) in allU3"
            :key="index"
            style="background:#fff;border-radius:8px;padding:10px;margin-bottom:20px;"
          >
            <div v-for="(item,index) in all3" :key="index" class="order_header">
              <div style="height:26px;line-height:26px;color:#999;font-size:16px">
                <span style="float:left;margin-right:5px;">JD</span>
                <span style="float:left;color:#333;">{{item.shop_name}}</span>
                <span style="float:right;font-size:14px;margin-right:10px;color:#e93b3d;">待收货</span>
              </div>
              <div style="padding:8px 0 0;height:75px;text-align:left;">
                <img style="wdith:75px;height:75px;float:left;" :src="path+item.img_cover" alt />
                <div style="font-size: 14px;color: #333;line-height: 21px;margin-top:15px;">
                  <span>{{item.goods_name}}</span>
                </div>
              </div>
              <div
                style="padding:6px 0 6px 20%;width:80%;color:#999;font-size:14px;text-align:right;border-bottom:1px solid #f6f6f6;"
              >
                <span style="font-size:12px;margin-right:5px;">共{{item.num}}件商品</span>
                <span>应支付金额：</span>
                <span style="color:#151515;">¥ {{item.money_now}}</span>
              </div>
              <div style="padding-top:10px;width:100%;text-align:right;font-size:14px;height:30px;">
                <span
                  style="color: #f2270c;border: 1px solid #f2270c;height:30px;display:inline-block;width:82px;text-align:center;line-height:30px;border-radius:15px;"
                >确认收货</span>
              </div>
            </div>
          </div>
          <div style="font-size: 14px;color: #999;line-height: 21px;margin: 12px 0;">
            <span>已经没有更多订单了</span>
          </div>
        </div>
        <div v-else style="padding:100px 10px 15px;background:#f6f6f6;">
          <div>
            <img style="width:25%;border-radius:50%;" src="../../assets/img/dd_null.png" alt />
          </div>
          <div>
            <p style="margin-top:15px;color:#666;font-size:16px;">您暂时没有相关订单 !</p>
          </div>
        </div>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import navBar from "components/common/navbar/NavBar";
import { getOrder, getOrderbyOrderId } from "network/order";
export default {
  name: "myPaygo",
  data() {
    return {
      activeName: "one",
      path: "http://106.12.85.17:8090/public/image/goods/",
      aa: false
    };
  },
  components: {
    navBar
  },
  computed: {},
  created() {
    setTimeout(() => {
      this.aa = true;
    }, 2000);
    console.log(this.$store.state.userInfo.id);
    this.user_id = this.$store.state.userInfo.id;
    getOrder({ user_id: this.$store.state.userInfo.id }).then(res => {
      this.allU = res.data;
      console.log(res.data);
      for (var i = 0; i < res.data.length; i++) {
        getOrderbyOrderId(res.data[i].id).then(res => {
          this.all = res.data;
          // console.log(this.all);
        });
      }
    });

    getOrder({ user_id: this.$store.state.userInfo.id, state: 1 }).then(res => {
      this.allU1 = res.data;
      // console.log(res.data);
      for (var i = 0; i < res.data.length; i++) {
        getOrderbyOrderId(res.data[i].id).then(res => {
          this.all1 = res.data;
          // console.log(this.all1);
        });
      }
    });

    getOrder({ user_id: this.$store.state.userInfo.id, state: 2 }).then(res => {
      this.allU2 = res.data;
      // console.log(res.data);
      for (var i = 0; i < res.data.length; i++) {
        getOrderbyOrderId(res.data[i].id).then(res => {
          this.all2 = res.data;
          // console.log(this.all2);
        });
      }
    });

    getOrder({ user_id: this.$store.state.userInfo.id, state: 3 }).then(res => {
      this.allU3 = res.data;
      // console.log(res.data);
      for (var i = 0; i < res.data.length; i++) {
        getOrderbyOrderId(res.data[i].id).then(res => {
          this.all3 = res.data;
          // console.log(this.all3);
        });
      }
    });
  },
  activated() {},
  deactivated() {},
  mounted() {},
  methods: {
    getState() {
      getOrder({ user_id: this.$store.state.userInfo.id }).then(res => {
        console.log(res.data);
      });
    }
  },
  watch: {}
};
</script>

