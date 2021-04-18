<template>
  <div class="containerGallery">
    <div v-if="carList">
      <div class="row justify-content-center mt-5">
        <div
          class="card shadow m-3 text-center"
          style="width: 20rem"
          v-for="car in carList.results"
          :key="car.id"
        >
          <h5 class="card-title title-font text-uppercase pt-3">
            nissan {{ car.model }}
          </h5>
          <div class="col-12">
            <img
              class="card-img-top"
              :src="
                'https://s3.sa-east-1.amazonaws.com/simplimotos-stg.com/' +
                car.gallery[0].large
              "
            />
          </div>

          <div class="card-body">
            <hr />
            <h6 class="text-muted card-subtitle">Precio desde:</h6>
            <span class="text-uppercase text-success fw-bold"
              >{{ car.amount }}{{ car.currency }}
            </span>

            <hr />
            <div class="row text-uppercase fw-bold">
              <div class="col-4">
                {{ car.detail.characteristics.engine }}
              </div>
              <div class="col-4">{{ car.specs.technical_details.body }}</div>
              <div class="col-4">{{ car.detail.characteristics.gas_type }}</div>
            </div>
            <div class="card-text text-muted description mt-1">
              <small class="text-left" widht="20px">{{
                car.detail.description
              }}</small>
            </div>
            <div class="card-text">
              <button
                class="btn btn-outline-danger mt-3"
                onclick="location.href='/detail'"
              >
                Mostrar detalle y cotización.
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

export default {
  name: "carGallery",
  data() {
    return { carList: null };
  },
  mounted() {
    this.fetchCars();
  },
  methods: {
    async fetchCars() {
      this.carList = await this.$axios.$get(
        "https://4my1q6hsyo.api.quickmocker.com/product",
        {
          headers: {
            Accept: "application/json",
            Authorization: "Bearer qwertyuiopasdfghjklzxcvbnm123456",
          },
        }
      );
      console.log(this.carList);
    },
  },
};
</script>
<style>
.containerGallerry {
  margin-top: 100px;
}
.description {
  height: 120px;
}
.card {
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.08), 0 0 6px rgba(0, 0, 0, 0.05);
  transition: 0.3s transform cubic-bezier(0.155, 1.105, 0.295, 1.12),
    0.3s box-shadow,
    0.3s -webkit-transform cubic-bezier(0.155, 1.105, 0.295, 1.12);
  cursor: pointer;
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.12), 0 4px 8px rgba(0, 0, 0, 0.06);
}
.title-font {
  font-family: SFDisplay;
}
</style>