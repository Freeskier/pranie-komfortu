<script lang="ts">
	type Props = {
		beforeImg: string;
		afterImg: string;
	};

	type Circle = {
		cx: number;
		cy: number;
		r: number;
	};

	import before from "/src/assets/before_img.jpg";
	import after from "/src/assets/after_img.jpg";
	import { onMount } from "svelte";
	import { Spring } from "svelte/motion";
	import Icon from "@iconify/svelte";
	import { Slider } from "melt/builders";

	//   let { beforeImg, afterImg }: Props = $props();

	let sliderPosition = $state(50);
	let focused = $state(false);
	let circles: Circle[] = $state([]);
	let containerWidth = $state(600);
	let containerHeight = $state(400);

	const slider = new Slider({
		step: 0.01,
		min: 0,
		max: 100,
		value: 50,
		orientation: "horizontal",
		onValueChange: (num) => (sliderPosition = num),
	});

	const clip = $derived(`inset(0 ${100 - sliderPosition}% 0 0)`);
	const sliderX = $derived((sliderPosition / 100) * containerWidth);

	onMount(() => {
		// Adjust the count as needed.
		circles = generateCircles(300, containerWidth, containerHeight);
	});

	function generateCircles(count: number, width: number, height: number): Circle[] {
		const result: Circle[] = [];
		for (let i = 0; i < count; i++) {
			const cx = Math.random() * width;
			const cy = Math.random() * height;
			const r = 10 + Math.random() * (25 - 5); // radius between 10 and 50
			result.push({ cx, cy, r });
		}
		return result;
	}

	function getCircleOpacity(circleX: number, sliderX: number, threshold: number = 40): number {
		const distance = Math.abs(circleX - sliderX);
		// Linear fade: opacity 1 at the slider position, fading to 0 when distance >= threshold.
		return Math.max(0, 1 - distance / threshold);
	}

	function getCircleScale(circleX: number, sliderX: number, threshold: number = 100): number {
		const distance = Math.abs(circleX - sliderX);
		// When at the slider (distance 0), scale is 1.
		// When distance >= threshold, scale is clamped to 0.5.
		return Math.max(0.5, 1 - 0.5 * (distance / threshold));
	}

	function onfocus() {
		focused = true;
	}

	function onblur() {
		focused = false;
	}
</script>

<div bind:clientWidth={containerWidth} bind:clientHeight={containerHeight} class="container">
	<img src={before.src} alt="After" />

	<div class="before-container" style="clip-path: {clip};">
		<img src={after.src} alt="Before" />
	</div>
	<svg
		class="circle-overlay"
		width={containerWidth}
		height={containerHeight}
		viewBox={`0 0 ${containerWidth} ${containerHeight}`}
	>
		{#each circles as circle (circle.cx + "-" + circle.cy)}
			<circle
				cx={circle.cx}
				cy={circle.cy}
				r={circle.r * getCircleScale(circle.cx, sliderX)}
				fill="white"
				opacity={getCircleOpacity(circle.cx, sliderX)}
			/>
		{/each}
	</svg>
	<div class="slider-controls">
		<label for="image-slider" class="visually-hidden">Adjust Image Comparison</label>

		<div
			{...slider.root}
			class="slider-track"
			{onfocus}
			{onblur}
			aria-label="Image comparison slider"
		>
			<div {...slider.thumb} class="slider-thumb">
				<div class="icon-wrapper">
					<Icon icon={"mdi:chevron-left-right"} width={32} />
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	.container {
		position: relative;
		aspect-ratio: 3/2;
		max-width: 600px;
		width: 100%;
		overflow: hidden;
		user-select: none;
		border-radius: 1rem;
	}

	.slider-track {
		position: absolute;
		inset: 0;
	}

	.slider-thumb {
		position: absolute;
		background: #f3bc34;
		left: var(--percentage);
		top: 50%;
		transform: translate(-50%, -50%);
		width: 6px;
		height: 100%;

		& .icon-wrapper {
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			background-color: #f3bc34;
			border-radius: 50%;
			width: 2.5rem;
			height: 2.5rem;
			display: flex;
			align-items: center;
			justify-content: center;

			:global(svg) {
				color: white;
			}
		}
	}

	.thumb {
		width: 5px;
		height: 100%;
		position: absolute;
		top: 0;
		z-index: 100;
		background-color: #f3bc34;
		cursor: ew-resize;
		pointer-events: none;
	}

	.circle-overlay {
		position: absolute;
		top: 0;
		left: 0;
		z-index: 3;
		pointer-events: none;
	}

	/* Both images fill the container */
	.container img {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		object-fit: cover;
		pointer-events: none;
	}

	/* The before image container clips the image to reveal the diff */
	.before-container {
		position: absolute;
		top: 0;
		left: 0;
		height: 100%;
		overflow: hidden;
		object-fit: contain;
		width: 100%;
	}

	/* Styling for the slider controls container */
	.slider-controls {
		text-align: center;
		position: absolute;
		width: 100%;
		height: 100%;
		top: 50%;
		translate: 0 -50%;
		z-index: 10;
	}

	.visually-hidden {
		position: absolute;
		width: 1px;
		height: 1px;
		margin: -1px;
		padding: 0;
		border: 0;
		clip: rect(0, 0, 0, 0);
		overflow: hidden;
	}
</style>
