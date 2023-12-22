<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { unrefElement } from '@vueuse/core'
import { useSortable } from '@vueuse/integrations/useSortable'
import { EllipsisVerticalIcon } from '@heroicons/vue/24/solid'

import Sortable from 'sortablejs'

const el = ref<HTMLElement | null>(null)
const el2 = ref<HTMLElement | null>(null)


const fn = evt => {
  const from = evt.from.getAttribute('data-group');
  const to = evt.to.getAttribute('data-group');
  if (from !== to) {
    console.log(`Target changed from ${from} to ${to}`);
  }
}
const options = {
  animation: 150,
  handle: '.handle',
  group: 'foo',
  onEnd: fn,
};

onMounted(() => {
  const e1 = unrefElement(el);
  const e2 = unrefElement(el2);

  Sortable.create(e1, options);
  Sortable.create(e2, options);
})

// how to get group data for each item?
// events for when these change?


const list = ref([
  { id: 1, name: 'aaaa', description: 'lorem ipsum.' },
  { id: 2, name: 'bbbb', description: 'lorem ipsum.' },
  { id: 3, name: 'cccc', description: 'lorem ipsum.' },
  { id: 4, name: 'dddd', description: 'lorem ipsum.' },
  { id: 5, name: 'eeee', description: 'lorem ipsum.' },
  { id: 6, name: 'ffff', description: 'lorem ipsum.' },
  { id: 7, name: 'gggg', description: 'lorem ipsum.' },
  { id: 8, name: 'hhhh', description: 'lorem ipsum.' },
])
const list2 = ref([
])
// // //const { option } =
// useSortable(el, list, options)
// // // useSortable(el2, list2, options)
// useSortable(el2, list2, options)



</script>

<template>
  <div class="flex flex-nowrap gap-5 m-5 w-1/2 font-normal subpixel-antialiased ">
    <div class="flex flex-col flex-1">
      <div class="bg-gray-500/5 flex-1 flex flex-col">
        <p><h2 class="text-lg p-4">Group 1</h2></p>
        <div ref="el" class="min-w-[500px] rounded foo bg-amber-50 flex-1 py-1 relative" data-group="g1">
          <div v-for="item in list" :key="item.id" class="w-1/2 w-full inline-block my-1 px-2">
            <div class="flex group flex-nowrap">
              <div class="handle bg-gray-500/5 rounded-l cursor-grab flex group-active:cursor-grabbing items-center">
                <EllipsisVerticalIcon class="w-5 h-5 p-0 m-0 group-hover:visible invisible hover:group-active:text-amber-400" />
              </div>

              <span class="flex-1 bg-gray-500/5">
                <div class="ring-2 ring-amber-50 rounded my-2 mx-1 px-2 py-1 ">
                  <div class="text-sm font-semibold">{{ item.name }}</div>
                  <div class="text-xs">{{ item.description }}</div>
                </div>
              </span>

              <div class="handle bg-gray-500/5 rounded-r cursor-grab flex group-active:cursor-grabbing items-center">
                <EllipsisVerticalIcon class="w-5 h-5 p-0 m-0 group-hover:visible invisible hover:group-active:text-amber-400" />
              </div>
            </div>
          </div>

          <!-- empty! -->
          <div class="only:flex absolute inset-0 items-center hidden">
            <div class="flex-1 text-center font-light text-amber-900">Nothing here...</div>
          </div>
        </div>
      </div>
    </div>

    <div class="flex flex-col flex-1">
      <div class="bg-gray-500/5 flex-1 flex flex-col">
        <p><h2 class="text-lg p-4">Group 2</h2></p>
        <div ref="el2" class="min-w-[500px] rounded foo bg-amber-50 flex-1 py-1 relative" data-group="g2">

          <!-- empty! -->
          <div class="only:flex absolute inset-0 items-center hidden">
            <div class="flex-1 text-center font-light text-amber-900">Nothing here...</div>
          </div>
        </div>
      </div>
    </div>


  </div>
</template>
