<template>
  <VCard class="card">
    <VResponsive :aspect-ratio="aspectRatio">
      <Chart
        class="chart"
        :theme="theme"
        :autoresize="true"
        :options="siteOptions"
        style="width:100%;height:100%"
      />
    </VResponsive>
  </VCard>
</template>

<script>
import drawSitePlay from "../../charts/site_play.js";
export default {
  props: { siteData: Object() },
  data() {
    return {
      siteOptions: Object(),
      theme: "colorful"
    };
  },
  computed: {
    isDark() {
      return this.$store.state.dark;
    },
    aspectRatio() {
      if (document.body.clientWidth <= 600) {
        return 5 / 3;
      } else {
        return 8 / 3;
      }
    }
  },
  watch: {
    isDark(val) {
      if (val) {
        this.theme = "mydark";
      } else {
        this.theme = "colorful";
      }
    },
    siteData: function(val) {
      this.siteData = val;
      this.siteOptions = drawSitePlay(val);
    }
  },
  mounted() {
    if (this.$store.state.dark) {
      this.theme = "mydark";
    } else {
      this.theme = "colorful";
    }
  }
};
</script>

<style scoped>
.video-img {
  height: 70px;
  border-radius: 4px;
}
.chart {
  height: 25vmax;
}
@media only screen and (max-width: 1029px) {
  .chart {
    height: 60vmin;
  }
}
</style>
