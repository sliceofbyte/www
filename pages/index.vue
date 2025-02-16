<template>
  <main class="min-h-screen relative">
    <hero />
    <github />
    <section
      class="relative mx-auto max-w-5xl px-4 sm:px-6 lg:px-8 overflow-hidden"
    >
      <post v-for="post in data" :content="post" />
    </section>
  </main>
</template>

<script setup>
import seo from "../seo/index";
useHead({
  title: seo.title,
  meta: [
    {
      name: "description",
      content: seo.description,
      meta: [
        { name: "og:title", content: seo.og.title },
        { name: "og:description", content: seo.og.description },
        { name: "og:image", content: seo.og.image },
        { name: "og:url", content: seo.og.url },
        { name: "twitter:title", content: seo.og.title },
        { name: "twitter:description", content: seo.og.description },
        { name: "twitter:image", content: seo.og.image },
        { name: "twitter:card", content: "summary_large_image" },
      ],
    },
  ],
});
const { data } = await useAsyncData("feed", () =>
  queryContent("/posts").find()
);
</script>
