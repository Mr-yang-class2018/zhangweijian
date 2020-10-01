<style lang='less'>
.fl {
  float: left;
}
.fr {
  float: right;
}
#details {
  /* tabbar导航的数量*/
  /* @tabbar_length : 4;*/
  width: 100vw;
  height: 100vh;
  background-color: #eee;
  .detailsScroll {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 59px;
    overflow: hidden;
    .message {
      .shopInfo {
        border-radius: 10px;
      }
      .discount,
      .selected,
      .distribution,
      .weight,
      .freeFreight,
      .service {
        display: flex;
        min-height: 40px;
        background-color: #fff;
        position: relative;
        line-height: 30px;
        padding: 5px 10px;
        .left {
          flex: 1;
          text-align: left;
          padding-left: 15px;
        }
        .right {
          flex: 5;
          text-align: left;
          font-size: 12px;
          padding-right: 20px;
          div {
            text-overflow: ellipsis;
            overflow: hidden;
            display: -webkit-box; /*必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。*/
            -webkit-line-clamp: 1; /*用来限制在一个块元素显示的文本的行数。*/
            -webkit-box-orient: vertical; /*必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。*/
            span {
              color: red;
              border: 1px solid red;
              margin-right: 5px;
            }
          }
          span.icon {
            position: absolute;
            right: 10px;
            top: 10px;
            font-size: 16px;
          }
        }
      }
      .discount {
        height: 60px;
        border-radius: 10px;
        margin-top: 10px;
      }
      .selected {
        margin-top: 10px;
        border-top-left-radius: 10px;
        border-top-right-radius: 10px;
      }
      .distribution {
        p {
          padding-right: 40px;
        }
      }
      .service {
        text-align: left;
        padding-right: 30px;
        background-color: rgb(223, 223, 223);
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 10px;
        .icon {
          position: absolute;
          right: 10px;
          top: 10px;
        }
      }
    }
  }
}

.selectedopen {
  padding-bottom: 50px;
  .selectBtnBox {
    display: flex;
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 40px;
    background-color: #fff;
    padding-bottom: 5px;
    button {
      flex: 1;
      margin: 0 10px;
      border-radius: 25px;
      border: none;
      outline: none;
      background-color: red;
      color: #fff;
    }
    button:nth-child(2) {
      background-color: yellow;
      color: #000;
    }
  }
}
.ylike {
  float: left;
  padding: 5% 0%;
  width: 100%;
}
.like {
  float: left;
}
.tuijian {
  width: 100%;
  height: 390px;
  float: left;
  ul {
    width: 100%;
    height: 100%;
    li {
      width: 109px;
      height: 178px;
      margin: 10px 2px 10px 1px;
      color: #333;
      font-size: 12px;
      img {
        height: 109px;
        width: 100%;
      }
      p {
        height: 43px;
        line-height: 20px;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
        overflow: hidden;
        margin-bottom: 5px;
      }
      span {
        color: #f2270c;
        float: left;
      }
    }
  }
}
.el-tabs__nav {
  width: 100%;
}
.el-tabs__active-bar {
  background: none;
}
</style>
<template>
  <div id="details" v-loading="loading">
    <details-nav-bar ref="detailsNavBar" :title="titleArr"></details-nav-bar>
    <scroll class="detailsScroll" ref="DetailsScroll" @parentScroll="getScrollY" :probeType="3">
      <details-banner :dfeature="goodsImg"></details-banner>
      <div class="message">
        <!-- 商品信息 -->
        <details-base-info :goodsInfo="detailsGoods"></details-base-info>

        <!-- 优惠 -->
        <div class="discount" @click="open('discount')">
          <div class="left">优惠</div>
          <div class="right">
            <div>
              <span>换购</span>是否有换购---有 显示,没有不选是
            </div>
            <div>
              <span>限购</span>是否有限购---有 显示,没有不选是 111 111 111 1 11 11
            </div>
            <span class="icon el-icon-more"></span>
          </div>
        </div>
        <!-- 已选 -->
        <div class="selected" @click="open('selected')">
          <div class="left">已选</div>
          <div class="right">
            <span>规格....</span>
            <span>{{orderSel.order_num}}个</span>

            <span class="icon el-icon-more"></span>
          </div>
        </div>
        <!-- 送至 -->
        <div class="distribution" @click="open('distribution')">
          <div class="left">送至</div>
          <div class="right">
            <p>{{addr | changeAddr}}</p>
            <p>
              <span v-if="true" title="库存有货则显示">现货</span>
              {{getDistributionTime}}
            </p>
            <span class="icon el-icon-more"></span>
          </div>
        </div>
        <!-- 重量   不免运费  显示重量   免运费  显示 运费-->
        <div class="freeFreight" v-if="free_freight">
          <div class="left">运费</div>
          <div class="right">
            <p>免运费</p>
            <span class="icon el-icon-more"></span>
          </div>
        </div>
        <div class="weight" v-else>
          <div class="left">重量</div>
          <div class="right">
            <p>不免运费，显示重量(kg)</p>
            <span class="icon el-icon-more"></span>
          </div>
        </div>

        <!-- 服务 -->
        <div class="service" @click="open('service')">
          <div class="left">服务</div>
          <div class="right">
            <span class="icon el-icon-more"></span>
          </div>
        </div>
      </div>

      <!--评价 自定义 一个变量数组 暂时使用 -->
      <details-evaluate :evaluate="detailsEvaluate" :cDetailsId="detailsId"></details-evaluate>
      <!-- 问答 -->

      <!-- 体验 -->

      <!-- 商铺信息 -->
      <shops-info :shopsinfo="shopInfo"></shops-info>

      <!-- 推荐 -->
      <div style="height:500px;background-color:#fff;margin-top:10px;padding:0 5%;border-radius:12px;">
        <div class="ylike">
          <span class="like">猜你喜欢</span>
        </div>
        <div class="tuijian">
          <ul>
            <li v-for="(item,index) in jq" :key="index" class="fl">
              <img :src="path+item.img_cover" alt />
              <p>{{item.name}}</p>
              <span>￥{{item.money_old}}</span>
            </li>
          </ul>
        </div>
      </div>
      <!-- 详情 -->
      <div style="height:1560px;background-color:#fff;margin-top:10px;border-radius:12px;">
        <el-tabs v-model="activeName" @tab-click="handleClick">
          <el-tab-pane label="商品介绍" name="one">
            <div style="padding:0 10px 4px;color:#666;">
              <div style="height:28px;line-height:28px;">
                <span>编辑推荐</span>
              </div>
              <div style="text-align:left;line-height:25px;margin-bottom:60px;">
                <p>☆“巴巴爸爸”的变形特点和天马行空的故事，让孩子们在充满想象的阅读情境中学习和认知，充满童心和童趣，以及儿童对未知世界的无限渴望；关注每个孩子的不同性格、不同爱好，体现尊重儿童，关爱生命的教育观。</p>
                <p>
                  ☆巴巴爸爸经典故事在一家人相亲相爱、互相关心，互相帮助中展开，为小读者营造出温馨、和睦的家庭氛围，传递出无尽的温暖与爱。
                  <br />☆简单至极的艺术创作。“巴巴爸爸”的形象是世界上“zui简单”的创作之一，在作者的笔下展开的“巴巴爸爸”的世界变化无穷，充满想象，正如儿童的想象世界，带给他们无尽的快乐。
                  <br />☆巴巴爸爸经典故事系列专为3-6岁幼儿编写的图画故事书。流传近50年的世界经典图画书，畅销50多个国家和地区，累积销量超过1亿册，入选向全国青少年推荐百种优秀图书。
                </p>
              </div>
              <div style="height:28px;line-height:28px;">
                <span>内容简介</span>
              </div>
              <div style="text-align:left;line-height:25px;">
                <div>
                  <p>巴巴爸爸的问世：</p>
                  <p>巴巴爸爸名字由来于1970年5月一个晴朗的午后，泰勒和妻子缇森在卢森堡公园散步。泰勒听到一个孩子嘴里喊着：“巴巴、巴巴哒、巴巴”听不懂法语的泰勒问妻子是什么意思，妻子告诉他说是法语里的棉花糖（barbe &agrave; papa）。不久以后，他们在家附近的“祖尔Zeyer”咖啡馆开始画了个粉红色的，圆圆的，柔软的，像棉花糖一样的小粉人,小粉人自然就取名为巴巴爸爸（barbapapa）。</p>
                </div>
                <div>
                  <p>巴巴爸爸的欢乐一家：</p>
                  <p>巴巴爸爸与巴巴妈妈和七个巴巴宝宝（巴巴布拉伯、巴巴利波、巴巴拉拉、巴巴祖、巴巴波、巴巴布莱特、巴巴贝尔）是一个全球性的成功。他们造型奇特、色彩丰富、相亲相爱，能任意变成各种形状，非常有创意，赢得了一代又一代孩子的喜爱。</p>
                </div>
                <div>
                  <p>全世界孩子都喜欢的好爸爸：</p>
                  <p>（1）巴巴爸爸是du yi wu er的。</p>
                  <p>巴巴爸爸是可以变来变去的爸爸。只要一声“可里可里可里，巴巴变”，巴巴爸爸就可以随心所欲地改变身体的形状，变成大坝、变成桥、变成帐篷……</p>
                  <p>（2）巴巴爸爸是温暖和爱的象征。</p>
                  <p>巴巴爸爸、巴巴妈妈和7个孩子之间相亲相爱，互相温暖。巴巴爸爸对所有人和动物也都充满了爱，他走到哪里，就把温暖和关爱带到哪里，哪里就成了温馨和睦的乐园。</p>
                  <p>（3）巴巴爸爸教育理念很先进。</p>
                  <p>巴巴爸爸认为，每个孩子都有自己的性格爱好非但不让人头疼，反而是一件特别好的事情。对于孩子们，应该顺从他们的天性，教给他们不同的知识。巴巴爸爸学校里的孩子们*出色了，让家长们欣喜赞叹。</p>
                  <p>（4）巴巴爸爸用行动倡导和谐。</p>
                  <p>巴巴爸爸总是用平和的心态处理生活中的一切问题，顺应环境而变化，他可以变成桥梁、变成梯子、变成车辆，变成各种东西顺应自然，和环境形成和谐的统一，自然有自己的规律，人类要适应自然，不可以去改变自然。</p>
                </div>
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="规格参数" name="two">
            <div style="padding:0 10px 4px;">
              <div style="height:28px;line-height:28px;font-size:13px;color:#666;">
                <span>商品参数</span>
                <div
                  style="width:96%;border:1px solid #ccc;float:left;text-align:left;padding:2%;margin-top:10px;"
                >
                  <span style="border-right:1px solid #ccc;padding:2% 20px 2% 0;">商品编号</span>
                  <span style="padding-left:10px;">12648719</span>
                </div>
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="售后保障" name="three">
            <div style="padding:0 10px 4px;color:#666;font-size:12px;">
              <div>
                <p>服务承诺</p>
                <p style="text-align:left;line-height:20px;margin-top:10px;">
                  京东商城向您保证所售商品均为正品行货，京东自营商品开具机打发票或电子发票。凭质保证书及京东商城发票，可享受全国联保服务（奢侈品、钟表除外；奢侈品、钟表由京东联系保修，享受法定三包售后服务），与您亲临商场选购的商品享受相同的质量保证。京东商城还为您提供具有竞争力的商品价格和
                  <a
                    style="color:red;"
                    target="_self"
                    href="//wqs.jd.com/my/cart/extraYunfeiRule.shtml?detail=1"
                  >运费政策</a>，请您放心购买！
                  <br />注：因厂家会在没有任何提前通知的情况下更改产品包装、产地或者一些附件，本司不能确保客户收到的货物与商城图片、产地、附件说明完全一致。只能确保为原厂正货！并且保证与当时市场上同样主流新品一致。若本商城没有及时更新，请大家谅解！
                </p>
                <p style="margin:10px 0;">版权声明</p>
                <p style="text-align:left;">
                  京东商城上的所有商品信息、客户评价、商品咨询、网友讨论等内容，是京东商城重要的经营资源，未经许可，禁止非法转载使用。
                  本站商品信息均来自于厂商，其真实性、准确性和合法性由信息拥有者（厂商）负责。本站不提供任何保证，并不承担任何法律责任。
                </p>
                <p style="margin:10px 0;">价格说明</p>
                <p style="text-align:left;"><strong>1.京东价：</strong>京东价为商品的销售价，是您最终决定是否购买商品的依据。
                <br>
                <strong>2.划线价：</strong>商品展示的划横线价格为参考价，该价格可能是品牌专柜标价、商品吊牌价或由品牌供应商提供的正品零售价（如厂商指导价、建议零售价等）或该商品在京东平台上曾经展示过的销售价；由于地区、时间的差异性和市场行情波动，品牌专柜标价、商品吊牌价等可能会与您购物时展示的不一致，该价格仅供您参考。
                <br>
                <strong>3.折扣：</strong>如无特殊说明，折扣指销售商在原价、或划线价（如品牌专柜标价、商品吊牌价、厂商指导价、厂商建议零售价）等某一价格基础上计算出的优惠比例或优惠金额；如有疑问，您可在购买前联系销售商进行咨询。
                <br>
                <strong>4.异常问题：</strong>商品促销信息以商品详情页“促销”栏中的信息为准；商品的具体售价以订单结算页价格为准；如您发现活动商品售价或促销信息有异常，建议购买前先联系销售商咨询。
                </p>
              </div>
            </div>
          </el-tab-pane>
        </el-tabs>
      </div>

      <!-- 遮罩菜单 -->

      <el-drawer
        title="优惠"
        direction="btt"
        :close-on-press-escape="false"
        :visible.sync="discount"
        :append-to-body="true"
        size="70%"
      >
        <span>我来啦!</span>
      </el-drawer>
      <el-drawer
        title="已选"
        direction="btt"
        :close-on-press-escape="false"
        :visible.sync="selected"
        :append-to-body="true"
        :withHeader="false"
        custom-class="selectedopen"
        size="70%"
      >
        <div>
          <div v-for="(item,index) in selectNorm" :key="index">
            <div v-for="(i,j) in item" :key="j">
              <div>{{j}}</div>
              <div
                v-for="(m,n) in i"
                :key="n"
                style="width:90%;height:30px;text-overflow:hidden;overflow:hidden;margin-bottom:10px;text-align:left;background-color:#d4d4d4;line-height:30px;margin-left:5%;border-radius:15px;"
              >{{m.name}}</div>
            </div>
          </div>
          <div class="order_num">
            <div>数量</div>
            <div>
              <button @click="order_num--" :disabled="orderSel.order_num <= 1">-</button>
              <input type="text" v-model="orderSel.order_num" />
              <button @click="orderSel.order_num++">+</button>
            </div>
          </div>
          <div class="selectBtnBox" v-if="isConfirm">
            <button @click="addShop">添加至购物车</button>
            <button @click="addOrder(2)">立即购买</button>
          </div>
          <div class="selectBtnBox" v-else>
            <button @click="confirm">确认</button>
          </div>
        </div>
      </el-drawer>
      <!-- 配送 -->
      <el-drawer
        title="配送至"
        direction="btt"
        :close-on-press-escape="false"
        :visible.sync="distribution"
        :append-to-body="true"
        size="70%"
      >
        <ul
          style="text-align:left;line-height:20px; font-size:14px;padding:0 10px;"
          v-if="$store.state.userInfo"
        >
          <li
            style="padding:10px 0;"
            v-for="(item,index) in allAddress"
            :key="index"
            @click="changeAddr(item.takeover_addr)"
          >
            <!-- 使用过滤器吧地址进行拼接 -->
            {{ item.takeover_addr | changeAddr}}
          </li>
        </ul>
        <div v-else>省市县三级列表菜单</div>
      </el-drawer>
      <el-drawer
        title="服务"
        direction="btt"
        :close-on-press-escape="false"
        :visible.sync="service"
        :append-to-body="true"
        :withHeader="false"
        size="70%"
      >
        <span>服务</span>
      </el-drawer>
    </scroll>

    <details-tab-bar :addshopcart="addShop" :toaddorder="addOrder"></details-tab-bar>
  </div>
</template>

<script>
import Scroll from "components/contents/scroll/Scroll";
//引入当前组件的子组件
import DetailsNavBar from "./childComp/DetailsNavBar";
import DetailsBanner from "./childComp/DetailsBanner";
import DetailsBaseInfo from "./childComp/DetailsBaseInfo";
import ShopsInfo from "./childComp/ShopsInfo";
import DetailsEvaluate from "./childComp/DetailsEvaluate";
import DetailsTabBar from "./childComp/DetailsTabBar";
//引入商品数据网络请求
// import {getgoods,getGoods_id} from 'network/goods'
import { getGoodsId } from "network/details";
import { get_user_address } from "network/address";
import { addShopCart } from "network/shopCart";
import { get_goods } from "network/details";
import {
  GoodsInfo,
  ShopInfo,
  SelectNorm,
  Evaluate,
  orderConfirmData,
} from "common/utils";
// import { GoodsInfo, ShopInfo} from "common/utils";
export default {
  name: "Details",
  props: {},
  data() {
    return {
      activeName: "one",
      // path: "http://106.12.85.17:8090/public/image",
      titleArr: ["商品", "评价", "详情", "推荐"],
      detailsGoods: {}, //商品详情数据
      goodsImg: [], //轮播图数据
      shopInfo: {}, //商铺数据
      selectNorm: {}, // 规格数据
      detailsEvaluate: {}, // 商品评价
      currentIndex: 0,
      saveY: 0,
      tabCenter: null,
      loading: false, // 是否加载等待
      discount: false, //优惠遮罩层，不显示
      selected: false, // 选择遮罩层 不显示
      distribution: false, // 送至遮罩层 不显示
      service: false, //服务遮罩层不显示
      nowGoods: true,
      shopCategory: "", //商铺是个体还是自营
      addr: "", // 在本地存储取到的地址
      free_freight: 0, // 是否免运费  0 不免  1 免
      isConfirm: true,
      orderSel: {
        norm: {},
        order_num: 1,
      },
      confirmData: {}, //用于存储当前详情页提交的数据
      path: "http://106.12.85.17:8090/public/image/goods/",
    };
  },
  components: {
    Scroll,
    DetailsNavBar,
    DetailsBanner,
    DetailsBaseInfo,
    ShopsInfo,
    DetailsEvaluate,
    DetailsTabBar,
  },
  computed: {
    getDistributionTime() {
      //获取配送的时间
      let nowTime = new Date();
      // let h = nowTime.getHours();
      let h = 20;
      let temp = "";
      if (this.shopCeatgory == "自营") {
        //jd自营
        if (this.aa) {
          //本地配送  +1
          if (h >= 0 && h < 11) {
            temp = `在11:00前下单，预计今天送达,${this.shopCategory}`;
          }
          if (h > 11 && h < 23) {
            temp = `在23:00前下单，预计明天( ${this.setDate(nowTime, 1)})送达,${
              this.shopCategory
            }`;
          }
          if (h >= 23) {
            temp = `在明天(11:00)前下单,预计明天(${this.setDate(
              nowTime,
              1
            )})17:00前送达,${this.shopCategory}`;
          }
        } else {
          //异地配送  +2
          if (h >= 0 && h < 11) {
            temp = `在11:00前下单，预计${this.setWeek(
              nowTime,
              3
            )}(${this.setDate(nowTime, 2)})送达,${this.shopCategory}`;
          }
          if (h > 11 && h < 23) {
            temp = `在23:00前下单，预计${this.setWeek(
              nowTime,
              3
            )}(${this.setDate(nowTime, 3)})送达,${this.shopCategory}`;
          }
          if (h >= 23) {
            temp = `在明天(11:00)前下单,预计${this.setWeek(
              nowTime,
              3
            )}(${this.setDate(nowTime, 3)})17:00前送达,${this.shopCategory}`;
          }
        }
      } else {
        // 个体
        if (h >= 0 && h < 11) {
          temp = `在11:00前下单，预计今天送达,${this.shopCategory}`;
        }
        if (h > 11 && h < 23) {
          temp = `在23:00前下单，预计${this.setWeek(nowTime, 3)}(${this.setDate(
            nowTime,
            3
          )})送达,${this.shopCategory}`;
        }
        if (h >= 23) {
          temp = `在明天(11:00)前下单,预计${this.setWeek(
            nowTime,
            3
          )}(${this.setDate(nowTime, 3)})17:00前送达,${this.shopCategory}`;
        }
      }
      return temp;
    },
    allAddress() {
      return this.$store.state.allAddress;
    },
    localPath() {
      return this.$store.state.localData;
    },
  },
  created() {
    // console.log(this.$router);
    //在keep-alive状态下，created()方法只执行1此，因为当前组件不会被销毁
    // console.log("details被创建");
    this.detailsId = this.$route.params.id;
    this.getGoods(this.detailsId);
    this.getAddr();
    this.lookLocalStorage();
    this.get_goods();
  },
  watch: {},
  mounted() {
    this.$bus.$on("toDE", (path) => {
      this.isShow = true;
      this.$refs.DetailsScroll.scroll.scrollTo(0, -path * 800, 200);
      this.$refs.detailsNavBar.currentIndex = this.titleArr[path];
    });
    this.tabCenter = this.$refs.detailsNavBar.$el.querySelector(".tabCenter");
    // console.log(this.tabCenter);
  },
  methods: {
    get_goods() {
      get_goods().then((res) => {
        console.log(res);
        this.jq = res.data.slice(0, 6);
        console.log(this.jq);
      });
    },
    handleClick(tab, event) {
      console.log(tab, event);
    },
    //通过id获取商品的方法
    getGoods(data) {
      //页面等待
      this.loading = true;
      getGoodsId(data).then((res) => {
        if (res.code != 200) return;
        console.log(res);
        // 获取轮播数据
        this.goodsImg = res.data.goodsData.img_detalis_list;
        // 商品数据
        this.detailsGoods = new GoodsInfo(
          res.data.goodsData,
          res.data.shopData
        );
        // 取店铺数据
        this.shopInfo = new ShopInfo(res.data.shopData);
        console.log(this.detailsGoods);
        // 取规格数据
        this.selectNorm = new SelectNorm(
          res.data.norms,
          res.data.relationGoods
        );
        // this.getNorm(res.data.norms,res.data.relationGoods)
        //获取评价
        this.detailsEvaluate = new Evaluate(res.data.sevaluateDate);
        //获取立即购买需要提交的数据信息
        this.confirmData = new orderConfirmData(
          res.data.goodsData,
          res.data.shopData
        );

        console.log(this.detailsEvaluate);
        //自营 还是个体

        this.shopCategory = res.data.shopData.category;
        //是否免运费
        this.free_freight = res.data.goodsData.free_freight == 0 ? false : true;
        console.log(this.free_freight);
        this.loading = false;
      });
    },
    //在滚动的时候计算 tabCenter的显示，以及tanCenter的显示
    getScrollY(position) {
      if (-position.y <= 0) return;
      if (-position.y < 0) this.tabCenter.style.display = "none";
      else this.tabCenter.style.display = "flex";
      this.$refs.detailsNavBar.$el.style.background = `rgba(255,255,255,${
        -position.y / 100
      })`;
      this.tabCenter.style.opacity = `${-position.y / 100}`;
      this.tabCenter.style.filter = `opacity(${-position.y})`;
      this.$refs.detailsNavBar.currentIndex = this.titleArr[
        parseInt(-position.y / 800)
      ];
    },
    //tabCenter 点击后跳转滚动条位置

    // 设置一下送至的地址
    setAddr() {
      let address = this.$store.state.ShoppingAddress;
      let arr = address.takeover_addr.split(",");
      arr.pop();
      let temp = [];
      console.log(arr);
      for (let elem of arr.values()) {
        if (temp.indexOf(elem) == -1) {
          temp.push(elem);
        }
      }
      if (temp.length == 3) temp.pop();
      return temp.join(" ");
    },
    changeAddr(val) {
      //存到本地存储中 ， 存储的数据，不去存截取后的值，直接存原值
      this.addr = val;
      let data = window.localStorage.getItem(this.localPath);
      if (data != null) {
        data = JSON.parse(data);
      } else {
        data = {};
      }
      data.orderAddr = val;
      window.localStorage.setItem(this.localPath, JSON.stringify(data));
      this.distribution = false;
    },
    getAddr() {
      let data = window.localStorage.getItem(this.localPath);
      if (data != null && data != "") {
        data = JSON.parse(data);
        if (
          data.orderAddr != undefined &&
          data.orderAddr != null &&
          data.orderAddr != ""
        ) {
          this.addr = data.orderAddr;
        } else {
          this.addr = "北京市,北京市,昌平区,";
          data.orderAddr = "北京市,北京市,昌平区,";
        }
      } else {
        this.addr = "北京市,北京市,昌平区,";
        data = {};
        data.orderAddr = "北京市,北京市,昌平区,";
      }
      console.log(this.addr);
      window.localStorage.setItem(this.localPath, JSON.stringify(data));
    },
    setDate(nowtime = new Date(), val = 1) {
      let calculationTime = new Date(
        nowtime.getTime() + val * 24 * 60 * 60 * 1000
      );
      let a = `${calculationTime.getMonth()}月${calculationTime.getDate()}日`;
      return a;
    },
    setWeek(nowtime = new Date(), day = 4) {
      let setDay = nowtime.getDay();
      if (setDay + day > 7) {
        return "下周" + num(setDay + day - 7);
      } else {
        return "本周" + num(setDay + day);
      }
      //取值
      function num(temp) {
        let a = "";
        switch (temp) {
          case 7:
            a = "日";
            break;
          case 1:
            a = "一";
            break;
          case 2:
            a = "二";
            break;
          case 3:
            a = "三";
            break;
          case 4:
            a = "四";
            break;
          case 5:
            a = "五";
            break;
          case 6:
            a = "六";
            break;
        }
        return a;
      }
    },
    open(val) {
      if (val == "discount") {
        this.discount = true;
      }
      if (val == "selected") {
        this.selected = true;
        this.isConfirm = true;
      }
      if (val == "distribution") {
        this.distribution = true;
        // 点击配送至 ---->如果用户没有登录，应该先让他登录。在获取数据
        if (!this.$store.state.userInfo) {
          //打开省市县 地址

          this.$store.state.allAddress = "弹出个选择框-省-市-县";
          //在弹出框内 的县的位置，点击选择之后。把 省市县的值赋值给  this.$store.state.allAddress
          //并且  "省,市,县," ==>  ['省','市','县','']

          return;
        }
        if (this.allAddress == null) {
          get_user_address({
            user_id: this.$store.state.userInfo.id,
          }).then((res) => {
            this.$store.state.allAddress = res.data;
          });
        }
      }
      if (val == "service") {
        this.service = true;
      }
    },
    getNorm(norm, relation) {
      this.selectNorm = {};
      let aaa = {};
      if (norm.length > 0) {
        for (let i = 0; i < norm.length; i++) {
          if (!aaa[norm[i].ggname]) {
            aaa[norm[i].ggname] = [];
          }
          aaa[norm[i].ggname].push(norm[i]);
        }
      }
      this.selectNorm.norm = aaa;
      let bbb = {};
      if (relation.length > 0) {
        for (let i = 0; i < relation.length; i++) {
          console.log(bbb);
          if (!bbb[relation[i].relation_name]) {
            bbb[relation[i].relation_name] = [];
          }
          bbb[relation[i].relation_name].push(relation[i]);
        }
      }
      this.selectNorm.relation = bbb;
      console.log(this.selectNorm);
    },
    //添加购物车
    addShop() {
      let shopCart = {};
      shopCart.goods_id = this.detailsId;
      shopCart.user_id = this.$store.state.userInfo
        ? this.$store.state.userInfo.id
        : "";
      shopCart.num = this.orderSel.order_num;
      //需要计算取值
      shopCart.norm = JSON.stringify(this.orderSel.norm); //传递json串
      shopCart.takeover_addr = this.addr;
      //添加
      console.log(this.detailsGoods);
      shopCart.shop_id = this.shopInfo.shop_id;
      // shopCart.goods_name = this.detailsGoods.title
      // shopCart.goods_name = this.detailsGoods.title
      // shopCart.goods_name = this.detailsGoods.title
      // console.log(shopCart);

      // goods_name: "南极人女鞋夏季气垫鞋休闲鞋女士飞织透气女时尚学生板鞋运动跑步鞋韩版百搭潮鞋网鞋镂空"
      // money_now: "73"
      // money_old: "80"
      //如果用户存在
      if (this.$store.state.userInfo) {
        //请求购物车
        addShopCart(shopCart).then((res) => {
          if (res.code != 200) return console.log(res.msg);
          //重新获取购物车数据
          this.$store.dispatch("getShopCart", this.$store.state.userInfo.id);
        });
      } else {
        //没有用户的情况下。也能添加购物车
        console.log("用户不存在");
        let data = window.localStorage.getItem(this.localPath);
        console.log(data);
        if (data != null && data != "") {
          data = JSON.parse(data);
          let temp = 0;
          if (data.shopCart) {
            for (let i = 0; i < data.shopCart.length; i++) {
              if (
                data.shopCart[i].goods_id == shopCart.goods_id &&
                data.shopCart[i].norm == shopCart.norm &&
                data.shopCart[i].takeover_addr == shopCart.takeover_addr
              ) {
                data.shopCart[i].num += shopCart.num * 1;
                break;
              }
              temp++;
              console.log(temp);
            }
            if (temp == data.shopCart.length) {
              data.shopCart.push(shopCart);
            }
          } else {
            data.shopCart = [];
            data.shopCart.push(shopCart);
          }
        } else {
          data = {};
          data.shopCart = [];
          data.shopCart.push(shopCart);
        }
        this.calculationStorageShopNum(data.shopCart);
        //。。。shopCart是否存在.存在 添加数据。不存在创建数据
        window.localStorage.setItem(this.localPath, JSON.stringify(data));
      }
    },
    addOrder(val) {
      console.log("执行了添加订单");
      if (val == 1) {
        this.selected = true;
        this.isConfirm = false;
      } else {
        this.confirm();
      }
    },
    confirm() {
      // 确认console.log('被执行');
      this.confirmData.num = this.orderSel.order_num;
      //需要计算取值
      this.confirmData.norm = JSON.stringify(this.orderSel.norm);
      this.confirmData.takeover_addr = this.addr;
      this.$store.state.payMentData = [this.confirmData];
      //把 payMentData 的数据变成json数据并 提交到本地存储中

      //做存储   把数据存储到本地存储中

      let data = window.localStorage.getItem(this.$store.state.localData);
      data =
        data != undefined && data != null && data != "" ? JSON.parse(data) : {};
      //为 本地存储中添加 payMentData ， 值为提交到confirmOrder中的数据
      data.payMentData = this.$store.state.payMentData;
      //存储
      window.localStorage.setItem(
        this.$store.state.localData,
        JSON.stringify(data)
      );

      this.$router.push("/confirm_order/aaa");
    },
    //查看本地存储是否存有购物车数据
    lookLocalStorage() {
      if (!this.$store.state.userInfo) {
        console.log("a");
        let data = window.localStorage.getItem(this.localPath);
        console.log(data);
        if (data == null || data == "") return;
        data = JSON.parse(data);
        if (!data.shopCart) return;
        this.calculationStorageShopNum(data.shopCart);
      }
    },
    //计算用户没有登录的时候购物车的数量
    calculationStorageShopNum(arr) {
      this.$store.state.shopCartLength = 0;
      arr.forEach((item) => {
        this.$store.state.shopCartLength += item.num * 1;
      });
    },
  },
  filters: {
    changePrice(val, str = "$") {
      return str + Number(val).toFixed(2);
    },
    changeEvaluate(val) {
      console.log(val);
      return val;
    },
    changeAddr(val) {
      //去掉重复值的操作。。。。。
      // console.log(val);
      let addr = val.split(",");
      let temp = [];
      for (let i = 0; i < addr.length; i++) {
        if (temp.indexOf(addr[i]) == -1) {
          temp.push(addr[i]);
        }
      }
      addr = temp.join("");
      return addr;
    },
  },
};
</script>

