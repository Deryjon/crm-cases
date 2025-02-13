<script setup lang="ts">
import { useSidebarStore } from '@/stores/sidebar'
import { onClickOutside } from '@vueuse/core'
import { ref } from 'vue'
import SidebarItem from './SidebarItem.vue'

const target = ref(null)

const sidebarStore = useSidebarStore()

onClickOutside(target, () => {
  sidebarStore.isSidebarOpen = false
})

const menuGroups = ref([
  {
    menuItems: [
      {
        icon: `<svg
  xmlns="http://www.w3.org/2000/svg"
  class="h-5 w-5"
  fill="none"
  viewBox="0 0 22 22"
  stroke="currentColor"
>
  <path
    stroke-linecap="round"
    stroke-linejoin="round"
    stroke-width="2"
    d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13l-1.35 2.7a1 1 0 00.9 1.5h11.1a1 1 0 00.9-1.5L17 13M7 13h10M10 21a1 1 0 100-2 1 1 0 000 2zm8 0a1 1 0 100-2 1 1 0 000 2z"
  />
</svg>
`,
        label: 'Товары',
        route: '#',
        children: [
          { label: 'Каталог', route: '/catalog' },
          { label: 'Импорт', route: '/import' },
          { label: 'Инвентаризация', route: '/inventory' },
          { label: 'Трансфер', route: '/transfer' },
          { label: 'Поставщики', route: '/suppliers' }
        ]
      },
      {
        icon: `
        <svg
  xmlns="http://www.w3.org/2000/svg"
  class="h-6 w-6"
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
>
  <path
    stroke-linecap="round"
    stroke-linejoin="round"
    stroke-width="2"
    d="M6 3h12M6 7h12M3 10h18v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-7zm3 3h6m-6 3h6"
  />
</svg>

`,
        label: 'Продажи',
        route: '#',
        children: [
          { label: 'Новая продажа', route: '/create' },
          { label: 'Все продажи', route: '/all' }
        ]
      },
      {
        icon: `<svg
  xmlns="http://www.w3.org/2000/svg"
  class="h-6 w-6"
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
>
  <path d="M16 14c2.2 0 4 1.8 4 4v2H4v-2c0-2.2 1.8-4 4-4h8zm-4-2a4 4 0 1 0 0-8 4 4 0 0 0 0 8z" />
</svg>
`,
        label: 'Клиенты',
        route: '#',
        children: [
          { label: 'Все клиенты', route: '/clients/all' },
          { label: 'Программа лояльности', route: '/clients/loyalty' },
          { label: 'Долги клиентов', route: '/clients/debts' }
        ]
      },
      {
        icon: `<svg
  xmlns="http://www.w3.org/2000/svg"
  class="h-6 w-6"
  fill="none"
  viewBox="0 0 24 24"
  stroke="currentColor"
>
  <path
    stroke-linecap="round"
    stroke-linejoin="round"
    stroke-width="2"
    d="M3 3v18h18M9 17v-6M13 17v-3M17 17v-9"
  />
</svg>
`,
        label: 'Отчеты',
        route: '#',
        children: [
          { label: 'Магазин', route: '/reports/shop' },
          { label: 'Товары', route: '/reports/products' },
          { label: 'Продавцы', route: '/reports/sellers' },
          { label: 'Клиенты', route: '/reports/clients' }
        ]
      },
      {
        icon: `<svg
  xmlns="http://www.w3.org/2000/svg"
  class="h-6 w-6"
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
>
  <path d="M12 12c2.2 0 4 1.8 4 4v2H8v-2c0-2.2 1.8-4 4-4zM12 10a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM4 20h16M4 20v-2c0-2.2 1.8-4 4-4h8c2.2 0 4 1.8 4 4v2z" />
</svg>
`,
        label: 'Управление',
        route: '#',
        children: [
          { label: 'Сотрудники', route: '/management/staff' },
          { label: 'Роли', route: '/management/roles' }
        ]
      },
      {
        icon: `<svg
  xmlns="http://www.w3.org/2000/svg"
  class="h-6 w-6"
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
>
  <path
    stroke-linecap="round"
    stroke-linejoin="round"
    stroke-width="2"
    d="M12 15.5a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7zM19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 1 1-4 0v-.12a1.65 1.65 0 0 0-1-1.51 1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 1 1 0-4h.12a1.65 1.65 0 0 0 1.51-1 1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06a1.65 1.65 0 0 0 1.82.33h.18a1.65 1.65 0 0 0 1-1.51V3a2 2 0 1 1 4 0v.12a1.65 1.65 0 0 0 1 1.51h.18a1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82v.18a1.65 1.65 0 0 0 1.51 1H21a2 2 0 1 1 0 4h-.12a1.65 1.65 0 0 0-1.51 1z"
  />
</svg>

`,
        label: 'Настройки',
        route: '#',
        children: [
          { label: 'Профиль', route: '/settings/staff' },
          { label: 'Компания', route: '/settings/company' },
          { label: 'Магазины', route: '/settings/shops' },
          { label: 'Кассы', route: '/settings/cash-registers' },
          { label: 'Чеки', route: '/settings/checks' },
          { label: 'Валюты и оплаты', route: '/settings/currencies-and-payments' },
          { label: 'Товары', route: '/settings/products' },
          { label: 'Уведомления', route: '/settings/notifications' }
        ]
      }
    ]
  },
  {
    name: 'OTHERS',
    menuItems: [
      {
        icon: `<svg
                  class="fill-current"
                  width="18"
                  height="19"
                  viewBox="0 0 18 19"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <g clip-path="url(#clip0_130_9814)">
                    <path
                      d="M12.7127 0.55835H9.53457C8.80332 0.55835 8.18457 1.1771 8.18457 1.90835V3.84897C8.18457 4.18647 8.46582 4.46772 8.80332 4.46772C9.14082 4.46772 9.45019 4.18647 9.45019 3.84897V1.88022C9.45019 1.82397 9.47832 1.79585 9.53457 1.79585H12.7127C13.3877 1.79585 13.9221 2.33022 13.9221 3.00522V15.0709C13.9221 15.7459 13.3877 16.2802 12.7127 16.2802H9.53457C9.47832 16.2802 9.45019 16.2521 9.45019 16.1959V14.2552C9.45019 13.9177 9.16894 13.6365 8.80332 13.6365C8.43769 13.6365 8.18457 13.9177 8.18457 14.2552V16.1959C8.18457 16.9271 8.80332 17.5459 9.53457 17.5459H12.7127C14.0908 17.5459 15.1877 16.4209 15.1877 15.0709V3.03335C15.1877 1.65522 14.0627 0.55835 12.7127 0.55835Z"
                      fill=""
                    />
                    <path
                      d="M10.4346 8.60205L7.62207 5.7333C7.36895 5.48018 6.97519 5.48018 6.72207 5.7333C6.46895 5.98643 6.46895 6.38018 6.72207 6.6333L8.46582 8.40518H3.45957C3.12207 8.40518 2.84082 8.68643 2.84082 9.02393C2.84082 9.36143 3.12207 9.64268 3.45957 9.64268H8.49395L6.72207 11.4427C6.46895 11.6958 6.46895 12.0896 6.72207 12.3427C6.83457 12.4552 7.00332 12.5114 7.17207 12.5114C7.34082 12.5114 7.50957 12.4552 7.62207 12.3145L10.4346 9.4458C10.6877 9.24893 10.6877 8.85518 10.4346 8.60205Z"
                      fill=""
                    />
                  </g>
                  <defs>
                    <clipPath id="clip0_130_9814">
                      <rect width="18" height="18" fill="white" transform="translate(0 0.052124)" />
                    </clipPath>
                  </defs>
                </svg>`,
        label: 'Authentication',
        route: '#',
        children: [
          { label: 'Sign In', route: '/auth/signin' },
          { label: 'Sign Up', route: '/auth/signup' }
        ]
      }
    ]
  }
])
</script>

<template>
  <aside
    class="absolute left-0 top-0 z-9999 flex h-screen w-72.5 flex-col overflow-y-hidden bg-black duration-300 ease-linear dark:bg-boxdark lg:static lg:translate-x-0"
    :class="{
      'translate-x-0': sidebarStore.isSidebarOpen,
      '-translate-x-full': !sidebarStore.isSidebarOpen
    }"
    ref="target"
  >
    <!-- SIDEBAR HEADER -->
    <div class="flex flex-col justify-between items-center gap-2 px-6 py-5.5 lg:py-4">
      <router-link to="/" class="mx-auto">
        <img src="@/assets/images/logo/logo-icon.svg" alt="Logo" class="h-[100px]" />
      </router-link>
      <h1 class="">Konkurent.Cases</h1>

      <button class="block lg:hidden" @click="sidebarStore.isSidebarOpen = false">
        <svg
          class="fill-current"
          width="20"
          height="18"
          viewBox="0 0 20 18"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M19 8.175H2.98748L9.36248 1.6875C9.69998 1.35 9.69998 0.825 9.36248 0.4875C9.02498 0.15 8.49998 0.15 8.16248 0.4875L0.399976 8.3625C0.0624756 8.7 0.0624756 9.225 0.399976 9.5625L8.16248 17.4375C8.31248 17.5875 8.53748 17.7 8.76248 17.7C8.98748 17.7 9.17498 17.625 9.36248 17.475C9.69998 17.1375 9.69998 16.6125 9.36248 16.275L3.02498 9.8625H19C19.45 9.8625 19.825 9.4875 19.825 9.0375C19.825 8.55 19.45 8.175 19 8.175Z"
            fill=""
          />
        </svg>
      </button>
    </div>
    <!-- SIDEBAR HEADER -->

    <div class="no-scrollbar flex flex-col overflow-y-auto duration-300 ease-linear">
      <!-- Sidebar Menu -->
      <nav class="mt-5 py-4 px-4 lg:mt-1 lg:px-6">
        <template v-for="menuGroup in menuGroups" :key="menuGroup.name">
          <div>
            <h3 class="mb-4 ml-4 text-sm font-medium text-bodydark2">{{ menuGroup.name }}</h3>

            <ul class="mb-6 flex flex-col gap-1.5">
              <SidebarItem
                v-for="(menuItem, index) in menuGroup.menuItems"
                :item="menuItem"
                :key="index"
                :index="index"
              />
            </ul>
          </div>
        </template>
      </nav>
      <!-- Sidebar Menu -->

      <!-- Promo Box -->
    </div>
  </aside>
</template>
