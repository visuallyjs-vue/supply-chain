<script setup>
import { ref, onMounted } from 'vue';
import {
  SurfaceComponent,
  SurfaceProvider,
  SankeyChartComponent,
  ControlsComponent
} from "@visuallyjs/browser-ui-vue";
import { EVENT_TAP } from "@visuallyjs/browser-ui";
import SupplyChainNode from './components/SupplyChainNode.vue';
import renderOptions from "./render-options.js";
import { resolveNodeColor } from "./constants.js";
import SupplyChainPalette from "./SupplyChainPalette.vue";
import SupplyChainInspector from "./Inspector.vue";

const props = defineProps({
  url: {
    type: String,
    default: 'dataset.json'
  }
});

const pivotProperty = ref('');
const s = ref(null);

const viewOptions = {
  nodes: {
    default: {
      component: SupplyChainNode
    }
  },
  edges: {
    default: {
      targetMarker: "PlainArrow",
      events: {
        [EVENT_TAP]: ({ obj, model }) => {
          model.setSelection(obj);
        }
      }
    }
  }
};

const modelOptions = {
  edgeFactory: (model, type, data, cb) => {
    cb({
      type,
      value: 100,
      transitMode: "Air",
      carrier: "FedEx"
    });
  }
};

</script>

<template>
  <div class="vjs-supply-chain">
    <div class="vjs-supply-chain-toolbar">
      <strong>Supply Chain Analyzer</strong>
      <div class="pivot-controls">
        <span>Pivot Sankey:</span>
        <select v-model="pivotProperty">
          <option value="">Direct (No Pivot)</option>
          <option value="transitMode">By Transit Mode</option>
          <option value="carrier">By Carrier</option>
        </select>
      </div>
    </div>
    <div class="vjs-supply-chain-canvas">
      <SurfaceProvider>
        <SupplyChainPalette />
        <div class="vjs-supply-chain-view-panel">
          <SurfaceComponent
            ref="s"
            :url="url"
            :modelOptions="modelOptions"
            :renderOptions="renderOptions"
            :viewOptions="viewOptions"
          >
            <ControlsComponent />
          </SurfaceComponent>
          <SupplyChainInspector />
        </div>
        <div class="vjs-supply-chain-view-panel">
          <SankeyChartComponent
            style="height: 500px"
            :options="{
              labelProperty: 'name',
              linkColorStrategy: 'source',
              colorGenerator: {
                generate: (obj) => resolveNodeColor(obj.type)
              }
            }"
            :pivot="pivotProperty" :useModel="true"
          />
        </div>
      </SurfaceProvider>
    </div>
  </div>
</template>
