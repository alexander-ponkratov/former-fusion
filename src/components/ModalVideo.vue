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
    thumb: string
    thumbWidth: number
    thumbHeight: number
    video: string
    videoWidth: number
    videoHeight: number
}
const props = defineProps<Props>()
</script>
<template>
    <div>
        <!-- Video thumbnail -->
        <button @click="modalOpen = true" aria-label="Смотреть видео" data-aos="fade-in" type="button"
            class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-full text-sm px-8 py-4 text-center">
            <h4 class="text-white font-extrabold text-sm text-center  min-[500px]:text-start">
                <div class="flex items-center gap-x-2">
                    <span>ПОСМОТРЕТЬ ВИДЕО</span>
                    <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 576 512"
                        class="fill-white"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
                        <path
                            d="M549.655 124.083c-6.281-23.65-24.787-42.276-48.284-48.597C458.781 64 288 64 288 64S117.22 64 74.629 75.486c-23.497 6.322-42.003 24.947-48.284 48.597-11.412 42.867-11.412 132.305-11.412 132.305s0 89.438 11.412 132.305c6.281 23.65 24.787 41.5 48.284 47.821C117.22 448 288 448 288 448s170.78 0 213.371-11.486c23.497-6.321 42.003-24.171 48.284-47.821 11.412-42.867 11.412-132.305 11.412-132.305s0-89.438-11.412-132.305zm-317.51 213.508V175.185l142.739 81.205-142.739 81.201z">
                        </path>
                    </svg>
                </div>
            </h4>
        </button>
        <!-- End: Video thumbnail -->
        <TransitionRoot :show="modalOpen" as="template">
            <Dialog :initialFocus="videoRef" @close="modalOpen = false">
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
                                <video ref="videoRef" loop controls>
                                    <source :src="props.video" :width="props.videoWidth" :height="props.videoHeight"
                                        type="video/mp4" />
                                    Your browser does not support the video tag.
                                </video>
                                <svg class="absolute top-3 right-3 fill-white cursor-pointer" @click="modalOpen = false" xmlns="http://www.w3.org/2000/svg" height="1.5em" viewBox="0 0 384 512"><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path  d="M342.6 150.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0L192 210.7 86.6 105.4c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L146.7 256 41.4 361.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0L192 301.3 297.4 406.6c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L237.3 256 342.6 150.6z"/></svg>
                            </div>
                        </DialogPanel>
                    </div>
                </TransitionChild>
                <!-- End: Modal dialog -->

            </Dialog>
        </TransitionRoot>
    </div>
</template>