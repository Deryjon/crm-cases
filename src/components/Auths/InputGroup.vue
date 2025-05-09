<script setup lang="ts">
const props = defineProps<{
  label: string
  inputType: 'phone' | 'text' | 'number' // добавляем возможность для типа 'phone'
  placeholder: string
  modelValue: string | number
  maxLength?: number
}>()

const emit = defineEmits(['update:modelValue'])

function formatPhone(value: string): string {
  // Удаляем всё, кроме цифр
  const digits = value.replace(/\D/g, '').slice(0, props.maxLength || 9)

  // Формат по шаблону: 99 999 99 99
  const parts = []
  if (digits.length > 0) parts.push(digits.slice(0, 2))
  if (digits.length > 2) parts.push(digits.slice(2, 5))
  if (digits.length > 5) parts.push(digits.slice(5, 7))
  if (digits.length > 7) parts.push(digits.slice(7, 9))

  return parts.join(' ')
}

function handleInput(event: Event) {
  const target = event.target as HTMLInputElement
  let value = target.value

  // Удаляем все нецифры
  let digits = value.replace(/\D/g, '')

  // Ограничиваем до 9 цифр максимум
  digits = digits.slice(0, props.maxLength ?? 9)

  // Форматируем для типа 'phone'
  if (props.inputType === 'phone') {
    value = formatPhone(digits)
  } else {
    value = digits
  }

  emit('update:modelValue', value)
}
function handleKeyDown(event: KeyboardEvent) {
  if (
    (props.inputType === 'number' || props.inputType === 'phone') &&
    !/^\d$/.test(event.key) &&
    event.key !== 'Backspace' &&
    event.key !== 'Tab' &&
    event.key !== 'ArrowLeft' &&
    event.key !== 'ArrowRight'
  ) {
    event.preventDefault()
  }
}
</script>

<template>
  <div class="mb-4">
    <label class="mb-2.5 block font-medium text-black dark:text-white">{{ props.label }}</label>
    <div class="relative">
      <input
        :type="props.inputType === 'number' ? 'text' : props.inputType"
        :placeholder="props.placeholder"
        :value="modelValue"
        @input="handleInput"
        @keydown="handleKeyDown"
        :inputmode="
          props.inputType === 'number' || props.inputType === 'phone' ? 'numeric' : undefined
        "
        :maxlength="props.inputType === 'phone' ? 12 : props.maxLength"
        class="w-full rounded-lg border border-stroke bg-transparent py-4 pl-6 pr-10 outline-none focus:border-primary focus-visible:shadow-none dark:border-form-strokedark dark:bg-form-input dark:focus:border-primary text-black dark:text-white"
      />

      <span class="absolute right-4 top-4">
        <slot></slot>
      </span>
    </div>
  </div>
</template>
