<script setup lang="ts">
import { reactive } from 'vue'
import ToggleOption from './ToggleOption.vue'

type OptionKey = 'fast' | 'cheap' | 'quality'

const options = reactive<Record<OptionKey, boolean>>({
  fast: true,
  cheap: false,
  quality: true,
})

function updateOption(key: OptionKey, value: boolean) {
  options[key] = value

  if (!value) {
    return
  }

  if (key === 'cheap' && options.fast && options.quality) {
    options.quality = false
  }

  if (key === 'quality' && options.fast && options.cheap) {
    options.cheap = false
  }

  if (key === 'fast' && options.cheap && options.quality) {
    options.cheap = false
  }
}
</script>

<template>
  <section class="card">
    <ToggleOption
      label="БЫСТРО"
      :model-value="options.fast"
      @update:model-value="updateOption('fast', $event)"
    />
    <ToggleOption
      label="ДЁШЕВО"
      :model-value="options.cheap"
      @update:model-value="updateOption('cheap', $event)"
    />
    <ToggleOption
      label="КАЧЕСТВЕННО"
      :model-value="options.quality"
      @update:model-value="updateOption('quality', $event)"
    />
  </section>
</template>

<style scoped>
.card {
  position: relative;
  width: min(460px, 100%);
  min-height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 14px;
  padding: 28px;
  overflow: hidden;
  background:
    linear-gradient(#ffffff, #ffffff) padding-box,
    linear-gradient(135deg, #ffd166, #06d6a0, #764bff) border-box;
  border: 2px solid transparent;
  border-radius: 28px;
  box-shadow:
    0 30px 80px rgba(67, 56, 202, 0.22),
    0 18px 44px rgba(6, 214, 160, 0.14),
    inset 0 1px 0 rgba(255, 255, 255, 0.95);
}

.card::before {
  content: "";
  position: absolute;
  inset: 0;
  pointer-events: none;
  background-image:
    radial-gradient(circle at 18% 8%, rgba(255, 209, 102, 0.24), transparent 24%),
    radial-gradient(circle at 86% 18%, rgba(6, 214, 160, 0.18), transparent 24%),
    radial-gradient(circle at 74% 92%, rgba(118, 75, 255, 0.14), transparent 26%);
  mask-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.75), transparent 86%);
}
</style>
