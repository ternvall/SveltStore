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
		if (isOpen && product) {
			modal.showModal();
		} else {
			modal.close();
		}
	}

	function handleClose() {
		onClose();
	}
</script>

<dialog bind:this={modal} class="modal" on:close={handleClose}>
	<div class="modal-box">
		{#if product}
			<button class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2" on:click={handleClose}>✕</button>

			<img sizes="(max-width: 60px) 30px"
				src={product.thumbnail}
				alt={product.title}
				class="w-full h-16 object-cover rounded-lg mb-4"
			/>

			<h3 class="font-bold text-xl mb-2">{product.title}</h3>
			<p class="text-2xl font-bold text-blue-600 mb-4">${product.price}</p>
			<p class="text-gray-600 mb-4">{product.description}</p>

			<div class="flex justify-between text-sm text-gray-500 mb-4">
				<span>Brand: {product.brand}</span>
				<span>Stock: {product.stock}</span>
				<span>Rating: {product.rating}/5</span>
			</div>

			<button class="btn btn-primary w-full">Add to Cart</button>
		{/if}
	</div>
	<form method="dialog" class="modal-backdrop">
		<button on:click={handleClose}>close</button>
	</form>
</dialog>
