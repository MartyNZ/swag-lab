<script setup>
const route = useRoute();
const fullPath = route.fullPath;
// console.log(fullPath)

const isPromoPage = ref(false);
const path = fullPath.split("/");
for (let i = 0; i < path.length; i++) {
  if (path[i] === "promotions") { isPromoPage.value = true; }
}
const showPromoBanner = ref(true);
if (fullPath === '/' || isPromoPage.value) {
  showPromoBanner.value = false;
}
</script>
<template>
  <header
    class="bg-surface-200 shadow-surface-400 dark:bg-surface-800 dark:shadow-surface-700 sticky top-0 z-30 shadow-sm">
    <div class="bg-surface-700 w-full">
      <div class="mx-auto flex max-w-[1280px] flex-wrap items-center justify-between px-2 py-2 md:px-4 text-surface-50">
        <AppBrand />
        <div class="flex items-center justify-end gap-1 md:gap-3">
          <app-header-navigation />
          <product-cart-summary />
          <AppColorMode />
        </div>
      </div>
    </div>
    <div v-if="showPromoBanner" class="bg-surface-950 text-primary-50 w-full ">
      <div class="flex max-h-min max-w-[1280px] place-content-center">
        <a href="#subscribe" class="hover:text-surface-0 my-2 text-xs sm:text-base">
          <span
            class="after:bg-primary-700 relative after:absolute after:-bottom-[5px] after:left-0 after:h-[3px] after:w-[0%] after:rounded-xl after:duration-300 after:content-[''] hover:after:w-[100%]">
            Get 15% off your first purchase
          </span>
        </a>
      </div>
    </div>
  </header>
</template>
