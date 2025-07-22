<script>
  import { onMount } from 'svelte';

  let scrollProgress = 0;

  function handleScroll() {
    const section = document.getElementById('section1');
    const rect = section.getBoundingClientRect();
    const windowHeight = window.innerHeight;

    const progress = Math.min(1, Math.max(0, 1 - rect.top / windowHeight));
    scrollProgress = progress;
  }

  onMount(() => {
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  });

  const subtitleWords = ['felix.', 'gardner.', 'bartoletta.', 'bowie.'];

  // Compute overlay opacity so it fades in faster than scrollProgress (up to full opacity)
  $: overlayOpacity = Math.min(scrollProgress * 2, 1);
</script>

<style>
  #section1 {
    height: 150vh;
    background-image: url('/Maternal-Mortality-Data-Storytelling/winners2.png');
    background-size: cover;
    background-position: center;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 2rem;
    box-sizing: border-box;
    overflow: hidden;
  }

  .overlay-fade {
    position: absolute;
    top: 0;
    right: 0;
    width: 40%;
    height: 100%;
    pointer-events: none;
    background: linear-gradient(to right, rgba(255,255,255,0), #888888);
    opacity: 0;
    transition: opacity 1s ease;
    z-index: 1.5;
  }

  .nike-text {
    font-family: 'NikeFont', sans-serif;
    font-size: 2rem;
    position: relative;
    z-index: 2; /* Above overlay */
  }

  .subtitle {
    font-size: 3rem;
    color: #f7f5eb;
    margin-top: 1rem;
    display: flex;
    gap: 0.4rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  .subtitle span.gray {
    color: gray;
    transition: color 1s ease;
  }

  .year-title {
    position: relative;
    font-size: 10rem;
    margin: 0;
  }

  .year-text {
    display: block;
    transition: color 1s ease, opacity 1s ease;
    color: #e3ff00;
    text-shadow: 1px 1px 0 #007052;
  }

  .year-text.gray {
    color: gray;
  }


</style>

<section id="section1">
  <div
    class="overlay-fade"
    style="opacity: {overlayOpacity};"
  ></div>

  <div class="content nike-text">
    <h1 class="year-title">
      <span
        class="year-text"
        class:gray={scrollProgress > 0.9} 
        style="opacity: 1; margin-bottom: 1rem;"
      >
        2016
      </span>
      <span id = "2023"
        class="year-text"
        class:gray={scrollProgress <= 0.9}
        style="opacity: {scrollProgress};"
      >
        2023
      </span>
    </h1>

    <div class="subtitle">
      {#each subtitleWords as word}
        <span class:gray={word === 'bowie.' && scrollProgress >= 0.999}>{word}</span>
      {/each}
    </div>
  </div>
</section>
