<script setup>
import { resolveNodeColor } from "../constants.js";

const props = defineProps({
  data: Object,
  model: Object,
  obj: Object
});

const color = resolveNodeColor(props.data.type);
</script>

<template>
  <div :style="{ '--node-color': color }" data-vjs-target="true" class="vjs-supply-chain-node">
    <div class="vjs-supply-chain-node-type">{{ data.type.toUpperCase() }}</div>
    <div style="font-size: 14px">{{ data.name || data.label }}</div>
    <div class="vjs-connect" data-vjs-source="true" />
  </div>
</template>
