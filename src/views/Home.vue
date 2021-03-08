<template>
  <v-main>
    <v-title> 镜湖 - lte.ldwid.com </v-title>
    <v-row no-gutters>
      <!-- color-picker -->
      <v-col :cols="$vuetify.breakpoint.mdAndUp ? 6 : 12">
        <color-picker></color-picker>
      </v-col>
      <!-- preview-zone -->
      <v-col :cols="$vuetify.breakpoint.mdAndUp ? 6 : 12">
        <preview-zone></preview-zone>
      </v-col>
    </v-row>
  </v-main>
</template>

<script>
import VTitle from "../components/title";
import ColorPicker from "../components/ColorPicker";
import PreviewZone from "../components/PreviewZone";
export default {
  data: () => ({}),
  methods: {},
  components: {
    VTitle,
    ColorPicker,
    PreviewZone
  }
};
</script>

<style lang="scss">
</style>
