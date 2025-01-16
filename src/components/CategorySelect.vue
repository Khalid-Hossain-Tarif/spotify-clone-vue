<script setup>
import { ref, toRef } from "vue";
import uniqolor from "uniqolor";

let randomColor = ref('')
randomColor.value = uniqolor.random()

const props = defineProps({
  category: String,
  image: String
})

// const { category } = toRef(props)
</script>

<template>
  <div>
    <RouterLink to="/library">
      <div
          :style="`background-color: ${randomColor.color};`"
          class="
              contrast-[2]
              brightness-[0.87]
              rounded-xl
              aspect-square
              relative
              overflow-hidden
          "
      >
        <div class="text-white pt-3 pl-4 font-semibold text-[23px]">{{ category }}</div>
        <img
            class="
                absolute
                contrast-[0.55]
                -right-3.5
                bottom-0
                max-w-[100px]
                rotate-[20deg]
            "
            :src="image || ''"
            alt=""
        >
      </div>
    </RouterLink>
  </div>
</template>