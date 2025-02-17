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
      initialSlide: 1,
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

<div bind:this={swiper} class="swiper-container">
  <div class="swiper-wrapper">
    {#each slides as slide}
      <div class="swiper-slide">
        <div class="image-container">
          <img src={cleaningImg.src} alt="cleaning" />
        </div>
        <div class="icon-container">
          <Icon icon={slide.icon} width={48} color={"#F3BC34"} />
        </div>
        <div class="content">
          <h3>{slide.title}</h3>
          <ul>
            {#each slide.features as feature}
              <li>
                <Icon icon={"mdi:check-bold"} width={20} />
                {feature}
              </li>
            {/each}
          </ul>
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

<style>
  .swiper-container {
    max-width: 1200px;
    justify-self: center;
  }
  .swiper-wrapper {
    display: flex;
    padding: 3rem;
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
