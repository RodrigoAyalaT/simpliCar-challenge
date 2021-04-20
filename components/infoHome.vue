<template>
  <div class="col-12">
    <div class="pa">
      <div class="col-12">
        <h1 class="title text-danger fw-bold">AHORA ES ONLINE.</h1>
      </div>
      <div class="col-7">
        <p class="description font-monospaced">
          Con Nissan Store, podés acceder a tu nuevo 0km con todos los servicios
          asociados desde la comunidad de tu sofá. Probanos!.
        </p>
      </div>
    </div>
    <div class="pa2 mg d-grid gap-2 col-5">
      <b-button
        class="btn btn-danger btn-lg text-uppercase text-start bg-arrow"
        onclick="location.href='/store'"
        >Ingresa a Nissan Store</b-button
      >
    </div>
  </div>
</template>
<style>
.pa {
  padding-top: 140px;
  padding-left: 140px;
}
.pa2 {
  padding-left: 140px;
}

.description {
  font-size: 25px;
  color: #343434;
  font-weight: 300;
}
.title {
  font-size: 60px;
  padding: 0;
}
.mg {
  margin-top: 53px;
}
.bg-arrow {
  background-image: url(~/assets/arrow-right.svg);
  background-position: left;
  background-repeat: no-repeat;
  background-position: 300px;
  color: #fff;
  font-weight: 500;
  height: 60px;
  width: 350px;
  border-radius: 10px;
  border: none;
  margin-top: 53px;
  text-align: left;
  padding-left: 40px;
}
</style>