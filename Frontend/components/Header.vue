<template>
    <div class="header flexRowSpaced">
      <img src="techman.png" alt="" class="logo" />
      <div class="headerContent flexRowRight">
        <p>Novo equipamento</p>
        <img src="logout_sair.png" alt="" class="logout" @click="goBack()"/>
      </div>
    </div>
</template>

<script>
export default {
  name: "Header",
  data(){
    return{

    }
  },
  methods:{
    goBack(){
      this.$router.back();
    }
  }
};
</script>

<style lang="scss" scoped>
.header {
  height: 75px;
  width: 100%;
  padding: 0 5px;
  background-color: var(--background);
  -webkit-box-shadow: 0px 0px 11px 0px rgba(0, 0, 0, 0.78);
  box-shadow: 0px 0px 11px 0px rgba(0, 0, 0, 0.78);

  img {
    height: 70px;
    width: 400px;
    margin-top: 5px;
  }

  .headerContent {
    padding-right: 15px;
    p {
      width: auto;
      height: auto;
      color: var(--dark);
      font-weight: bold;
      font-size: 20px;
      margin-right: 30px;
      cursor: pointer;
    }
    .logout {
      height: 30px;
      width: 30px;
      cursor: pointer;
    }
  }
}
</style>
