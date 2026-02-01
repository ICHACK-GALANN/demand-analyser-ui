<script setup lang="ts">
type Props = {
  name: string;
  country: string;
  delta: number;
  score: number;
}

const {
  name,
  country,
  delta,
  score
} = defineProps<Props>();

const formattedDelta = delta > 0 ? `+${delta}` : `-${delta}`;
const deltaColor = delta > 0 ? 'text-green-400' : 'text-red-400';
</script>

<template>
  <div class="border border-muted hover:border-red-400 hover:bg-red-400/10 flex justify-between items-center py-2 px-4">
    <div>
      <strong>{{ name }}</strong>
      <div class="flex justify-between">
        <span class="text-muted">{{ country }}</span> 
        <span :class="deltaColor">{{ formattedDelta }}</span>
      </div>
    </div>
  </div>
</template>