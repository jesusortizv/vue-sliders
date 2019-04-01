<template>
  <v-container grid-list-md text-xs-center fluid fill-height>
    <v-layout row wrap>
      <v-flex v-for="(area, i) in areas" :key="`6${i}`" xs6 d-flex>
        <v-card
          class="center-aligned clickable"
          :color="`${area.color} lighten-4`"
          @click="selectArea(area)"
        >
          <v-card-title primary class="headline font-weight-bold">{{
            area.label
          }}</v-card-title>
        </v-card>
      </v-flex>
      <v-dialog
        v-model="showDialog"
        persistent
        fullscreen
        transition="scale-transition"
        origin="center center"
        hide-overlay
      >
        <v-toolbar dark>
          <v-spacer></v-spacer>
          <v-btn icon @click="toggleDialog()" dark>
            <v-icon>close</v-icon>
          </v-btn>
        </v-toolbar>
        <component
          :is="selectedArea.carousel"
          :config="selectedArea.displayConfig"
          :parent-label="selectedArea.label"
        ></component>
      </v-dialog>
    </v-layout>
  </v-container>
</template>

<script>
import CarouselA from "@/components/CarouselA.vue";
import CarouselB from "@/components/CarouselB";
import CarouselC from "@/components/CarouselC";
import CarouselD from "@/components/CarouselD";

export default {
  name: "Areas",
  data() {
    return {
      selectedArea: {},
      showDialog: false,
      areas: [
        {
          label: "A",
          color: "green",
          carousel: CarouselA,
          displayConfig: {
            auto: false
          }
        },
        {
          label: "B",
          color: "light-blue lighten-4",
          carousel: CarouselB,
          displayConfig: {
            auto: true,
            interval: 4000
          }
        },
        {
          label: "C",
          color: "yellow lighten-4",
          carousel: CarouselC,
          displayConfig: {
            auto: true,
            interval: 6000
          }
        },
        {
          label: "D",
          color: "red lighten-4",
          carousel: CarouselD,
          displayConfig: {
            auto: false
          }
        }
      ]
    };
  },
  methods: {
    selectArea(area) {
      this.selectedArea = area;
      this.toggleDialog();
    },
    toggleDialog() {
      this.showDialog = !this.showDialog;
    }
  }
};
</script>

<style scoped>
.center-aligned {
  display: flex;
  justify-content: center;
}
.clickable {
  cursor: pointer;
}
</style>
