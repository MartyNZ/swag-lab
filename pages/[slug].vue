<script setup>
import { qryPage } from "~/queries/siteSettings";
const route = useRoute();
const slug = route.params.slug;
const { data: page } = await useSanityQuery(qryPage, { slug: slug });
const data = useSiteSettingsStore();
const settings = data.settings;

useSeoMeta({
  title: () => page.value.title,
  description: () => page.value.description,
  ogTitle: () => page.value.title,
  ogDescription: () => page.value.description,
  ogImage: () => settings.image,
  twitterTitle: () => page.value.title,
  twitterDescription: () => page.value.description,
  twitterImage: () => settings.image,
  twitterCard: "summary_large_image",
});

defineOgImageComponent(
  'default',
  {
    title: settings.title,
    description: settings.description,
    image: settings.image,
    siteName: settings.title,
    siteLogo: settings.logoUrl,
  });

definePageMeta({
  layout: false,
});
</script>

<template>
  <div>
    <NuxtLayout name="default">
      <template #main>
        <section class="content surface-section px-6 pb-20 pt-4 md:px-12 lg:px-20">
          <div v-for="section in page.sections" :key="section._id">
            <template v-if="section._type != 'policy'">
              <div>{{ section._type }}</div>
            </template>
            <app-policy v-else :section="section" />
            <!-- <component :is="section._type" :section="section" /> -->
          </div>
        </section>
      </template>
      <template #sidebar>
        <product-sidebar />
      </template>
    </NuxtLayout>
  </div>
</template>
