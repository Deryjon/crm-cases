<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'
import BreadcrumbDefault from '@/components/Breadcrumbs/BreadcrumbDefault.vue'
import CalendarCard from '@/components/CalendarCard.vue'
import DefaultLayout from '@/layouts/DefaultLayout.vue'

const pageTitle = ref('Catalog')

const createProduct = async () => {
  try {
    const product = {
      title: 'Test Product',
      description: 'Test description',
      price: 100,
      brand: 'TestBrand',
      category: 'TestCategory',
      thumbnail: 'https://example.com/image.jpg',
    }

    const response = await axios.post('http://localhost:3000/products', product)

    console.log('Product created:', response.data)
    alert('Product created successfully!')
  } catch (error) {
    console.error('Error creating product:', error)
    alert('Failed to create product')
  }
}
</script>


<template>
  <DefaultLayout>
    <div class="mx-auto max-w-7xl">
      <!-- Breadcrumb Start -->
      <BreadcrumbDefault :pageTitle="pageTitle" />
      <!-- Breadcrumb End -->
      <button class="btn-primary p-3 bg-black" @click="createProduct">Create product</button>
      <p class="mt-[1000px]">efeifje</p>
    </div>
  </DefaultLayout>
</template>
