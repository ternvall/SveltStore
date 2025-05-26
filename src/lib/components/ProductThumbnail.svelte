<script lang="ts">
	type Product = {
		id: number;
		title: string;
		description: string;
		price: number;
		discountPercentage: number;
		rating: number;
		stock: number;
		brand: string;
		category: string;
		thumbnail: string;
		images: string[];
	};

	export let product: Product;

	export let onClick: (product: Product) => void;
</script>

<div
	class="w-full bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow cursor-pointer border overflow-hidden group"
	on:click={() => onClick(product)}
	role="button"
	tabindex="0"
	on:keydown={(e) => e.key === 'Enter' && onClick(product)}
>
	<div class="flex items-center space-x-4 p-4 border border-gray-200 rounded-lg">
		<img
			src={product.thumbnail}
			alt={product.title}
	class="product-thumbnail"
		/>

		<!-- Price in top corner -->
		<div class="absolute top-2 right-2 bg-blue-600 text-white text-xs font-bold px-2 py-1 rounded">
			${product.price}
		</div>

		<!-- Name on bottom -->
		<div class="absolute bottom-0 left-0 right-0 bg-black bg-opacity-70 text-white p-2">
			<p class="text-xs font-medium truncate">{product.title}</p>
		</div>
	</div>
</div>

<style>
  .product-thumbnail {
    width: 128px !important; /* Overrides Tailwind */
    height: 128px;
  }
</style>
