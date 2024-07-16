<template>
  <header id="darkModeHeader" class="header-area bg-white mb-4">
    <div class="container-fluid">
      <div class="row align-items-center">
        <div class="col-lg-6 col-md-7">
          <div class="left-header-content">
            <ul
              class="d-lg-flex d-md-flex align-items-center ps-0 mb-0 list-unstyled"
            >
              <li class="mb-3 mb-md-0 mb-lg-0">
                <div
                  class="d-flex justify-content-between align-items-center cw-273"
                >
                
                  <router-link to="/" class="flex-shrink-0">
                    <img
                      src="../../assets/images/logo.png"
                      class="main-logo"
                      alt="main-logo"
                    />
                    <img
                      src="../../assets/images/white-logo.png"
                      class="d-none white-logo"
                      alt="white-logo"
                    />
                  </router-link>
                  <div>
                    <button
                      class="border-0 p-0 bg-transparent js-sidebar-expand flex-grow-1 ms-3 text-sm-end menu-bergur"
                      @click="stateStoreInstance.onChange"
                    >
                      <div
                        id="closeBtn"
                        @click="toggleButtonVisibility('openBtn')"
                        v-show="showOpenBtn"
                      >
                        <vue-feather type="menu"></vue-feather>
                      </div>
                      <div
                        id="openBtn"
                        @click="toggleButtonVisibility('closeBtn')"
                        v-show="showCloseBtn"
                      >
                        <vue-feather type="x"></vue-feather>
                      </div>
                    </button>
                  </div>
                </div>
              </li>
              <li class="d-none d-lg-block d-md-none">
                <h3 class="mb-0">Maestra SHF</h3>
              </li>
            </ul>
          </div>
        </div>

        <div class="col-lg-6 col-md-5">
          <div class="float-lg-end float-md-end">
            <ul
              class="right-header-content list-unstyled d-flex justify-content-lg-end justify-content-md-end justify-content-center align-items-center mb-0 ps-0"
            >
              <li>
                <div class="dropdown date">
                  <button
                    class="btn bg-transparent p-0 border-0 p-0 position-relative badge"
                    type="button"
                    data-bs-toggle="dropdown"
                    aria-expanded="false"
                  >
                    <vue-feather class="t-0" type="calendar"></vue-feather>
                  </button>
                  <div class="dropdown-menu dropdown-lg p-0 rounded-0 border-0">
                    <div class="today-date">
                      <span class="fw-medium">{{ formattedDate }}</span>
                      <vue-feather type="calendar"></vue-feather>
                    </div>
                  </div>
                </div>
              </li>

              <li>
                <div class="dropdown user-profile">
                  <a
                    href="#"
                    class="d-flex align-items-center user-control text-decoration-none"
                    data-bs-toggle="dropdown"
                    aria-expanded="false"
                  >
                   
                    <div class="flex-grow-1 ms-3">
                      <div class="d-flex align-items-center justify-content-between">
                        <div class="me-5 d-none d-lg-block">
                          <h3 id="java_spring_nombre">{{ JSspr_name }}</h3>
                          <span id="java_spring_permisions">{{ JSspr_details }}</span>
                        </div>
                      </div>
                    </div>
                  </a>

                  <ul class="dropdown-menu border-0 box-shadow rounded-0">
                    <li class="me-0">
                      <router-link
                        class="dropdown-item d-flex align-items-center text-body"
                        to="/log-out"
                      >
                        <vue-feather
                          type="log-out"
                          class="text-primary"
                        ></vue-feather>
                        <span class="ms-2 text-dark">Logout</span>
                      </router-link>
                    </li>
                  </ul>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import stateStore from "../../utils/store";


export default defineComponent({
  name: "MainHeader",
  data() {
    return {
      showOpenBtn: true,
      showCloseBtn: false,
      JSspr_details:'',
      JSspr_name:'',
    };
  },
  methods: {
    toggleButtonVisibility(buttonId: string) {
      if (buttonId === "openBtn") {
        this.showOpenBtn = false;
        this.showCloseBtn = true;
        
      } else if (buttonId === "closeBtn") {
        this.showOpenBtn = true;
        this.showCloseBtn = false;
        
      }
    },
  },
  mounted() {
    let detalle = document.getElementById("spr_details");
    let name = document.getElementById("spr_name");
    
    if (detalle) {
      this.JSspr_details = detalle.getAttribute("data-message");
      
    }
    if (name) {
      this.JSspr_name = name.getAttribute("data-message");
    }    
    

  },
  setup() {
    
    const stateStoreInstance = stateStore;

    const formattedDate = ref("");

    

    onMounted(() => {
      const months = [
        "Enero",
        "Febrero",
        "Marzo",
        "Abril",
        "Mayo",
        "Junio",
        "Julio",
        "Agosto",
        "Septiembre",
        "Octubre",
        "Noviembre",
        "Diciembre",
      ];

      const currentDate = new Date();
      

      formattedDate.value = `${currentDate.getDate()} ${
        months[currentDate.getMonth()]
      } ${currentDate.getFullYear()}`;
    });

    return {
      stateStoreInstance,
      formattedDate,
    };
  },
});
</script>