<template>
  <v-carousel
    height="95vh"
    :cycle="config.auto"
    :interval="config.interval"
    :hide-controls="config.auto"
    :hide-delimiters="config.auto"
  >
    <v-carousel-item
      v-for="i in 3"
      :key="i"
      :src="`https://picsum.photos/500/300?image=${i * 15 + 10}`"
    >
      <v-card color="blue-grey darken-1" class="white--text">
        <v-card-title primary-title>
          <div>
            <div class="headline">{{ "Titulo " + parentLabel + i }}</div>
            <span>{{ "Subtitulo " + parentLabel + i }}</span>
          </div>
        </v-card-title>
      </v-card>
    </v-carousel-item>
  </v-carousel>
</template>

<script>
export default {
  name: "CarouselD",
  props: {
    config: {
      type: Object,
      default() {
        return {
          auto: true,
          interval: 5000
        };
      }
    },
    parentLabel: {
      type: String,
      default: ""
    }
  }
};
</script>
