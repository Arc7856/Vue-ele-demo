<!--  -->
<template>
  <div class="edit-address">
    <Headertitle :header-title="headerTitle"></Headertitle>
    <main>
      <div class="form">
        <div class="form-group">
          <label for class="item-title">联系人</label>
          <div class="name-box">
            <div class="item-control name">
              <input
                type="text"
                placeholder="姓名"
                v-model="username"
                class="item-input"
                name="username"
              />
            </div>
            <div class="item-control male">
              <div :class="['new_radio',{active:gender=='先生'} ]" style="margin-right:10px">
                <label class="radio-hidden">
                  <input type="radio" v-model="gender" class="item-input" name="gender" value="先生" />
                </label>
                <span>先生</span>
              </div>
              <div :class="['new_radio',{active:gender=='女士'} ]">
                <label class="radio-hidden">
                  <input type="radio" v-model="gender" class="item-input" name="gender" value="女士" />
                </label>
                <span>女士</span>
              </div>
            </div>
          </div>
        </div>
        <div class="form-group">
          <label for class="item-title">电话</label>
          <div class="item-control phone-number more-text">
            <input type="tel" placeholder="手机号码" v-model="phone" class="item-input" name="phone" />
            <span>
              <i>+</i>通讯录
            </span>
          </div>
        </div>
        <router-link
          tag="div"
          :to="{path:'/search_city/'+ addressInfo.id,query:{search_type:'map',info:addressInfo}}"
          class="form-group"
        >
          <label for class="item-title">地址</label>
          <div class="item-control more-text">
            <span :class="{'black':address !== '选择收货地址'}">{{address}}</span>
            <i class="fa fa-angle-right"></i>
          </div>
        </router-link>
        <div class="form-group">
          <label for class="item-title">门牌号</label>
          <div class="item-control">
            <input
              type="text"
              placeholder="例：5号楼203室"
              v-model="detailAdd"
              class="item-input"
              name="detailAdd"
            />
          </div>
        </div>
        <div class="form-group">
          <label for class="item-title">标签</label>
          <div class="item-control mark">
            <div :class="['new_radio',{active:addressMark=='家'} ]" style="margin-right:10px">
              <label class="radio-hidden">
                <input
                  type="radio"
                  v-model="addressMark"
                  class="item-input"
                  name="addressMark"
                  value="家"
                />
              </label>
              <span>家</span>
            </div>
            <div :class="['new_radio',{active:addressMark=='公司'} ]" style="margin-right:10px">
              <label class="radio-hidden">
                <input
                  type="radio"
                  v-model="addressMark"
                  class="item-input"
                  name="addressMark"
                  value="公司"
                />
              </label>
              <span>公司</span>
            </div>
            <div :class="['new_radio',{active:addressMark=='学校'} ]" style="margin-right:10px">
              <label class="radio-hidden">
                <input
                  type="radio"
                  v-model="addressMark"
                  class="item-input"
                  name="addressMark"
                  value="学校"
                />
              </label>
              <span>学校</span>
            </div>
          </div>
        </div>
        <button class="btn btn-primary">保存并使用</button>
      </div>
    </main>
  </div>
</template>

<script>
import Headertitle from "@/components/Header/header";
import { mapState, mapMutations, mapActions } from "vuex";
export default {
  data() {
    return {
      headerTitle: "",
      addressInfo: null,
      username: "",
      gender: "",
      phone: "",
      address: "选择收货地址",
      detailAdd: "",
      addressMark: ""
    };
  },

  components: { Headertitle },

  computed: { ...mapState(["currentPosition", "selectPosition"]) },

  mounted() {
    this.init_data();
  },

  methods: {
    init_data() {
      this.headerTitle = this.$route.meta.title;
      this.addressInfo = this.$route.query.addressInfo;
      this.username = this.$route.query.addressInfo.user_name;
      this.gender = this.$route.query.addressInfo.user_gender;
      this.phone = this.$route.query.addressInfo.user_phoneNum;
      this.address = this.$route.query.addressInfo.title;
      this.detailAdd = this.$route.query.addressInfo.user_detailAdd;
      this.addressMark = this.$route.query.addressInfo.user_addressMark;
      console.log("info", this.addressInfo);
    }
  }
};
</script>
<style lang='scss' scoped>
.edit-address {
  main {
    width: 100%;
    padding: 0 0.12rem;
    margin-top: 0.63rem;
    .form {
      width: 100%;
      font-size: 12px;
      .form-group {
        width: 100%;
        display: flex;
        padding: 10px 0;
        border-bottom: 1px solid;
        border-bottom-color: rgba(204, 204, 204, 0.3);
        input {
          border: 0;
          font-size: 12px;
        }
        .item-title {
          display: inline-block;
          width: 0.6rem;
          color: #000;
          font-weight: 700;
        }
        .name-box {
          width: 82%;
        }
        .male {
          display: block;
          padding-top: 10px;
        }
        .phone-number {
          span {
            color: #26a2ff;
          }
        }
        .new_radio {
          width: 0.6rem;
          height: 0.18rem;
          line-height: 0.18rem;
          text-align: center;
          display: inline-block;
          padding-right: 15px;
          border: 1px solid;
          border-color: rgba(204, 204, 204, 0.5);
          border-radius: 5px;
        }
        .radio-hidden {
          opacity: 0;
        }
        .more-text {
          width: 82%;
          display: flex;
          justify-content: space-between;
          align-items: center;
          i {
            font-size: 16px;
          }
          .blank {
            color: #000 !important;
          }
        }

        .active {
          border-color: #26a2ff !important;
          color: #26a2ff;
        }
        .name {
          padding-bottom: 10px;
          border-bottom: 1px solid;
          border-bottom-color: rgba(204, 204, 204, 0.3);
        }
      }
      button {
        margin-top: 0.2rem;
      }
    }
  }
}
</style>