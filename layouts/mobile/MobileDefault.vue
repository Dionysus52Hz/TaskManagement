<template>
   <div>
      <header class="h-[70px] fixed top-0 z-[100]">
         <slot name="header">
            <Sheet>
               <div
                  class="px-4 items-center fixed flex top-0 w-full h-[70px] z-[1000] justify-between shadow bg-white"
                  @click="console.log(123)"
               >
                  <span class="bg-gray-200 h-[38px] aspect-square"></span>
                  <SheetTrigger as-child>
                     <Button
                        variant="outline"
                        size="icon"
                     >
                        <AlignCenter class="w-5 h-5" />
                     </Button>
                  </SheetTrigger>
               </div>

               <SheetContent
                  side="top"
                  class="pt-[70px] z-[50]"
               >
                  <div class="pt-0">
                     <Accordion
                        type="single"
                        class="w-full"
                        collapsible
                     >
                        <AccordionItem
                           v-for="item in accordionItems"
                           :key="item.value"
                           :value="item.value"
                        >
                           <AccordionTrigger>{{ item.title }}</AccordionTrigger>
                           <AccordionContent>
                              {{ item.content }}
                           </AccordionContent>
                        </AccordionItem>
                     </Accordion>

                     <div class="grid gap-y-4 mt-4">
                        <Button>Get for free</Button>
                        <Button variant="outline">Log in</Button>
                     </div>
                  </div>
               </SheetContent>
            </Sheet>
         </slot>
      </header>

      <main class="mt-[70px]">
         <slot />
      </main>

      <footer class="bg-blue-950">
         <section class="grid text-white px-4">
            <div class="flex justify-between mx-4 mt-6">
               <div class="w-[125px] h-10 bg-gray-200"></div>
               <Button variant="ghost">Log In</Button>
            </div>
            <ul class="mx-4">
               <li class="first:border-y first:my-4 first:py-4">
                  <h3 class="pb-2">About</h3>
                  <p class="text-sm">What's behind our tool.</p>
               </li>
               <li class="pb-4 mb-4 border-b">
                  <h3 class="pb-2">About</h3>
                  <p class="text-sm">What's behind our tool.</p>
               </li>
               <li class="pb-4 mb-4 border-b">
                  <h3 class="pb-2">About</h3>
                  <p class="text-sm">What's behind our tool.</p>
               </li>
               <li class="pb-4 mb-4 border-b">
                  <h3 class="pb-2">About</h3>
                  <p class="text-sm">What's behind our tool.</p>
               </li>
            </ul>
         </section>

         <section class="grid mx-8 text-white text-sm">
            <div class="flex items-center pb-4">
               <Earth class="w-6 h-6 mr-2 text-white" />
               <Select>
                  <SelectTrigger
                     class="w-[120px] bg-transparent border-none outline-none text-white"
                  >
                     <SelectValue placeholder="English" />
                  </SelectTrigger>
                  <SelectContent>
                     <SelectGroup>
                        <SelectLabel>Fruits</SelectLabel>
                        <SelectItem value="apple"> Apple </SelectItem>
                     </SelectGroup>
                  </SelectContent>
               </Select>
            </div>

            <ul>
               <li class="py-1">
                  <a href="#"> Privacy Policy </a>
               </li>
               <li class="py-1">
                  <a href="#"> Terms </a>
               </li>
               <li class="py-1">
                  <a href="#"> Copyright 2024 </a>
               </li>
            </ul>

            <div class="flex gap-x-8 items-center h-[120px]">
               <Instagram />
               <Facebook />
               <Linkedin />
               <Twitter />
               <Youtube />
            </div>
         </section>
      </footer>
   </div>
</template>

<script setup lang="ts">
   import { Button } from '@/components/ui/button';
   import {
      Sheet,
      SheetClose,
      SheetContent,
      SheetDescription,
      SheetFooter,
      SheetHeader,
      SheetTitle,
      SheetTrigger,
   } from '@/components/ui/sheet';
   import { AlignCenter, X } from 'lucide-vue-next';
   import { ref } from 'vue';
   import {
      Select,
      SelectContent,
      SelectGroup,
      SelectItem,
      SelectLabel,
      SelectTrigger,
      SelectValue,
   } from '@/components/ui/select';
   import {
      Earth,
      Instagram,
      Facebook,
      Linkedin,
      Twitter,
      Youtube,
   } from 'lucide-vue-next';
   import {
      Accordion,
      AccordionContent,
      AccordionItem,
      AccordionTrigger,
   } from '@/components/ui/accordion';

   const defaultValue = 'item-1';

   const accordionItems = [
      {
         value: 'item-1',
         title: 'Features',
         content: 'Yes. It adheres to the WAI-ARIA design pattern.',
      },
      {
         value: 'item-2',
         title: 'Solutions',
         content:
            "Yes. It's unstyled by default, giving you freedom over the look and feel.",
      },
      {
         value: 'item-3',
         title: 'Plans',
         content:
            'Yes! You can use the transition prop to configure the animation.',
      },
   ];
</script>
