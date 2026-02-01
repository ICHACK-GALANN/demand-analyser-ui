# AI Coding Agent Instructions for demand-analyser-ui

## Project Overview
- **Type**: Nuxt 4 Frontend Application (minimal starter)
- **Framework Stack**: Nuxt 4, Vue 3, TypeScript, Vue Router 4
- **Package Manager**: pnpm
- **Runtime**: Node.js with ESM (type: "module")
- **Purpose**: UI for demand analysis

## Architecture & File Organization

### Core Entry Points
- **[app/app.vue](app/app.vue)**: Root Vue component - main application shell
- **[nuxt.config.ts](nuxt.config.ts)**: Nuxt configuration (minimal setup with devtools enabled)
- **[tsconfig.json](tsconfig.json)**: TypeScript references Nuxt-generated tsconfig files in `.nuxt/` directory

### Directory Structure
- `app/`: Application source components and pages
- `public/`: Static assets served directly
- `.nuxt/`: Auto-generated Nuxt build artifacts (do not edit)
- `node_modules/`: Dependencies installed via pnpm

## Developer Workflows

### Setup & Installation
```bash
pnpm install      # Install dependencies (replaces npm/yarn/bun)
nuxt prepare      # Runs automatically on postinstall
```

### Development
```bash
pnpm dev          # Start dev server on http://localhost:3000 with hot reload
```

### Building & Deployment
```bash
pnpm build        # Production build (generates .output/ directory)
pnpm preview      # Preview production build locally
pnpm generate     # Generate static site (if needed)
```

## Code Patterns & Conventions

### Vue 3 & Nuxt 4 Standards
- **Component Files**: Use `.vue` single-file components in `app/` directory
- **Auto-imports**: Nuxt auto-imports components and composables; prefix with `Nuxt` for Nuxt components (e.g., `<NuxtRouteAnnouncer />`)
- **Routing**: Vue Router 4 - create pages in `app/pages/` for automatic route generation (follows Nuxt conventions)
- **TypeScript**: Strict mode enabled; all components should have type safety

### Script Setup Syntax
Use `<script setup lang="ts">` for modern, concise component definitions:
```vue
<script setup lang="ts">
interface Props {
  title: string
}
defineProps<Props>()
</script>
```

### Composables
Place reusable logic in `app/composables/` - Nuxt auto-imports with `use` prefix:
```typescript
// app/composables/useDemandAnalysis.ts
export const useDemandAnalysis = () => {
  // Logic here
}
```

## Key Dependencies & Integration Points

### External Packages
- **Nuxt 4**: Full-stack Vue framework with built-in SSR, routing, auto-imports
- **Vue 3**: Component framework with Composition API
- **Vue Router 4**: Client-side routing (integrated with Nuxt)
- **Three.js**: 3D graphics library for WebGL rendering
- **globe.gl**: Three.js-based interactive globe visualization

### Important Nuxt Features Used
- **Devtools**: Enabled in dev mode for debugging components, state, API calls

## Core Components & Features

### Globe Heatmap Visualization ([app/components/GlobeHeatmap.vue](app/components/GlobeHeatmap.vue))
- **Purpose**: Renders a 3D interactive globe with regional demand heatmap
- **Props**: 
  - `data: RegionData[]` - Array of regions with lat, lng, value, name
  - `height: number` - Container height (default: 600px)
- **Features**:
  - Auto-rotating globe
  - Hexbin aggregation of regional demand data
  - Color gradient (blue→cyan→green→yellow→red) mapped to demand intensity
  - Region labels visible on hover
  - Responsive sizing
- **Integration**: Uses `useRegionalDemand` composable for color mapping and utilities

### Regional Demand Composable ([app/composables/useRegionalDemand.ts](app/composables/useRegionalDemand.ts))
- **Exports**: `RegionData` interface, `useRegionalDemand()` composable
- **Functions**:
  - `getColorForValue(value)` - Maps demand values (0-100) to hex colors
  - `getIntensityLabel(value)` - Returns human-readable demand level
  - `defaultRegions` - Sample data for 8 major global cities

### Pages
- **[app/pages/index.vue](app/pages/index.vue)**: Home page with feature overview and navigation
- **[app/pages/heatmap.vue](app/pages/heatmap.vue)**: Full-page globe heatmap view with legend and sample data (10 regions)

## Critical Patterns & Requirements

1. **TypeScript Strictness**: All files must be type-safe; no `any` types without explicit justification
2. **Nuxt Conventions Over Configuration**: Follow Nuxt's directory structure for auto-discovery
   - Components in `app/components/` → auto-imported
   - Composables in `app/composables/` → auto-imported with `use` prefix
   - Pages in `app/pages/` → auto-routed
3. **ESM Module Format**: Use `import`/`export` (no CommonJS `require`)
4. **Component Naming**: PascalCase for components, camelCase for composables and utilities

## Build & Environment Notes

- **Compatibility Date**: Set to 2025-07-15 for API stability
- **Output Directory**: `.output/` generated after `pnpm build`
- **No Environment Files**: Currently no `.env` files - extend as needed for API endpoints
- **tsconfig.json**: Minimal; references auto-generated `.nuxt/` configs

## Debugging Tips

- **DevTools**: Browser DevTools shows Vue component tree; Nuxt DevTools accessible via keyboard shortcut
- **HMR**: Hot Module Replacement enabled - changes to components/composables reflect instantly
- **Build Errors**: Check `.nuxt/` generated files and TypeScript errors in IDE

---
**Last Updated**: January 2026 | Nuxt 4.3.0
