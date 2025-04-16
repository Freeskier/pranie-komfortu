<script lang="ts">
	import { onMount } from "svelte";
	import PhotoSwipeLightbox from "photoswipe/lightbox";
	import "photoswipe/style.css";

	type Props = {
		images: { src: string; width: number; height: number }[];
	};

	const { images }: Props = $props();

	let galleryEl: HTMLDivElement;
	let lightbox: PhotoSwipeLightbox;

	onMount(() => {
		lightbox = new PhotoSwipeLightbox({
			gallery: galleryEl,
			children: "a",
			pswpModule: () => import("photoswipe"),
		});
		lightbox.init();

		return () => {
			lightbox.destroy();
		};
	});
</script>

<div bind:this={galleryEl} class="gallery-grid">
	{#each images as item (item.src)}
		<a href={item.src} data-pswp-width={item.width} data-pswp-height={item.height}>
			<img src={item.src} alt="Gallery image" class="thumbnail" />
		</a>
	{/each}
</div>

<style>
	.gallery-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 10px;
		max-width: 1200px;
		margin: 0 auto;
		padding-top: 2rem;
	}

	.thumbnail {
		width: 100%;
		height: 150px;
		object-fit: cover;
		border-radius: 8px;
		cursor: pointer;
		transition: opacity 0.3s ease;
	}

	.thumbnail:hover {
		opacity: 0.8;
	}
</style>
