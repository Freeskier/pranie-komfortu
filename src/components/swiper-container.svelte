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
      slidesPerView: 3,
      coverflowEffect: {
        rotate: 0,
        modifier: 1.5,
        slideShadows: false,
        depth: 0,
        scale: 0.95,
      },
      initialSlide: 2,
      loop: true,
      centeredSlides: false,
      pagination: {
        dynamicBullets: true,
        clickable: true,
        clickableClass: `swiper-pagination-clickable`,
      },
      slideToClickedSlide: true,
      spaceBetween: 25,
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
    },
    {
      icon: "mdi:car-outline",
      title: "Pranie tapicerki samochodowej",
      features: [
        "Usuwamy plamy, zabrudzenia i nieprzyjemne zapachy.",
        "Stosujemy bezpieczne i skuteczne środki czystości.",
      ],
    },
    {
      icon: "mdi:sofa-outline",
      title: "Pranie tapicerki meblowej",
      features: [
        "Odnawiamy sofy, fotele i krzesła.",
        "Chronimy materiały przed szybkim zabrudzeniem.",
      ],
    },
    {
      icon: "mdi:car-outline",
      title: "Pranie tapicerki samochodowej",
      features: [
        "Usuwamy plamy, zabrudzenia i nieprzyjemne zapachy.",
        "Stosujemy bezpieczne i skuteczne środki czystości.",
      ],
    },
    {
      icon: "mdi:sofa-outline",
      title: "Pranie tapicerki meblowej",
      features: [
        "Odnawiamy sofy, fotele i krzesła.",
        "Chronimy materiały przed szybkim zabrudzeniem.",
      ],
    },
  ];
</script>

<div bind:this={swiper}>
  <div class="swiper-wrapper">
    {#each slides as slide}
      <div class="swiper-slide">
        <Icon icon={slide.icon} width={48} color={"#F3BC34"} />
        <img src={cleaningImg.src} alt="cleaning" />
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

<style>
  .swiper-wrapper {
    display: flex;
    padding: 3rem;
    z-index: 10;
    position: relative;
    max-width: 100%;
  }

  .swiper-slide {
    width: 200px;
    height: 300px;
    overflow: hidden;

    img {
      object-fit: cover;
      height: 200px;
    }
  }
</style>
