<script setup>
import { computed } from "vue";
import { useRoute, useRouter } from "vue-router";
import { Back } from "@element-plus/icons-vue";
import { ROUTES_PATHS } from "@/constants";

const props = defineProps({
  imgUrl: {
    type: String,
    required: true,
  },
  backFunc: {
    type: Function,
  },
  isBackButtonVisible: {
    type: Boolean,
    default: true,
  },
});

const route = useRoute();
const router = useRouter();

const routeName = computed(() => route.name);

function goForCocktailRandom() {
  router.push(ROUTES_PATHS.COCKTAIL_RANDOM);

  if (routeName.value === ROUTES_PATHS.COCKTAIL_RANDOM) {
    router.go();
  }
}

function goBack() {
  props.backFunc ? props.backFunc() : router.go(-1);
}
</script>

<template>
  <div class="root">
    <div :style="`background-image: url(${imgUrl})`" class="img"></div>
    <div class="main">
      <div class="btns">
        <el-button
          v-if="isBackButtonVisible"
          type="primary"
          :icon="Back"
          circle
          class="back"
          @click="goBack"
        />
        <el-button class="btn" @click="goForCocktailRandom"
          >Get random cocktail</el-button
        >
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'

.root
  display: flex
  min-height: 100vh
  background-color: $background

.img
  width: 50%
  background-repeat: no-repeat
  background-position: 50% 50%
  background-size: cover

.main
  position: relative
  width: 50%
  padding: 32px 40px

.btn
  position: absolute
  top: 32px
  right: 40px
  font-size: 16px
  font-family: 'Raleway', 'Arial', sans-serif
  background-color: $accent
  border-color: $accent
  color: $text

  &:hover,
  &:active
    background-color: darken($accent, 10%)
    border-color: darken($accent, 10%)

.btns
  display: flex
  justify-content: space-between
  align-items: center

.back
  background-color: transparent
  border-color: #fff

  &:hover
    border-color: $accent
</style>
