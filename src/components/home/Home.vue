<template>
  <el-container>
    <el-header>
      <el-row>
        <el-col :span="8">
          <img src="../../assets/images/logo.png" alt height="60px" width="60px" />
        </el-col>
        <el-col :span="8">
          <h1>ERP标签打印平台</h1>
        </el-col>
        <el-col :span="8" class="col_r">
          当前用户:{{ userName }}
          <a href="#" @click.prevent="logout">退出</a>
        </el-col>
      </el-row>
    </el-header>

    <el-container>
      <el-aside width="210px">
        <el-menu
          default-active="2"
          :router="true"
          class="el-menu-vertical-demo"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="blue"
        >
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-printer"></i>
              <span>入库标签打印</span>
            </template>

            <el-menu-item index="/rm_non_wafer">
              <i class="el-icon-folder-opened"></i>
              <span style="font-size:smaller">原材料上机标签</span>
            </el-menu-item>
            <el-menu-item index="/rm_in">
              <i class="el-icon-folder-opened"></i>
              <span style="font-size:smaller">原材料进料标签</span>
            </el-menu-item>
            <el-menu-item index="/rm_wafer">
              <i class="el-icon-folder-opened"></i>
              <span style="font-size:smaller">晶圆入库标签</span>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main>
        <!-- router出口 -->
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      userName: "",
    };
  },
  created() {
    this.userName = localStorage.getItem("userName");
    if (
      this.userName == null ||
      this.userName == "" ||
      this.userName == undefined
    ) {
      // 2.跳转到Login页
      this.$router.push("/login");
    }
    // console.log("获取的用户名:", this.userName);
  },
  methods: {
    // 展开
    handleOpen() {
      console.log("展开");
    },
    handleClose() {
      console.log("关闭");
    },
    // 退出
    logout() {
      // 确认框
      this.$confirm("此操作将退出该账户, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          // 1.提示
          this.$message({
            type: "success",
            message: "退出成功!",
            duration: 800,
          });
          // 2.跳转到Login页
          this.$router.push("/login");
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消退出",
            duration: 800,
          });
        });
    },
  },
};
</script>

<style scoped>
/* 外部容器 */
.el-container {
  height: 100%;
  min-width: 900px;
}
/* 头部 */
.el-header {
  background: #5d8db8;
  /* 去除空余部分 */
  padding: 0;
}

/* 头部标题 */
h1 {
  color: rgba(255, 255, 255, 0.973);
  /* 居中 */
  text-align: center;
  line-height: 60px;
  font-size: 30px;
}

.col_r {
  text-align: right;
  line-height: 60px;
  padding-right: 30px;
}

.col_r a {
  color: blue;
}

/* 侧栏 */
.el-aside {
  background: #545c64;
}
/* 主体 */
.el-main {
  background: #eaeef1;
}

.el-menu-item.is-active {
  background: #f377b4 !important;
}
</style>