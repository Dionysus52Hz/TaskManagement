<template>
   <div>
      <NuxtLayout name="mobile-default">
         <template #header> </template>

         <div class="flex flex-col introduce p-4 bg-[#F9CE60]">
            <h1 class="font-black text-[32px] text-center mb-2">
               Organize & track your work!
            </h1>

            <h2 class="text-xl text-center mb-6">
               Keep everything in the same place—even if your team isn’t.
            </h2>

            <Button class="text-base py-6">Sign up - it's free</Button>

            <div class="w-full aspect-square bg-gray-200 mt-8">
               <!-- Place photo here -->
            </div>
         </div>

         <div class="">
            <div class="p-4 grid">
               <p class="uppercase font-medium mb-2">Lorem ipsum</p>
               <h2 class="text-2xl font-medium mb-4">A productivity tool</h2>
               <p class="text-xl">
                  Simple, flexible, and powerful. All it takes are boards,
                  lists, and cards to get a clear view of who's doing what and
                  what needs to get done.
               </p>
            </div>

            <div
               class="w-full flex flex-col justify-center items-center p-4 gap-y-4"
            >
               <Carousel
                  class="relative w-full"
                  @init-api="(val) => (emblaMainApi = val)"
               >
                  <CarouselContent>
                     <CarouselItem
                        v-for="(_, index) in 5"
                        :key="index"
                     >
                        <div class="p-1">
                           <Card>
                              <CardContent
                                 class="flex aspect-square items-center justify-center p-6"
                              >
                                 <span class="text-4xl font-semibold">{{
                                    index + 1
                                 }}</span>
                              </CardContent>
                           </Card>
                        </div>
                     </CarouselItem>
                  </CarouselContent>
               </Carousel>

               <Carousel
                  class="relative w-full"
                  @init-api="(val) => (emblaThumbnailApi = val)"
               >
                  <CarouselContent class="flex gap-1 ml-0">
                     <CarouselItem
                        v-for="(_, index) in 5"
                        :key="index"
                        class="pl-0 cursor-pointer"
                     >
                        <div class="p-1">
                           <Card class="overflow-hidden">
                              <CardContent class="flex items-center p-0">
                                 <div
                                    class="overflow-hidden relative h-full p-4 pl-6 after:bg-emerald-600 after:w-2 after:absolute after:block after:top-0 after:bottom-0 after:left-0"
                                 >
                                    <h3 class="mb-2 font-medium">
                                       Lorem ipsum
                                    </h3>
                                    <p>
                                       Lorem ipsum dolor sit amet consectetur
                                       adipisicing elit. Repudiandae expedita
                                       sunt mollitia fuga tempore corrupti
                                       harum, ut esse dignissimos deleniti
                                       veritatis quis accusantium delectus dicta
                                       pariatur alias necessitatibus id hic!
                                    </p>
                                 </div>
                              </CardContent>
                           </Card>
                        </div>
                     </CarouselItem>
                  </CarouselContent>
               </Carousel>

               <div class="flex gap-x-2">
                  <span
                     v-for="(_, index) in 5"
                     :key="index"
                     class="abc block rounded-full h-2 w-2"
                     :class="
                        index === selectedIndex
                           ? 'w-[60px] bg-black'
                           : 'bg-gray-400'
                     "
                     @click="onCarouselDotClick(index)"
                  ></span>
               </div>
            </div>
         </div>

         <div class="px-4 py-[48px] grid justify-center gap-y-6 bg-fuchsia-800">
            <h2 class="text-2xl font-semibold text-white">
               Get started with our tool today
            </h2>
            <Button class="text-base py-6">Sign up - it's free</Button>
         </div>
      </NuxtLayout>
   </div>
</template>

<script setup lang="ts">
   definePageMeta({
      layout: false,
   });

   import { Button } from '~/components/ui/button';
   import { Card, CardContent } from '@/components/ui/card';
   import {
      Carousel,
      CarouselContent,
      CarouselItem,
      CarouselNext,
      CarouselPrevious,
      type CarouselApi,
   } from '@/components/ui/carousel';
   import { watchOnce } from '@vueuse/core';

   const emblaMainApi = ref<CarouselApi>();
   const emblaThumbnailApi = ref<CarouselApi>();
   const selectedIndex = ref(0);

   const onMainSelect = () => {
      if (!emblaMainApi.value || !emblaThumbnailApi.value) return;
      selectedIndex.value = emblaMainApi.value.selectedScrollSnap();
      emblaThumbnailApi.value.scrollTo(emblaMainApi.value.selectedScrollSnap());
   };

   const onThumbnailSelect = () => {
      if (!emblaMainApi.value || !emblaThumbnailApi.value) return;
      selectedIndex.value = emblaThumbnailApi.value.selectedScrollSnap();
      emblaMainApi.value.scrollTo(emblaThumbnailApi.value.selectedScrollSnap());
   };

   const onCarouselDotClick = (index: number) => {
      if (!emblaMainApi.value || !emblaThumbnailApi.value) return;
      emblaMainApi.value.scrollTo(index);
      emblaThumbnailApi.value.scrollTo(index);
   };

   watchOnce(emblaMainApi, (emblaMainApi) => {
      if (!emblaMainApi) return;

      onMainSelect();
      emblaMainApi.on('select', onMainSelect);
      emblaMainApi.on('reInit', onMainSelect);
   });

   watchOnce(emblaThumbnailApi, (emblaThumbnailApi) => {
      if (!emblaThumbnailApi) return;

      onThumbnailSelect();
      emblaThumbnailApi.on('select', onThumbnailSelect);
      emblaThumbnailApi.on('reInit', onThumbnailSelect);
   });
</script>

<style scope>
   .abc {
      transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
   }
</style>
