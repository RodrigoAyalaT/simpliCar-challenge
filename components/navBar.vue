<template>
  <div>
    <nav class="navbar p-0 navbar-expand-lg navbar-light bg-transparent">
      <div class="shadow-lg container-fluid p-0">
        <a class="navbar-brand p-0" href="">
          <img
            src="~/assets/logo.jpg"
            alt=""
            width="100"
          />
        </a>
        <b-button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </b-button>

        <div
          class="collapse navbar-collapse col-8 p-2"
          id="navbarSupportedContent" 
        >
          <ul class="navbar-nav nav-link me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active fw-bold" aria-current="page" href="store">Vehículos</a>
            </li>
            <li class="nav-item">
              <a class="nav-link SFDisplay-bold" href="#">Descubrí Nissan</a>
            </li>
          </ul>
          <div class="col-4 d-flex justify-content-end">
            <form class="d-flex">
              <input
                id="search"
                class="form-control me-2"
                type="search"
                placeholder="BUSCAR POR MODELO O VEHÍCULO"
                aria-label="Search"
              />
            </form>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>
<style>
input#search{
    background-image: url(assets/search.svg);
    background-repeat: no-repeat;
    background-position: 15px;
    border: none;
    border-radius: 10px;
    background-color: hsla(0,0%,100%,.8);
    width: 323px;
    height: 60px;
    float: right;
    padding-left: 50px;
    padding-right: 50px;
    font-size: 13px;
}

</style>