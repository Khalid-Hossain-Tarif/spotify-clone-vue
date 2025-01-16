<script setup>
import { ref, toRefs, watchEffect } from "vue"
import { useRoute } from "vue-router"

const route = useRoute()

const props = defineProps({
    iconString: String,
    iconSize: Number,
    pageUrl: String,
    name: String
})

const { iconString, iconSize, pageUrl, name } = toRefs(props)

let icon = ref(null)
let textIsHover = ref(false)

watchEffect(() => {
    if(route.path === pageUrl.value) {
        icon.value = iconString.value + '-active'
        textIsHover.value = true
    } else {
        icon.value = iconString.value + '-inactive'
        textIsHover.value = false
    }
})

const isHover = () => {
    if(icon.value === iconString.value + '-active') return

    if(icon.value === iconString.value + '-inactive') {
        icon.value = iconString.value + '-inactive-hover'
        textIsHover.value = true
    } else {
        icon.value = iconString.value + '-inactive'
        textIsHover.value = false
    }
}
</script>

<template>
    <li 
        @mouseenter="isHover()"
        @mouseleave="isHover()"
        class="flex items-center justify-start pb-4 cursor-pointer"
    >
        <img :width="iconSize" :src="`/images/icons/${icon}.png`" alt="menu">
        <div 
            class="font-semibold text-sm mt-0.5 ml-4"
            :class="textIsHover ? 'text-white' : 'text-gray-400'"
        >
            {{ name }}
        </div>
    </li>
</template>