<script lang="ts">
	import Swiper from "swiper";
	import { Pagination, EffectCoverflow } from "swiper/modules";
	import { onMount } from "svelte";
	import Icon from "@iconify/svelte";
	import cleaningImg from "/src/assets/cleaning-carpet.jpg";

	let swiper: HTMLDivElement = $state()!;
	let currentExtraInfo: string = $state("");
	let isPopoverOpen: boolean = $state(false);

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
			icon: "mdi:floor-plan",
			title: "Doczyszczanie posadzek",
			features: [
				"Czyszczenie posadzek w domach, firmach i halach.",
				"Skutecznie usuwamy plamy i zabrudzenia.",
			],
			description: "Skuteczne czyszczenie posadzek każdego typu.",
			extraInfo: `
			<h2>Doczyszczanie Posadzek</h2>
			<p>Doczyszczanie posadzek to nasza specjalność. Skutecznie usuwamy plamy, zabrudzenia oraz wszelkie zanieczyszczenia z różnych rodzajów powierzchni. Nasze usługi obejmują czyszczenie posadzek w domach, biurach, sklepach czy halach przemysłowych.</p>
			<p>Dzięki profesjonalnym urządzeniom i odpowiednim środkom czyszczącym, jesteśmy w stanie przywrócić im doskonały wygląd i dbałość o każdy detal.</p>
			<div class="notice">
				<strong>W TRAKCIE SZKOLENIA DOSTĘPNE NIEBAWEM</strong>
			</div>
		`,
		},
		{
			icon: "mdi:air-filter",
			title: "Ozonowanie",
			features: ["Usuwamy bakterie, wirusy i alergeny.", "Eliminujemy nieprzyjemne zapachy."],
			description: "Ozonowanie, które skutecznie usuwa bakterie, wirusy i nieprzyjemne zapachy.",
			extraInfo: `
				<h2>Ozonowanie</h2>
				<p>Ozonowanie to skuteczna metoda dezynfekcji, która pozwala na eliminację bakterii, wirusów oraz nieprzyjemnych zapachów. Dzięki ozonowi poprawiamy jakość powietrza w pomieszczeniu, a także eliminujemy alergeny i zapachy, które trudno usunąć tradycyjnymi metodami.</p>
				<p>To świetna opcja dla osób cierpiących na alergie lub dla tych, którzy chcą zapewnić sobie czystsze i zdrowsze środowisko w swoim domu lub biurze.</p>
				<div class="price-link">
					<a href="/cennik#ozonowanie">Sprawdź szacunkowy koszt usługi – Cennik</a>
				</div>
			`,
		},
		{
			icon: "mdi:carpet",
			title: "Pranie dywanów i wykładzin",
			features: [
				"Przywracamy dywanom świeżość i żywe kolory.",
				"Głęboko oczyszczamy włókna z alergenów i kurzu.",
			],
			description:
				"Profesjonalne pranie dywanów i wykładzin, które przywróci im świeżość i czystość. Szybka realizacja i wysoka jakość usług!",
			extraInfo: `
				<h2>Pranie Dywanów i Wykładzin</h2>
				<p>Pranie dywanów i wykładzin to nasza specjalność. Używamy nowoczesnego sprzętu, który umożliwia szybkie i skuteczne czyszczenie. Dzięki wysokiej temperaturze prania oraz profesjonalnym środkom, nasze usługi gwarantują najlepsze efekty.</p>
				<p>Dodatkowo, oferujemy suszenie dywanów na miejscu, co znacząco skraca czas oczekiwania na efekt końcowy. Jeśli masz większą ilość dywanów, wykonamy usługę na wskroś, by zapewnić kompleksowe czyszczenie.</p>
				<div class="price-link">
					<a href="/cennik#pranie-dywanow-i-wykładzin">Sprawdź szacunkowy koszt usługi – Cennik</a>
				</div>
			`,
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
			extraInfo: `
				<h2>Pranie Tapicerki Meblowej</h2>
				<p>Przywrócenie czystości Twoim meblom jest proste z naszymi usługami. Skorzystaj z prania tapicerki meblowej, które efektywnie usuwa brud i plamy z materiałów różnego typu.</p>
				<p>Używamy tylko bezpiecznych preparatów, które nie uszkodzą tapicerki. Dzięki nowoczesnemu sprzętowi oraz doświadczeniu naszych pracowników, zapewniamy kompleksową i dokładną usługę.</p>
				<div class="price-link">
					<a href="/cennik#pranie-tapicerki-meblowej">Sprawdź szacunkowy koszt usługi – Cennik</a>
				</div>
			`,
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
			extraInfo: `
				<h2>Pranie Tapicerki Samochodowej i Detailing Wnętrza</h2>
				<p>Zadbaj o wnętrze swojego auta dzięki profesjonalnemu czyszczeniu i detailingowi. Oferujemy dwa pakiety:</p>

				<div class="packages">
					<div class="package">
						<h3>Kompleksowe czyszczenie auta:</h3>
						<ul>
							<li>Czyszczenie podsufitki</li>
							<li>Mycie okien wewnątrz</li>
							<li>Czyszczenie plastików</li>
							<li>Odkurzanie podłogi (tylko odkurzaczem)</li>
							<li>Pranie tapicerki</li>
							<li>Czyszczenie bagażnika</li>
						</ul>
					</div>

					<div class="package">
						<h3>Kompleksowe czyszczenie detailingowe auta:</h3>
						<ul>
							<li>Czyszczenie podsufitki</li>
							<li>Mycie okien wewnątrz</li>
							<li>Detailingowe czyszczenie plastików (szczelinowe, z użyciem pędzelków)</li>
							<li>Odkurzanie podłogi (odkurzaczem oraz powietrzem usuwającym 95% piasku i brudu)</li>
							<li>Pranie tapicerki</li>
							<li>Nałożenie dressingu ochronnego na plastiki</li>
							<li>Czyszczenie bagażnika</li>
						</ul>
					</div>
				</div>

				<p>Każdy pakiet zapewnia dokładną pielęgnację wnętrza pojazdu, dostosowaną do Twoich potrzeb. Z nami Twoje auto odzyska czystość i świeżość!</p>

				<div class="price-link">
					<a href="/cennik#pranie-tapicerki-samochodowej">Sprawdź szacunkowy koszt usługi – Cennik</a>
				</div>
			`,
		},

		{
			icon: "mdi:window-closed-variant",
			title: "Mycie okien i witryn",
			features: [
				"Myjemy powierzchnie szklane do 4 metrów wysokości.",
				"Dbamy o każdy detal bez smug i zacieków.",
			],
			description: "Mycie okien i witryn z dbałością o każdy detal.",
			extraInfo: `
				<h2>Mycie Okien/Witryn</h2>
				<p>Nasza usługa mycia okien i witryn obejmuje precyzyjne czyszczenie powierzchni szklanych, które przywraca ich blask. Pracujemy na wysokości do 4 metrów, co pozwala nam skutecznie dotrzeć do trudno dostępnych miejsc.</p>
				<p>Oferujemy mycie okien zarówno w domach, jak i biurach, a także czyszczenie witryn sklepowych i innych powierzchni szklanych. Działamy szybko, efektywnie i zawsze dbamy o to, by nie zostawić smug ani zacieków.</p>
				<div class="price-link">
					<a href="/cennik#mycie-okien-i-witryn">Sprawdź szacunkowy koszt usługi – Cennik</a>
				</div>
			`,
		},

		{
			icon: "mdi:toolbox-outline",
			title: "Wynajem sprzętu czyszczącego",
			features: [
				"Wynajem odkurzacza piorącego i chemii.",
				"Dodatkowe akcesoria i środki na trudne zabrudzenia.",
			],
			description: "Chcesz samodzielnie odświeżyć tapicerkę, dywan lub auto?",
			extraInfo: `
				<h2>Wynajem Sprzętu Piorącego i Innych Urządzeń</h2>
				<p>Nie masz budżetu na profesjonalne pranie tapicerki? Zrób to sam! Oferujemy wynajem odkurzacza piorącego Karcher Puzzi 10/1 wraz z chemią World of Clean, która działa lepiej niż standardowy proszek Karcher.</p>

				<div class="rental-info">
					<div class="rental-section">
						<h3>Koszt wynajmu:</h3>
						<ul>
							<li>✔️ 60 zł / 24h (1 proszek gratis)</li>
						</ul>
					</div>

					<div class="rental-section">
						<h3>W zestawie:</h3>
						<ul>
							<li>✔️ Opryskiwacz 1,5L</li>
							<li>✔️ Szczotka</li>
							<li>✔️ Możliwość dobrania ssawki (dywan, kanapa, auto)</li>
						</ul>
					</div>

					<div class="rental-section">
						<h3>Dodatki:</h3>
						<ul>
							<li>✔️ Specjalne środki na plamy, mocz i inne trudne zabrudzenia (cena ustalana indywidualnie)</li>
							<li>✔️ Wentylator Dri-Pod skracający czas schnięcia o połowę – 30 zł/dobę</li>
							<li>✔️ Farelka do Dri-Pod – 5 zł/dobę</li>
						</ul>
					</div>

					<div class="rental-section">
						<p>Dodatkowy proszek: 8 zł/szt.</p>
					</div>
				</div>

				<p>Nie gwarantujemy, że samemu usuną Państwo wszystkie zabrudzenia, ale na pewno pomożemy dobrać odpowiednie środki i sprzęt, aby efekt był jak najlepszy.</p>

				<div class="price-link">
					<a href="/wynajem">Sprawdź szczegóły wynajmu sprzętu</a>
				</div>
			`,
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
					<button
						class="more-info"
						onclick={() => {
							currentExtraInfo = slide.extraInfo;
							isPopoverOpen = true;
						}}
					>
						Dowiedz się więcej
					</button>
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

{#if isPopoverOpen}
	<div id="more-info-popover" class="popover">
		<div class="popover-content">
			<button class="close-btn" onclick={() => (isPopoverOpen = false)}>
				<Icon icon="mdi:close" width={24} />
			</button>
			{@html currentExtraInfo}
		</div>
		<div class="backdrop" onclick={() => (isPopoverOpen = false)}></div>
	</div>
{/if}

<style>
	.popover {
		position: fixed;
		inset: 0;
		z-index: 1000;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.popover-content {
		width: 80%;
		max-width: 800px;
		max-height: 80vh;
		overflow: auto;
		background-color: white;
		border-radius: 1rem;
		padding: 2rem;
		box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
		color: #09152a;
		position: relative;
		z-index: 1001;
	}

	.close-btn {
		position: absolute;
		top: 1rem;
		right: 1rem;
		background: none;
		border: none;
		cursor: pointer;
		color: #09152a;
		padding: 0.5rem;
	}

	.backdrop {
		position: fixed;
		inset: 0;
		background-color: rgba(9, 21, 42, 0.7);
		backdrop-filter: blur(4px);
		z-index: 1000;
	}

	:global(#more-info-popover h2) {
		color: #19a0b5;
		font-size: 1.8rem;
		margin-bottom: 1rem;
		font-family: "Caveat Variable", cursive;
	}

	:global(#more-info-popover h3) {
		color: #19a0b5;
		font-size: 1.3rem;
		margin-top: 1rem;
		margin-bottom: 0.5rem;
	}

	:global(#more-info-popover p) {
		margin-bottom: 1rem;
		line-height: 1.5;
	}

	:global(#more-info-popover ul) {
		list-style-type: none;
		margin-left: 1.5rem;
		margin-bottom: 1rem;
		line-height: 1.5;
	}

	:global(#more-info-popover .packages) {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 1.5rem;
		margin: 1.5rem 0;
	}

	:global(#more-info-popover .package) {
		background-color: #f7f7f7;
		padding: 1.5rem;
		border-radius: 0.75rem;
		box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
	}

	:global(#more-info-popover .rental-info) {
		background-color: #f7f7f7;
		padding: 1.5rem;
		border-radius: 0.75rem;
		margin: 1.5rem 0;
	}

	:global(#more-info-popover .rental-section) {
		margin-bottom: 1rem;
	}

	:global(#more-info-popover .price-link) {
		margin-top: 2rem;
		text-align: center;
	}

	:global(#more-info-popover .price-link a) {
		background-color: #19a0b5;
		color: white;
		padding: 0.75rem 1.5rem;
		border-radius: 0.5rem;
		text-decoration: none;
		font-weight: 600;
		transition: background-color 0.2s ease-in-out;
	}

	:global(#more-info-popover .price-link a:hover) {
		background-color: #158396;
	}

	:global(#more-info-popover .notice) {
		margin-top: 1.5rem;
		padding: 1rem;
		background-color: #f3bc34;
		color: #09152a;
		text-align: center;
		border-radius: 0.5rem;
		font-weight: 600;
	}

	@media (max-width: 768px) {
		:global(#more-info-popover .packages) {
			grid-template-columns: 1fr;
		}

		.popover-content {
			width: 90%;
			padding: 1.5rem;
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
