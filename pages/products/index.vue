<template>
  <div style="font-family: Arial, sans-serif">
    <!-- Header -->
    <header style="background-color: #282c34; color: white; padding: 10px 20px; text-align: center">
      <h1>Myntra Clone</h1>
    </header>

    <!-- Product Grid -->
    <div style="padding: 20px">
      <div style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 20px">
        <div v-for="product in products" :key="product.id" style="border: 1px solid #ddd; border-radius: 8px; overflow: hidden">
          <!-- Product Image -->
          <img
            :src="product.thumbnail" <!-- Ensure the image URL is correct -->
            :alt="product.title"
            style="width: 100%; height: 200px; object-fit: cover"
          />
          <div style="padding: 10px">
            <h3 style="margin: 0; font-size: 16px">{{ product.title }}</h3>
            <p style="margin: 5px 0; color: #555; font-size: 14px">{{ product.description }}</p>
            <p style="margin: 5px 0; font-weight: bold">${{ product.price }}</p>
          </div>
        </div>
      </div>

      <!-- Pagination -->
      <div style="margin-top: 20px; text-align: center">
        <nuxt-link v-if="page > 1" :to="`/products?page=${page - 1}`">
          <button style="margin-right: 10px; padding: 8px 16px; background-color: #282c34; color: white; border: none; border-radius: 4px; cursor: pointer">
            Previous
          </button>
        </nuxt-link>
        <nuxt-link :to="`/products?page=${page + 1}`">
          <button style="padding: 8px 16px; background-color: #282c34; color: white; border: none; border-radius: 4px; cursor: pointer">
            Next
          </button>
        </nuxt-link>
      </div>
    </div>

    <!-- Footer -->
    <footer style="background-color: #282c34; color: white; padding: 10px 20px; text-align: center; margin-top: 20px">
      <p>&copy; 2023 Myntra Clone. All rights reserved.</p>
    </footer>
  </div>
</template>

<script>
export default {
  async asyncData({ query }) {
    const page = query.page || 1;
    const limit = 15; // Display 15 products per page
    const skip = (page - 1) * limit;

    const res = await axios.get(`https://dummyjson.com/products?limit=${limit}&skip=${skip}`);
    const products = res.data.products;

    return {
      products,
      page: parseInt(page),
    };
  },
};
</script>

<style scoped>
/* Add custom styles here if needed */
</style>
