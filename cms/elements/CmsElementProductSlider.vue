<template>
  <div class="cms-element-product-slider">
    <SfSection :title-heading="title" class="section">
      <SfCarousel ref="carousel" class="product-carousel" :settings="options">
        <SfCarouselItem
          v-for="product in products"
          :key="product.id"
          class="product-carousel__item"
        >
          <SwProductCard :product="product" class="product-carousel__product" />
        </SfCarouselItem>
      </SfCarousel>
    </SfSection>
  </div>
</template>

<script>
import { SfSection, SfCarousel } from "@storefront-ui/vue"
import SwProductCard from "@/components/SwProductCard.vue"

export default {
  name: "CmsElementProductSlider",
  components: {
    SfSection,
    SfCarousel,
    SwProductCard,
  },
  props: {
    content: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {
    products() {
      return this.content && this.content.data ? this.content.data.products : []
    },
    title() {
      return this.content &&
        this.content.config &&
        this.content.config.title.value
        ? this.content.config.title.value
        : ""
    },
  },
  data() {
    return {
      options: {
        peek: 16,
        breakpoints: {
          480: {
            perView: 1,
            peek: {
              before: 0,
              after: 3,
            },
          },
          1023: {
            peek: 0,
            perView: 3,
          },
        },
      },
    }
  },
  beforeDestroy() {
    if (this.$refs.carousel.glide) {
      this.$refs.carousel.glide.destroy();
    }
  }
}
</script>

<style lang="scss" scoped>
@import "@/cms/settings.scss";

.product-carousel {
  margin: 0 calc(-1 * var(--spacer-sm)) 0 0;
  @include for-desktop {
    margin: 0;
  }
  &__item {
    margin: 1.9375rem 0 2.4375rem 0;
  }
}
</style>
