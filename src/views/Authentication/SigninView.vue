<script setup lang="ts">
import { ref, computed } from 'vue'
import DefaultAuthCard from '@/components/Auths/DefaultAuthCard.vue'
import InputGroup from '@/components/Auths/InputGroup.vue'
import DefaultLayout from '@/layouts/DefaultLayout.vue'
import { useRouter } from 'vue-router'

const router = useRouter()


const phone = ref('')
const password = ref('')
const phoneError = ref('')
const passwordError = ref('')
const showPassword = ref(false)


const cleanedPhone = computed(() => phone.value.replace(/\D/g, ''))

const isFormValid = computed(() => {
  return cleanedPhone.value.length === 9 && password.value.length >= 9
})

const signInWorker = () => {
  router.push('/') 
  localStorage.setItem('isAuth', 'true')
  localStorage.setItem('token', 'yes')
}


const validateForm = () => {
  let isValid = true
  phoneError.value = ''
  passwordError.value = ''

  // Валидация телефона
  if (cleanedPhone.value.length !== 9) {
    phoneError.value = 'Номер телефона должен содержать 9 цифр'
    isValid = false
  }

  // Валидация пароля
  if (password.value.length < 8) {
    passwordError.value = 'Пароль должен быть не короче 8 символов'
    isValid = false
  }

  return isValid
}

const handleSubmit = (e: Event) => {
  e.preventDefault()
  if (validateForm()) {
    console.log('Phone (raw):', cleanedPhone.value)
    console.log('Password:', password.value)
  }
  signInWorker()
}
</script>

<template>
  <DefaultLayout>
    <DefaultAuthCard title="Вход в аккаунт">
      <form @submit="handleSubmit">
        <InputGroup
          label="Введите номер телефона"
          inputType="phone"
          placeholder="XX XXX XX XX"
          v-model="phone"
          :maxLength="9"
        >
          <!-- Иконка -->
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="currentColor"
            width="24"
            height="24"
          >
            <path
              d="M6.62 10.79a15.054 15.054 0 006.59 6.59l2.2-2.2a1.003 1.003 0 011.11-.21c1.21.49 2.53.76 3.88.76a1 1 0 011 1v3.5a1 1 0 01-1 1C10.29 21.5 2.5 13.71 2.5 4a1 1 0 011-1h3.5a1 1 0 011 1c0 1.35.27 2.67.76 3.88a1.003 1.003 0 01-.21 1.11l-2.2 2.2z"
            />
          </svg>
        </InputGroup>
        <p v-if="phoneError" class="text-red-500 text-sm mt-1">{{ phoneError }}</p>

        <InputGroup
          label="Пароль"
          input-type="text"
          placeholder="Введите пароль"
          v-model="password"
        >
          <!-- Иконка -->
          <button type="button" class="ml-2">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="currentColor"
              viewBox="0 0 24 24"
              width="24"
              height="24"
            >
              <path
                d="M12 1a5 5 0 00-5 5v4H6a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2v-8a2 2 0 00-2-2h-1V6a5 5 0 00-5-5zm-3 5a3 3 0 116 0v4H9V6zm3 8a1.5 1.5 0 011.5 1.5c0 .65-.417 1.2-1 1.41V19h-1v-2.09a1.501 1.501 0 01-1-1.41A1.5 1.5 0 0112 14z"
              />
            </svg>
          </button>
        </InputGroup>
        <p v-if="passwordError" class="text-red-500 text-sm mt-1">{{ passwordError }}</p>

        <div class="mb-5 mt-6">
          <input
            type="submit"
            value="Вход в аккаунт"
            @click="signInWorker"
            :class="[
              'w-full rounded-lg border p-4 font-medium transition',
              isFormValid
                ? 'cursor-pointer bg-primary text-white hover:bg-opacity-90'
                : 'cursor-not-allowed bg-gray-400 text-gray-700'
            ]"
            :disabled="!isFormValid"
          />
        </div>

        <div class="mt-6 text-center">
          <p class="font-medium">
            Еще нет аккаунта?
            <router-link to="/auth/signup" class="text-primary">Создать аккаунт</router-link>
          </p>
        </div>
      </form>
    </DefaultAuthCard>
  </DefaultLayout>
</template>
