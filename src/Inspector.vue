<script setup>
import { Node, Edge, isNode, isPort } from "@visuallyjs/browser-ui";
import { InspectorComponent } from "@visuallyjs/browser-ui-vue";
import {ref} from "vue";

const current = ref(null)

const refresh = (obj) => {
  current.value = obj
}


</script>

<template>
  <InspectorComponent class="vjs-supply-chain-inspector"  :refresh="refresh">
      <div v-if="current?.objectType === Node.objectType">
        <label>Name:</label>
        <input type="text" vjs-att="name" placeholder="name" />
      </div>

      <div v-if="current?.objectType === Edge.objectType">
        <label>Value</label>
        <input type="text" vjs-att="value" vjs-datatype="integer" />
        <label>Transit Mode</label>
        <select vjs-att="transitMode">
          <option value="Air">Air</option>
          <option value="Sea">Sea</option>
          <option value="Road">Road</option>
        </select>
        <label>Carrier</label>
        <select vjs-att="carrier">
          <option value="Maersk">Maersk</option>
          <option value="DHL">DHL</option>
          <option value="FedEx">FedEx</option>
          <option value="UPS">UPS</option>
          <option value="DBCargo">DBCargo</option>
          <option value="Emirates">Emirates</option>
        </select>
      </div>
  </InspectorComponent>
</template>
