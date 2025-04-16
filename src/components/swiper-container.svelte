<script lang="ts">
	import Swiper from "swiper";
	import { Pagination, EffectCoverflow } from "swiper/modules";
	import { onMount } from "svelte";
	import Icon from "@iconify/svelte";
	import cleaningImg from "/src/assets/cleaning-carpet.jpg";

	let swiper: HTMLDivElement = $state()!;

	onMount(() => {
		const swipero = new Swiper(swiper, {
			modules: [Pagination, EffectCoverflow],
			speed: 500,
			effect: "coverflow",
			breakpoints: {
				0: {
					slidesPerView: 1.5,
				},
				640: {
					slidesPerView: 2,
				},
				1024: {
					slidesPerView: 3.5,
				},
			},
			coverflowEffect: {
				rotate: 0,
				modifier: 1.5,
				slideShadows: false,
				depth: 0,
				scale: 0.95,
			},
			initialSlide: 3.25,
			loop: false,
			centeredSlides: true,
			pagination: {
				dynamicBullets: true,
				clickable: true,
				clickableClass: `swiper-pagination-clickable`,
			},
			slideToClickedSlide: true,
			spaceBetween: 30,
		});
	});

	const slides = [
		{
			icon: "mdi:carpet",
			title: "Pranie dywanów i wykładzin",
			features: [
				"Przywracamy dywanom świeżość i żywe kolory.",
				"Głęboko oczyszczamy włókna z alergenów i kurzu.",
			],
			description:
				"Profesjonalne pranie dywanów i wykładzin, które przywróci im świeżość i czystość. Szybka realizacja i wysoka jakość usług!",
			extraInfo:
				"Używamy nowoczesnego sprzętu, który umożliwia szybkie i skuteczne czyszczenie. Dzięki wysokiej temperaturze prania oraz profesjonalnym środkom, nasze usługi gwarantują najlepsze efekty. Dodatkowo, oferujemy suszenie dywanów na miejscu. Jeśli masz większą ilość dywanów, wykonamy usługę na wskroś, by zapewnić kompleksowe czyszczenie.",
		},
		{
			icon: "mdi:car-outline",
			title: "Pranie tapicerki samochodowej",
			features: [
				"Usuwamy plamy, zabrudzenia i nieprzyjemne zapachy.",
				"Stosujemy bezpieczne i skuteczne środki czystości.",
			],
			description:
				"Oferujemy dwa warianty czyszczenia wnętrza auta – standardowe oraz detailingowe. Dokładne odświeżenie tapicerki i plastików.",
			extraInfo:
				"Zadbaj o wnętrze swojego auta dzięki profesjonalnemu czyszczeniu i detailingowi. Pakiet standardowy: czyszczenie podsufitki, mycie okien, plastików, pranie tapicerki. Detailing: czyszczenie szczelinowe, użycie pędzelków, odkurzanie sprężonym powietrzem, dressing ochronny na plastiki.",
		},
		{
			icon: "mdi:sofa",
			title: "Pranie tapicerki meblowej",
			features: [
				"Skutecznie usuwamy brud i plamy z mebli.",
				"Używamy bezpiecznych środków czystości.",
			],
			description:
				"Pranie tapicerki meblowej, które ożywi Twoje meble i usunie wszelkie zabrudzenia. Odświeżenie bez uszkodzenia materiału!",
			extraInfo:
				"Przywrócenie czystości Twoim meblom jest proste z naszymi usługami. Używamy tylko bezpiecznych preparatów. Zapewniamy kompleksową i dokładną usługę z wykorzystaniem nowoczesnego sprzętu.",
		},
		{
			icon: "mdi:window-closed-variant",
			title: "Mycie okien i witryn",
			features: [
				"Myjemy powierzchnie szklane do 4 metrów wysokości.",
				"Dbamy o każdy detal bez smug i zacieków.",
			],
			description: "Mycie okien i witryn z dbałością o każdy detal.",
			extraInfo:
				"Precyzyjne czyszczenie powierzchni szklanych, przywracające blask. Oferujemy mycie w domach, biurach, sklepach, do wysokości 4m. Działamy szybko i efektywnie.",
		},
		{
			icon: "mdi:air-filter",
			title: "Ozonowanie",
			features: ["Usuwamy bakterie, wirusy i alergeny.", "Eliminujemy nieprzyjemne zapachy."],
			description: "Ozonowanie, które skutecznie usuwa bakterie, wirusy i nieprzyjemne zapachy.",
			extraInfo:
				"Ozonowanie to skuteczna metoda dezynfekcji i poprawy jakości powietrza. Eliminuje alergeny i zapachy niedostępne dla tradycyjnych metod. Idealne dla alergików.",
		},
		{
			icon: "mdi:floor-plan",
			title: "Doczyszczanie posadzek",
			features: [
				"Czyszczenie posadzek w domach, firmach i halach.",
				"Skutecznie usuwamy plamy i zabrudzenia.",
			],
			description: "Skuteczne czyszczenie posadzek każdego typu.",
			extraInfo:
				"Doczyszczanie posadzek obejmuje różne typy powierzchni: biura, sklepy, hale. Używamy profesjonalnych środków i sprzętu. Dostępne wkrótce – w trakcie szkolenia.",
		},
		{
			icon: "mdi:toolbox-outline",
			title: "Wynajem sprzętu czyszczącego",
			features: [
				"Wynajem odkurzacza piorącego i chemii.",
				"Dodatkowe akcesoria i środki na trudne zabrudzenia.",
			],
			description: "Chcesz samodzielnie odświeżyć tapicerkę, dywan lub auto?",
			extraInfo:
				"Wynajmij profesjonalny odkurzacz piorący Karcher Puzzi 10/1. W zestawie: proszki czyszczące, opryskiwacz, szczotki, ssawki. Dodatkowo: środki na plamy, wentylator Dri-Pod, farelka. Pomagamy dobrać odpowiednie środki.",
		},
	];
</script>

<div bind:this={swiper} class="swiper-container">
	<div class="swiper-wrapper">
		{#each slides as slide, index}
			<div class="swiper-slide">
				<div class="image-container">
					<img src={`/swiper-images/slide_${index + 1}.jpg`} alt="cleaning" />
				</div>
				<div class="icon-container">
					<Icon icon={slide.icon} width={48} color={"#F3BC34"} />
				</div>
				<div class="content">
					<h3>{slide.title}</h3>
					<p>{slide.description}</p>
					<ul>
						{#each slide.features as feature}
							<li>
								<Icon icon={"mdi:check-bold"} width={20} />
								{feature}
							</li>
						{/each}
					</ul>
					<button popovertarget="more-info-popover" class="more-info">Dowiedz się więcej</button>
				</div>
			</div>
		{/each}
	</div>
	<!-- If we need pagination -->
	<div class="swiper-pagination"></div>

	<!-- If we need navigation buttons -->
	<div class="swiper-button-prev"></div>
	<div class="swiper-button-next"></div>

	<!-- If we need scrollbar -->
	<div class="swiper-scrollbar"></div>
</div>

<div id="more-info-popover" popover></div>

<style>
	#more-info-popover {
		position: fixed;
		inset: 0;
		width: fit-content;
		height: fit-content;
		margin: auto;
		border: solid;
		padding: 0.25em;
		overflow: auto;
		color: CanvasText;
		background-color: coral;
		z-index: 1000;

		&::backdrop {
			backdrop-filter: blur(0px);
			transition: backdrop-filter 300ms;
		}

		&:popover-open::backdrop {
			backdrop-filter: blur(6px);
			background-color: #ffffff66;
		}
	}

	.swiper-container {
		max-width: 1400px;
		margin: 0 auto;
		overflow: hidden;
	}
	.swiper-wrapper {
		display: flex;
		z-index: 10;
		position: relative;
	}

	.swiper-slide {
		display: grid;
		overflow: hidden;
		flex-shrink: 0;
		border-radius: 1rem;
		background-color: white;
		box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.3);
		grid-template-rows: auto auto 1fr;
		margin-bottom: 2rem;

		ul {
			list-style: none;
		}

		.image-container {
			position: relative;
			overflow: hidden;
			aspect-ratio: 16/9;
			img {
				object-fit: cover;
				z-index: -1;
				width: 100%;
			}
		}
		.icon-container {
			display: flex;
			justify-content: center;
			align-items: center;
			height: 4rem;
			aspect-ratio: 1;
			background-color: white;
			border-radius: 50%;
			border: 2px solid #f3bc34;
			align-self: end;
			justify-self: center;
			translate: 0 -50%;
		}

		.content {
			display: grid;
			gap: 0.5rem;
			padding-inline: 1.5rem;
			padding-bottom: 2rem;
			margin-top: -1.5rem;

			.more-info {
				justify-self: flex-end;
				width: fit-content;
				height: 2.5rem;
				background: transparent;
				border: 2px solid #f3bc34;
				padding: 0.25rem;
				border-radius: 0.5rem;
				font-family: inherit;
				font-size: inherit;
				font-weight: 600;
				color: #f3bc34;
				/* text-decoration: dashed;
				text-decoration-line: underline;
				text-decoration-color: #f3bc34;
				text-decoration-thickness: 3px;
				text-underline-offset: 0.3rem; */
				cursor: pointer;
			}

			ul {
				display: grid;
				gap: 0.25rem;
			}

			li {
				font-weight: 500;
				display: flex;
				gap: 0.5rem;
			}
			h3 {
				color: #09152a;
			}

			:global(svg) {
				color: #f3bc34;
				flex-shrink: 0;
			}
		}
	}
</style>
