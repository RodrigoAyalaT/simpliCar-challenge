<template>
  <div class="containerDetail">
    <div v-if="getCar" class="row g-0 pt-5">
      <div class="col-6 p-3">
        <div class="col-12">
          <b-carousel
            id="carousel-1"
            v-model="slide"
            :interval="5000"
            controls
            img-width="1024"
            img-height="480"
          >
            <div v-for="image in getCar.gallery" :key="image.id">
              <div class="">
                <b-carousel-slide
                  :img-src="
                    'https://s3.sa-east-1.amazonaws.com/simplimotos-stg.com/' +
                    image.large
                  "
                >
                </b-carousel-slide>
              </div>
            </div>
          </b-carousel>
        </div>
        <table class="d-none d-md-table table text-muted text-center">
          <thead>
            <tr class="">
              <th scope="col">Clase</th>
              <th scope="col">Caracteristicas</th>
              <th scope="col">Transmisión</th>
              <th scope="col">Colores</th>
            </tr>
          </thead>
          <tbody>
            <tr class="fw-bold m-0 p-0">
              <td>
                <ul class="list-group list-group-flush">
                  <li class="list-group-item">{{ getCar.specs.technical_details.body }}</li>
                  <li></li>
                </ul>
              </td>
              <td>
                <ul class="list-group list-group-flush">
                  <li
                    class="list-group-item"
                    v-for="feature in getCar.specs.technical_details.features.split(
                      ';'
                    )"
                    :key="feature.id"
                  >
                    {{ feature }}
                  </li>
                </ul>
              </td>
              <td>
                <ul class="list-group list-group-flush">
                  <li class="list-group-item">{{ getCar.specs.technical_details.transmission}}</li>
                  <li></li>
                </ul>
              </td>
              <td>
                <ul class="list-group list-group-flush">
                  <li v-for="color in getCar.detail.colors" :key="color.id" class="list-group-item">
                    <div class="vehicle-color" :style="'background-color:#'+color.hex+';'">
                    </div>
                  </li>
                </ul>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div v-if="message === null" class="col-6 p-5">
        <form class="row g-0 p-5">
          <h4>
            Solicitá una cotización completa de este Nissan {{ getCar.model }}
          </h4>
          <div class="col-12 m-1">
            <input
              v-model="formInf.fullname"
              type="text"
              placeholder="Nombre y Apellido"
              class="form-control"
              name="fullname"
              id="fullname"
              required
            />
          </div>
          <div class="col-12 m-1">
            <input
              v-model="formInf.email"
              type="email"
              placeholder="Correo Electrónico"
              class="form-control"
              name="email"
              id="email"
              required
            />
          </div>
          <div class="col-12 m-1">
            <input
              v-model="formInf.phone"
              type="text"
              placeholder="Teléfono"
              class="form-control"
              name="phone"
              id="phone"
              required
            />
          </div>
          <div class="col-12 d-grid gap-2 m-1">
            <b-button @click="sendInf()" size="lg" class="bg-danger">Enviar Cotización por E-Mail</b-button>
          </div>
        </form>
      </div>
      <div v-else class="col-6 p-4">
        <b-card class="bg-success text-white shadow">{{message}}</b-card>
      </div>
    </div>
    <b-overlay v-else :show="show">
      <div class="hg"></div>
       </b-overlay>
  </div>
</template>
<style>
.containerDetail {
  min-height: 800px;
  background: #fff;
}
span {
  display: none;
}
.carousel-control-next-icon {
  background-color: red;
}
.carousel-control-prev-icon {
  background-color: red;
}
.pa {
  margin-top: 100px;
  margin-left: 100px;
}
.vehicle-color{
  width: 25px;
  height: 25px;
  border-radius: 50%;
}
.list-item{
  height: 25px;
}
</style>
<script>
export default {
  computed: {
    carId() {
      return this.$route.params.id;
    },
    getCar() {
      if (this.carList === null) {
        return null;
      }
      return this.carList.results.find((item) => item.id === this.carId);
    },
    getDetails() {
      return this.getCar.detail;
    },
    getFeatureList() {
      this.featureList = this.getCar.specs.technical_details.features
        .split(";")
        .map((feat) => {
          return <li key={feat}>{feat}</li>;
        });
    },
  },
  data() {
    return {
      carList: null,
      slide: 0,
      sliding: null,
      show: false,
      featureList: null,
      formInf:{
        fullname:'',
        email:'',
        phone:'',
      },
      getFormInf:null,
      message:null,
    };
  },
  mounted() {
    this.fetchCars();
  },
  methods: {
    async fetchCars() {
      this.show = true;
      this.carList = await this.$axios.$get(
        "https://4my1q6hsyo.api.quickmocker.com/product/",
        {
          headers: {
            Accept: "application/json",
            Authorization: "Bearer qwertyuiopasdfghjklzxcvbnm123456",
          },
        }
      );
      this.show = false;
    },
    async sendInf(){
      this.getFormInf = await this.$axios.$post(
        "https://4my1q6hsyo.api.quickmocker.com/lead",
        {
          headers: {
            Accept: "application/json",
            Authorization: "Bearer qwertyuiopasdfghjklzxcvbnm123456",
          },
          data:this.formInf,
        }
      );
      this.message = this.getFormInf.msg
      console.log(this.getFormInf)
    }
  },
};
</script>