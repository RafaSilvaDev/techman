<template>
  <main class="flexRowCenter">
    <div class="loginContainer flexColumnCenter">
      <img src="techman.png" alt="techman" />

      <div class="login flexColumnCenter">
        <input type="password" name="" id="pass" v-model="password" disabled />
        <div class="numbersContainer flexColumnCenter">
          <div
            class="numberRows flexRowCenter"
            v-for="(row, index) in buttons"
            :key="index"
          >
            <button
              v-for="(btn, index) in row"
              :key="index"
              @click="btnClick(btn)"
            >
              {{ btn }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "login",

  data() {
    return {
      password: "",
      buttons: [
        ["1", "2", "3"],
        ["4", "5", "6"],
        ["7", "8", "9"],
        ["C", "0", "↲"],
      ],
    };
  },
  methods: {
    btnClick(btn) {
      switch (btn) {
        case "C":
          this.password = "";
          break;
        case "↲":
          if (this.password.length >= 6) {
            this.$axios
              .post(this.$store.state.BASE_URL + "/users/?auth", {
                password: this.password,
              })
              .then((response) => {
                console.log(response);
                if (response.data.msg !== undefined) {
                  alert(response.data.msg);
                  this.password = "";
                } else {
                  this.$router.push("/home");
                }
              })
              .catch((err) => {
                console.log(err);
              });
          } else {
            alert("Sua senha deve conter ao menos 6 digitos.");
          }
          break;
        default:
          this.password += btn;
          break;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
main {
  width: 100vw;
  height: 100vh;
  max-height: 100vh;
  background-color: var(--background);
}

.loginContainer {
  width: 50vw;
  max-width: 400px;
  height: 80vh;

  img {
    height: 100px;
    width: 100%;
  }
  .login {
    margin-top: 10px;
    padding: 30px 40px;
    width: 100%;
    height: 100%;
    background: var(--light);

    #pass {
      height: 50px;
      margin-bottom: 10px;
      border: none;
      border-bottom: 2px solid var(--dark);
      text-align: center;
      outline: none;
      font-size: 30px;
      color: var(--dark);
      background: none;
    }
    .numbersContainer {
      .numberRows {
        margin: 8px;
        button {
          border-radius: 100%;
          border: 1px solid var(--dark);
          margin: 0 8px;
          min-width: 90px;
          min-height: 90px;
          font-size: 35px;
          color: var(--dark);
          cursor: pointer;
          &:hover {
            background-color: var(--background);
          }
        }
      }
    }
  }
}
</style>
