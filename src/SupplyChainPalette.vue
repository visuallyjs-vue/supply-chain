<script setup>
import { PaletteComponent } from '@visuallyjs/browser-ui-vue';
import { NODE_TYPES, resolveNodeType } from "./constants.js";

function dataGenerator(el) {
  const type = el.getAttribute("data-vjs-type");
  const nodeType = resolveNodeType(type);
  return {
    type,
    name: nodeType.label
  };
}
</script>

<template>
  <PaletteComponent class="vjs-supply-chain-palette" :dataGenerator="dataGenerator">
    <div
      v-for="nt in NODE_TYPES"
      :key="nt.type"
      :data-vjs-type="nt.type"
      title="Drag to add new"
      class="vjs-supply-chain-palette-item"
      :style="{ '--node-color': nt.color }"
    >
      <div class="vjs-supply-chain-item-header">{{ nt.type.toUpperCase() }}</div>
    </div>
  </PaletteComponent>
</template>
