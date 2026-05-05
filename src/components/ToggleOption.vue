<script setup lang="ts">
defineProps<{
  label: string
  modelValue: boolean
}>()

const emit = defineEmits<{
  'update:modelValue': [value: boolean]
}>()

function updateValue(event: Event) {
  emit('update:modelValue', (event.target as HTMLInputElement).checked)
}
</script>

<template>
  <label class="option">
    <span class="option__label">{{ label }}</span>
    <input
      class="option__input"
      type="checkbox"
      :checked="modelValue"
      @change="updateValue"
    />
    <span class="option__toggle"></span>
  </label>
</template>

<style scoped>
.option {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 24px;
  width: 100%;
  min-height: 72px;
  padding: 16px 18px 16px 22px;
  overflow: hidden;
  background:
    linear-gradient(135deg, rgba(255, 255, 255, 0.92), rgba(255, 255, 255, 0.66));
  border: 1px solid rgba(118, 75, 255, 0.12);
  border-radius: 18px;
  cursor: pointer;
  transition:
    background 180ms ease,
    border-color 180ms ease,
    box-shadow 180ms ease,
    transform 180ms ease;
}

.option:hover {
  background:
    linear-gradient(135deg, rgba(255, 255, 255, 0.98), rgba(233, 255, 247, 0.9));
  border-color: rgba(6, 214, 160, 0.45);
  box-shadow:
    0 14px 30px rgba(67, 56, 202, 0.12),
    0 8px 18px rgba(6, 214, 160, 0.12);
  transform: translateY(-1px);
}

.option:has(.option__input:checked) {
  background:
    linear-gradient(135deg, rgba(255, 251, 235, 0.98), rgba(232, 255, 247, 0.95));
  border-color: rgba(6, 214, 160, 0.58);
  box-shadow:
    0 12px 28px rgba(6, 214, 160, 0.13),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
}

.option__label {
  position: relative;
  color: #18181b;
  font-size: 30px;
  font-weight: 800;
  line-height: 1.2;
  letter-spacing: 0;
}

.option__input {
  position: absolute;
  opacity: 0;
  pointer-events: none;
}

.option__toggle {
  position: relative;
  flex: 0 0 auto;
  width: 64px;
  height: 36px;
  border-radius: 999px;
  background: #e8e3f5;
  box-shadow:
    inset 0 2px 5px rgba(0, 0, 0, 0.12),
    0 1px 0 rgba(255, 255, 255, 0.8);
  transition:
    background 220ms ease,
    box-shadow 220ms ease,
    transform 220ms ease;
}

.option__toggle::before {
  content: "";
  position: absolute;
  top: 5px;
  left: 5px;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: #ffffff;
  box-shadow:
    0 6px 14px rgba(0, 0, 0, 0.24),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
  transition:
    transform 220ms cubic-bezier(0.22, 1, 0.36, 1),
    box-shadow 220ms ease;
}

.option__input:checked + .option__toggle {
  background: linear-gradient(135deg, #06d6a0, #764bff);
  box-shadow:
    inset 0 2px 8px rgba(24, 24, 27, 0.22),
    0 10px 24px rgba(118, 75, 255, 0.3);
}

.option__input:checked + .option__toggle::before {
  transform: translateX(28px);
}

.option__input:focus-visible + .option__toggle {
  outline: 3px solid rgba(6, 214, 160, 0.34);
  outline-offset: 4px;
}

.option:active .option__toggle {
  transform: scale(0.96);
}

.option:active .option__toggle::before {
  box-shadow:
    0 3px 8px rgba(0, 0, 0, 0.28),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
}

@media (max-width: 420px) {
  .option {
    min-height: 66px;
    padding: 14px 14px 14px 18px;
  }

  .option__label {
    font-size: 24px;
  }
}
</style>
