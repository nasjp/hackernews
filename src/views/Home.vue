<template>
  <div class="home">
    <News />
  </div>
</template>

<script>
// @ is an alias to /src
import News from "@/components/News.vue";

export default {
  name: "home",
  components: {
    News
  }
};
</script>
