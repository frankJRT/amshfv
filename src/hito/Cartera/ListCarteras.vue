<template>
  <div class="container-fluid">
    <div class="inner-main-content">
      <AllCarteras />
      <MainFooter />
    </div>
  </div>
</template>


<script lang="ts">

import { defineComponent } from "vue";
import AllCarteras from "../components/CateraComponent/AllCarteras.vue";
import MainFooter from "../../components/Layouts/MainFooter.vue";

export default defineComponent({
  name: "ListCarteraPage",
  components: {
    AllCarteras,
    MainFooter,
  },
});

</script>

<style lang="scss" scoped>

</style>