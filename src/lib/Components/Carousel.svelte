<script>
    import { onMount } from 'svelte'
    import bg from '$lib/assets/bg.jpg'
    import food from '$lib/assets/food.jpg'
    
    let currentIndex = 0
    let carouselElement
    const images = [
        { src: bg, alt: "restaurant pictures #1" },
        { src: food, alt: "restaurant pictures #2" }
    ]
    
    function goToNext() {
        currentIndex = (currentIndex + 1) % images.length
        scrollCarousel()
    }
    
    function goToPrev() {
        currentIndex = (currentIndex - 1 + images.length) % images.length
        scrollCarousel()
    }
    
    function scrollCarousel() {
        if (carouselElement) {
            const scrollPosition = currentIndex * carouselElement.offsetWidth
            carouselElement.scrollTo({
                left: scrollPosition,
                behavior: 'smooth'
            })
        }
    }
    
    // Initialize carousel position
    onMount(() => {
        scrollCarousel()
    })
    
    // Auto-scroll when currentIndex changes
    $: if (carouselElement) {
        scrollCarousel()
    }
</script>

<!-- Src: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Overflow/Carousels -->

<div class="carousel" bind:this={carouselElement} aria-label="Pictures of meals">
    {#each images as image, i (i)}
        <div class="carousel__img" class:active={i === currentIndex}>
            <img src={image.src} alt={image.alt}>
        </div>
    {/each}
</div>

<div class="carousel-controls">
    <button
        class="carousel-btn prev-btn"
        on:click={goToPrev}
        aria-label="Previous image"
    >
        ←
    </button>
    <button
        class="carousel-btn next-btn"
        on:click={goToNext}
        aria-label="Next image"
    >
        →
    </button>
</div>

<style>
    .carousel {
        width: 100%;
        height: 60vh;
        display: flex;
        position: relative;
        overflow-x: scroll;
        overflow: hidden;
        scroll-snap-type: x mandatory;
        anchor-name: --my-carousel;
        scroll-behavior: smooth;
        border-radius: 8px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }

    .carousel__img {
        min-width: 100%;
        min-height: 100%;
        flex: 0 0 100%;
        scroll-snap-align: center;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .carousel__img img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .carousel-controls {
        position: relative;
        width: 100%;
        margin: 0 auto;
    }

    .carousel-btn {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        background: #ac0000;
        color: white;
        border: none;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        font-size: 1.2rem;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all 0.3s ease;
        z-index: 10;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }

    .carousel-btn:hover {
        background: #8b0000;
        transform: translateY(-50%) scale(1.1);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    }

    .carousel-btn:focus {
        outline: 2px solid #ffffff;
        outline-offset: 2px;
    }

    .carousel-btn:active {
        transform: translateY(-50%) scale(0.95);
    }

    .prev-btn {
        left: 1rem;
    }

    .next-btn {
        right: 1rem;
    }

    @media (max-width: 768px) {
        .carousel {
            width: 100%;
            height: 40vh;
        }
        
        .carousel-btn {
            width: 35px;
            height: 35px;
            font-size: 1rem;
        }
        
        .prev-btn {
            left: 1rem;
        }
        
        .next-btn {
            right: 1rem;
        }
    }
</style>