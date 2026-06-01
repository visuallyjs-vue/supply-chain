### About this Demo

This Vue application demonstrates a **Supply Chain Analyzer** built with **VisuallyJS**. It combines a node-link diagram with a Sankey chart.

### VisuallyJS Components Used

The demo utilizes several components from the `@visuallyjs/browser-ui-vue` package:

- **SurfaceProvider**: Provides the VisuallyJS context.
- **SurfaceComponent**: Used to render the node-link representation of the supply chain.
- **SankeyChartComponent**: Used to render a Sankey representation of the supply chain data.
- **ControlsComponent**: UI controls for the surface.

### Component Options

The `SurfaceComponent` is configured with:
- **renderOptions**: Configures the rendering engine and visual properties.
- **viewOptions**: Defines custom components for nodes (e.g., `SupplyChainNode`) and markers for edges.
- **modelOptions**: Configures an edge factory for creating new connections.

The `SankeyChartComponent` is configured with:
- **options**: Includes `labelProperty`, `linkColorStrategy`, and a `colorGenerator`.
- **pivot**: Allows pivoting the data by specific properties (e.g., "transitMode", "carrier").
- **useModel**: Set to `true` to use the same underlying data model as the `SurfaceComponent`.

### CSS Requirement

For the VisuallyJS components to render correctly, the standard VisuallyJS stylesheet must be included in the project. In this demo, it is imported in `src/main.js`:

```javascript
import "@visuallyjs/browser-ui/css/visuallyjs.css"
```
