<template>
  <div class="h-screen flex flex-col items-center mt-32 px-3">
    <button
      class="px-3 py-2 bg-yellow-500 text-white rounded-md"
      @click="state = !state"
    >
      Open
    </button>
    state: {{ state }}
    <div
      v-if="state"
      ref="divRef"
      class="inline-block p-8 bg-gray-600 text-white rounded-md"
    >
      Now you can see me
    </div>
  </div>
</template>

<script>
import { defineComponent, onUpdated, ref } from "@nuxtjs/composition-api";
import { onClickOutside } from "@vueuse/core";

export default defineComponent({
  setup() {
    const state = ref(false);
    const divRef = ref(null);

    onClickOutside(divRef, () => {
      console.log("onClickOutside");
      state.value = false;
    });
    onUpdated(() => {
      console.log(`onUpdated ${state.value}`);
    });

    return {
      state,
      divRef,
    };
  },
});
</script>

<style>
</style>
