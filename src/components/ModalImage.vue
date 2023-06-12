<script setup lang="ts">
import { ref, watch } from 'vue'
import {
    Dialog,
    DialogPanel,
    TransitionRoot,
    TransitionChild,
} from '@headlessui/vue'
const modalOpen = ref<boolean>(false)
const videoRef = ref<HTMLVideoElement | null>(null)
watch(videoRef, () => {
    videoRef.value?.play()
})
interface Props {
    imageSrc: string,
    imageAlt: string
}
const props = defineProps<Props>()
</script>
<template>
    <div>
        <!-- Video thumbnail -->
        <img loading="lazy" a-aos="fade-in" @click="modalOpen = true" class="rounded-t-lg" :src=props.imageSrc :alt=props.imageAlt />
        <!-- End: Video thumbnail -->
        <TransitionRoot :show="modalOpen" as="template">
            <Dialog  @keypress.4="modalOpen = false" @keyup.esc="modalOpen = false" @close="modalOpen = false">
                <!-- Modal backdrop -->
                <TransitionChild className="fixed inset-0 z-[99999] bg-black bg-opacity-50 transition-opacity"
                    enter="transition ease-out duration-200" enterFrom="opacity-0" enterTo="opacity-100"
                    leave="transition ease-out duration-100" leaveFrom="opacity-100" leaveTo="opacity-0"
                    aria-hidden="true" />
                <!-- End: Modal backdrop -->
                <!-- Modal dialog -->
                <TransitionChild className="fixed inset-0 z-[99999] flex p-6" enter="transition ease-out duration-300"
                    enterFrom="opacity-0 scale-75" enterTo="opacity-100 scale-100" leave="transition ease-out duration-200"
                    leaveFrom="opacity-100 scale-100" leaveTo="opacity-0 scale-75">
                    <div class="max-w-5xl mx-auto h-full flex items-center">
                        <DialogPanel class="w-full max-h-full rounded-3xl shadow-2xl aspect-auto bg-black overflow-hidden">
                            <div class="relative flex">
                                <img loading="lazy" class="max-h-[100vh]" :src=props.imageSrc :alt=props.imageAlt />
                                <svg class="absolute top-3 right-3 cursor-pointer" @click="modalOpen = false" xmlns="http://www.w3.org/2000/svg" height="1.5em" viewBox="0 0 384 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M342.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L192 210.7 86.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L146.7 256 41.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L192 301.3 297.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L237.3 256 342.6 150.6z"/></svg>
                            </div>
                        </DialogPanel>
                    </div>
                    
                </TransitionChild>
                <!-- End: Modal dialog -->
            </Dialog>
        </TransitionRoot>
    </div>
</template>