<script>
  const slides = [
    { id: 1, content: 'Slide 1', Image : 'bg-blue-500' },
    { id: 2, content: 'Slide 2', bgColor: 'bg-green-500' },
    { id: 3, content: 'Slide 3', bgColor: 'bg-purple-500' },
    { id: 4, content: 'Slide 4', bgColor: 'bg-pink-500' }
  ];
</script>

<h1 class="text-3xl font-bold mb-4">CSS-only Carousel</h1>
<p class="mb-6 text-gray-600">This carousel is sgh with Svelte and Tailwind CSS only.</p>

<section class="relative w-full max-w-4xl mx-auto" aria-label="Gallery">
  <!-- Carousel viewport -->
  <ol class="flex overflow-x-scroll snap-x snap-mandatory scroll-smooth hide-scrollbar">
    {#each slides as slide, i}
        <li
        id="carousel__slide{slide.id}"
        tabindex="0"
        class="relative flex-shrink-0 w-full h-96 snap-start snap-always"
        >
        <div class="relative w-full h-full {slide.bgColor} flex items-center justify-center text-white text-4xl font-bold">
            {slide.content}
            
            <!-- Previous button -->
            <a
            href="#carousel__slide{i === 0 ? slides.length : i}"
            class="absolute left-4 top-1/2 -translate-y-1/2 bg-white/30 hover:bg-white/50 text-white px-4 py-2 rounded-lg transition"
            >
            ←
            </a>
            
            <!-- Next button -->
            <a
            href="#carousel__slide{i === slides.length - 1 ? 1 : slide.id + 1}"
            class="absolute right-4 top-1/2 -translate-y-1/2 bg-white/30 hover:bg-white/50 text-white px-4 py-2 rounded-lg transition"
            >
            →
            </a>
        </div>
        </li>
    {/each}
  </ol>
  
  <!-- Navigation dots -->
  <aside class="absolute bottom-4 left-1/2 -translate-x-1/2 z-30">
    <ol class="flex gap-3">
      {#each slides as slide}
        <li>
          <a
            href="#carousel__slide{slide.id}"
            class="block w-3 h-3 rounded-full bg-white/50 hover:bg-white transition"
            aria-label="Go to slide {slide.id}"
          >
          </a>
        </li>
      {/each}
    </ol>
  </aside>
</section>

<style>
  .hide-scrollbar {
    -ms-overflow-style: none;
    scrollbar-width: none;
  }
  
  .hide-scrollbar::-webkit-scrollbar {
    display: none;
  }
</style>
