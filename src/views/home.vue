<template>
<div class="content">

<div class="text main-text">欢迎使用 {{this.$project.projectName}}</div>

</div>
</template>
<script>
import router from '@/router/router-static'
export default {
  mounted(){
    this.init();
  },
  methods:{
    init(){
        if(this.$storage.get('Token')){
        this.$http({
            url: `${this.$storage.get('sessionTable')}/session`,
            method: "get"
        }).then(({ data }) => {
            if (data && data.code != 0) {
            router.push({ name: 'login' })
            }
        });
        }else{
            router.push({ name: 'login' })
        }
    }
  }
};
</script>

<style lang="scss" scoped>
.content {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 100%;
  height: 100%;
  min-height: 500px;
  text-align: center;
  /* 新增：背景图核心配置 */
  background-image: url("~@/assets/img/首页.png"); /* 路径对应首页图片存放位置，务必确认图片名称一致 */
  background-size: cover; /* 让背景图覆盖整个容器，保持比例不变形 */
  background-repeat: no-repeat; /* 禁止背景图重复平铺 */
  background-position: center center; /* 让背景图水平+垂直居中 */
  .main-text{
    font-size: 38px;
    font-weight: bold;
    margin-top: 15%;
  }
  .text {
    font-size: 24px;
    font-weight: bold;
    color: #333;
  }
}
</style>