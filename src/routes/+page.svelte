<script lang="ts">
  import ProductModal from "$lib/components/ProductModal.svelte";
  import ProductThumbnail from "$lib/components/ProductThumbnail.svelte";
  import { onMount } from "svelte";

  interface Product {
    id: number;
    title: string;
    price: number;
    thumbnail: string;
    description: string;
    rating: number;
    brand: string;
    category: string;
    stock: number;
    discountPercentage: number;
    images: string[];
  }

  let products: Product[] = [];
  let selectedProduct: Product | null = null;
  let isModalOpen = false;
  let loading = true;

  onMount(async () => {
    try {
      const response = await fetch("https://dummyjson.com/products");
      const data = await response.json();
      products = data.products;
    } catch (err) {
      console.error("Error fetching products:", err);
    } finally {
      loading = false;
    }
  });

  function openModal(product: Product) {
    selectedProduct = product;
    isModalOpen = true;
  }

  function closeModal() {
    selectedProduct = null;
    isModalOpen = false;
  }

  // Group products into rows of 4
</script>

<svelte:head>
  <title>Product Catalog</title>
</svelte:head>

<div class=" mx-auto p-4">
  <h1 class="text-3xl font-bold text-center mb-8">Product Catalog</h1>

  {#if loading}
    <div class="flex justify-center">
      <div class="loading loading-spinner loading-lg"></div>
    </div>
  {:else}
    <div class="grid-container">
      {#each products as product}
        <div class="grid-item">
          <ProductThumbnail {product} onClick={openModal} />
        </div>
      {/each}
    </div>
  {/if}
</div>

<ProductModal product={selectedProduct} isOpen={isModalOpen} onClose={closeModal} />

<style>
  .grid-container {
    display: grid;
    /* Defines 6 columns with equal width, using '1fr' for a flexible unit */
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    /* Optional: Add some gap between grid items */
    gap: 8px; /* Adjust as needed */
    padding: 8px;
    /* --- Changes for Fixed Container --- */
    margin: 0 auto; /* Centers the container horizontally */
    box-sizing: border-box; /* Ensures padding is included in the max-width */
    /* --- End of Changes --- */
  }

  .grid-item {
    border: 1px solid #ddd;
    padding: 20px;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
</style>
