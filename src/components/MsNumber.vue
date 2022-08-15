<template>
  <div>{{ label }}</div>
  <input @keyup="onKeyup" class="input-number" ref="input" />
</template>

<script>
import { ref, onMounted, getCurrentInstance, watch, nextTick } from "vue";
import AutoNumeric from "autonumeric";
export default {
  name: "MsNumber",
  props: {
    label: {
      type: String,
      default: "Số tiền",
    },
    value: {
      type: Number,
      default: 0,
    },
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 100,
    },
    step: {
      type: Number,
      default: 1,
    },
    modelValue: {
      default: 0,
      type: Number,
    },
    initValue:{
      default:0,
      type:Number
    }
  },
  setup(props, { emit }) {
    const { proxy } = getCurrentInstance();
    const input = ref({});
    const internalValue = ref(null);

    onMounted(() => {
      const numberic = new AutoNumeric(".input-number", {
        digitGroupSeparator: ",",
        decimalCharacter: ".",
        maximumValue:100000,
        decimalPlaces: 1,
      });

      proxy._numberic = numberic;
    });

    const onKeyup = (e) => {
      /* eslint-disable no-debugger */
      debugger;

      const rawValueText = proxy._numberic.rawValue;
      const valueNumber = Number(rawValueText);
      proxy._rawValue  = valueNumber;

      emit("update:modelValue", valueNumber);
    };

    watch(
      () => props.modelValue,
      (newValue) => {
        
        nextTick(() => {
          if (proxy._numberic && newValue !== proxy._rawValue) {
            proxy._numberic.set(newValue);
          }
        });
      },
      { immediate: true }
    );
    return {
      internalValue,
      onKeyup,
      input,
    };
  },
};
</script>
/* eslint-disable */
