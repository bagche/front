<script setup lang="ts">
useHead({
  title: "دسته‌بندی‌ها",
});
const { data }: any = useAsyncData("category", () =>
  queryContent("category").find()
);
</script>
<template>
  <section class="flex flex-col">
    <ContentDoc v-slot="{ doc }" path="/pages/category">
      <LazyBasePageIntro :data="doc" />
    </ContentDoc>

    <div class="w-full grid grid-cols-3 gap-10 align-middle mt-0">
      <UCard
        v-for="cat in data"
        :key="cat._path"
        class="w-full max-h-[30rem]"
        :ui="{
          base: '',
          ring: '',
          shadow: '',
          divide: 'divide-y divide-gray-200 dark:divide-gray-700',
          header: { padding: 'p-0' },
          body: {
            padding: 'sm:px-10',
            base: ' divide-gray-200 dark:divide-gray-700 text-s',
          },
          footer: { padding: 'p-4' },
        }"
      >
        <template #header>
          <div class="flex">
            <nuxt-img
              v-if="cat?.thumbnail"
              preload
              loading="lazy"
              sizes="sm:100vw md:50vw lg:80px"
              class="flex max-h-[7rem]"
              :src="cat?.thumbnail"
              :alt="cat?.title"
              :width="80"
              height="auto"
            />
            <div>
              <h3
                class="font-semibold text-sm  leading-tight hover:underline"
              >
                <NuxtLink :to="cat._path" class="">
                  # {{ cat.title }}
                </NuxtLink>
              </h3>

              <p
                class="font-thin text-s  leading-tight"
              >
                <ContentRenderer :value="cat" class="content" />
              </p>
            </div>
          </div>
        </template>
        <LazyBaseLatestItems :category="cat.name" />
      </UCard>
    </div>
  </section>
</template>
