<template>
  <main>
    <div class="modal-overlay flexColumnCenter" v-if="display">
      <div class="modal flexColumn">
        <div class="close" @click="closeModal()">
          <p class="icon">X</p>
        </div>
        <h2>Exclusão de equipamento</h2>
        <p>
          Atenção! tem certeza que deseja excluir o equipamento? essa ação não
          podera ser desfeita.
        </p>
        <button>excluir</button>
      </div>
    </div>
    <Header />
    <div class="homeContent flexColumn">
      <div
        class="equipment flexRowCenter"
        v-for="(device, index) in equipments"
        :key="index"
      >
        <div class="deviceImage flexRowCenter">
          <img
            v-if="device.image"
            :src="$store.state.BASE_URL + device.image"
            alt=""
            class="equipmentImg"
          />
        </div>
        <div class="equipmentContent flexColumnSpaced">
          <h2 class="name">{{ device.name }}</h2>
          <p class="description">{{ device.description }}</p>
          <div class="options flexRowBottom">
            <img src="comentario.png" alt="" class="option" />
            <img src="deletar.png" alt="" class="option" @click="openModal()" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
<script>
import axios from "axios";
export default {
  name: "home",
  components: "Header",
  data() {
    return {
      equipments: [],
      display: false,
    };
  },
  methods: {
    getDevices: async function () {
      await axios
        .get(this.$store.state.BASE_URL + "/apiv1/devices/")
        .then((response) => {
          let data = response.data;
          this.equipments = data.data;
          console.log(this.equipments);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    openModal() {
      this.display = true;
    },
    closeModal() {
      this.display = false;
    },
  },
  mounted: async function () {
    this.getDevices();
  },
};
</script>

<style lang="scss" scoped>
.modal-overlay {
  position: fixed;
  background-color: #000000da;
}
.modal {
  text-align: center;
  background-color: white;
  height: 500px;
  width: 400px;
  .close {
    height: 30px;
    width: 30px;
    margin: 10px;
    border: 1px solid #000;
    cursor: pointer;
    .icon {
      font-size: 12pt;
      font-weight: bold;
    }
  }
  h2{
    font-weight: bold;
    font-size: 12pt;
    color: var(--dark);
  }
  p{
    font-size: 10pt;
  }
}

.homeContent {
  height: auto;
  padding: 60px 40px;
  background: var(--bodyBackground);
  .equipment {
    padding: 25px 0;
    border-bottom: 1px solid var(--dark);
    .deviceImage {
      height: 200px;
      width: 500px;
      background: #fff;
      img {
        height: 120px;
        width: auto;
      }
      border: 1px solid var(--dark);
    }
    .equipmentContent {
      margin: 0 10px;
      height: 200px;
      .name {
        height: auto;
        width: auto;
        margin-bottom: 10px;
        font-size: 12pt;
        color: var(--dark);
      }
      .description {
        height: auto;
        max-width: 900px;
        font-size: 10pt;
        font-weight: 200;
      }
      .options {
        .option {
          height: 30px;
          width: 30px;
        }
        height: auto;
        width: auto;
        img {
          cursor: pointer;
          margin-right: 15px;
        }
      }
    }
  }
}
</style>
