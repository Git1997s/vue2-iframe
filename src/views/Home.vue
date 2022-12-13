<template>
  <div class="home">
    <el-container>
      <el-header id="header">Header</el-header>
      <el-container>
        <el-aside width="200px">Aside</el-aside>
        <el-container>
          <el-main>
              <Iframe />
          </el-main>
          <el-footer id="footer">Footer</el-footer>
        </el-container>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import Iframe from "./Iframe.vue";

export default {
  name: "Home",
  components: {
    Iframe,
  },
  data() {
      return {
      };
  },
  created() {
  },
  mounted() {
    this.setMyIframeHeight();
     window.addEventListener("resize", () => this.setMyIframeHeight(), false);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.setMyIframeHeight(), false);
  },
  methods: {
    setMyIframeHeight(){
        // 页面可视高-顶部实际高-底部实际高-多余部分高度
      let that = this;
      this.$nextTick(() => {
        let headerHeight = document.getElementById("header").offsetHeight;
        let footerHeight = document.getElementById("footer").offsetHeight;
        let bodyHeight = document.body.clientHeight;
        let outHeight =parseFloat(bodyHeight - headerHeight - footerHeight)-5+ "px";
          console.log('获取到le',bodyHeight);
        //设置iframe页面高度 因为在iframe时页面已经生成，高度无法改变，需要在iframe生成后直接设置高度
        document.querySelector("#myIframe").style.height = outHeight;
      });
    }
  }
};
</script>
<style>
    body{
        overflow: hidden !important;
    }
    .home,.el-container{
      height: 100%;
    }
  .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }
  
  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
  }
  
  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    padding: 0 !important;
  }
  
  body > .el-container {
    margin-bottom: 40px;
  }
  
  .el-footer{
      height: 60px;
      bottom: 0;
      width: 100%;
  }
</style>
