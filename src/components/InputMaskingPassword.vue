<template>
    <input ref="inputRef" v-bind="attrs" />
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, onBeforeUnmount, watch, defineProps, type PropType } from "vue";
  import { applyMaskedInput } from "@krozamdev/masked-password";
  
  const props = defineProps({
    onChangeEvent: {
      type: Function as PropType<(originalValue: string) => void>,
      required: true,
    },
    maskCharacter: {
      type: String,
      default: "•",
    },
    showPassword: {
      type: Boolean,
      default: false,
    },
  });

  console.log({props});
  
  
  const inputRef = ref<HTMLInputElement | null>(null);
  const maskedInputInstance = ref<ReturnType<typeof applyMaskedInput> | null>(null);
  
  // watchers and Lifecycle Hooks
  onMounted(() => {
    if (inputRef.value) {
      maskedInputInstance.value = applyMaskedInput(inputRef.value, {
        character: props.maskCharacter,
        onChange: (originalValue: string) => {
          if (typeof props.onChangeEvent === "function") {
            props.onChangeEvent(originalValue);
          }
        },
      });
    }
  });
  
  onBeforeUnmount(() => {
    if (maskedInputInstance.value) {
      maskedInputInstance.value.purgeDestroy();
    }
  });
  
  // watch for showPassword prop change
  watch(
    () => props.showPassword,
    (newVal) => {
      // ensure maskedInputInstance is not null before accessing it
      if (maskedInputInstance.value) {
        if (newVal) {
          maskedInputInstance.value.destroy();  // show the password (unmask)
        } else {
          maskedInputInstance.value.addEvent();  // hide the password (mask)
        }
      }
    },
    { immediate: true }  // trigger immediately when the component is mounted
  );
  
  // expose Attributes for the input element
  const attrs = { ...props };
  </script>
  