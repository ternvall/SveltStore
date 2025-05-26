<script lang="ts">
  export let product: {
    id: number;
    title: string;
    price: number;
    thumbnail: string;
    description: string;
    rating: number;
    brand: string;
    category: string;
    stock: number;
  } | null = null;

  export let isOpen = false;
  export let onClose: () => void;

  let modal: HTMLDialogElement;

  $: if (modal) {
    if (isOpen && product) modal.showModal();
    else modal.close();
  }
</script>

<dialog bind:this={modal} class="modal" on:close={onClose}>
  <div class="modal-box">
    {#if product}
      <!-- <button
        class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2"
        on:click={onClose}>✕</button
      > -->
      <div class="flex-container">
        <div class="flex-box box-one">
          <img
            src={product.thumbnail}
            alt={product.title}
            class="w-full h-16 object-cover rounded-lg mb-4"
          />

          <p class="text-2xl font-bold text-blue-600 mb-4">${product.price}</p>
        </div>
        <div class="flex-box box-two">
          <h3 class="font-bold text-xl mb-2">{product.title}</h3>
          <p class="text-gray-600 mb-4">{product.description}</p>

          <ul class="flex justify-between text-sm text-gray-500 mb-4">
            <li>Brand: {product.brand}</li>
            <li>Stock: {product.stock}</li>
            <li>Rating: {product.rating}/5</li>
          </ul>
        </div>
      </div>
    {/if}
  </div>

  <div style="display: flex; justify-content: end; margin-top: 20px; gap: 4px; /">
    <form method="dialog" class="modal-backdrop">
      <button on:click={onClose}>Close</button>
    </form>

    <button class="btn btn-primary w-full">Add to Cart</button>
  </div>
</dialog>

<style>
  .flex-container {
    display: flex; /* Makes this a flex container */
    flex-wrap: wrap; /* Allows items to wrap to the next line if needed (though not strictly necessary for 2 items here, good practice) */
    gap: 2px; /* Space between the boxes */
    margin: 20px auto; /* Center the container on the page */
  }

  /* Styling for individual boxes */
  .flex-box {
    flex: 1; /* Allows boxes to grow and shrink, distributing available space */
    max-width: 300px; /* Ensures boxes don't get too small before stacking */
    display: flex; /* Make content inside box flex, useful for internal alignment */
    flex-direction: column; /* Stack content inside the box vertically */
    justify-content: space-between; /* Pushes content to top/bottom if height varies */
  }
</style>
