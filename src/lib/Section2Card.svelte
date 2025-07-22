<script>
  import { onMount, onDestroy } from 'svelte';

  export let title;
  export let subtitle;
  export let sub2;
  export let sub3;

  let scrollX = 0;
  let scrollFraction = 0;

  function handleScroll() {
    const scrollTop = window.scrollY;
    const docHeight = document.documentElement.scrollHeight - window.innerHeight;
    scrollFraction = docHeight ? scrollTop / docHeight : 0;
    scrollX = scrollFraction * 2500;  // max 300px shift
  }

  onMount(() => {
    window.addEventListener('scroll', handleScroll);
    handleScroll();
  });

  onDestroy(() => {
    window.removeEventListener('scroll', handleScroll);
  });
</script>

<div class="title-card" style="height: 150vh;">
  <div class="content nike-text" style="text-align:center;">
    <h1
 style="transform: translateX({scrollX}px); transition: transform .1s ease;"
    >
      {title}
    </h1>
    <p
      style="transform: translateX({-scrollX}px); transition: transform 0.1s ease;"
    >
      {subtitle}
    </p>
    <p
      style="transform: translateX({scrollX}px); transition: transform 0.1s ease;"
    >
      {sub2}
    </p>
    <p
      style="transform: translateX({-scrollX}px); transition: transform 0.1s ease;"
    >
      {sub3}
    </p>
  </div>
</div>

<style>
  @font-face {
    font-family: 'NikeFont';
    src: url('/Maternal-Mortality-Data-Storytelling/fonts/NIKE.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
  }

  .nike-text {
    font-family: 'NikeFont', sans-serif;
    font-size: 2rem;
  }

  .title-card {
    background-image: url('/Maternal-Mortality-Data-Storytelling/tori3.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 2rem;
    box-sizing: border-box;
  }

  .title-card {
    height: 150vh; /* taller for scroll */
  }

  h1 {
    font-size: 3rem;
    margin: 0;
    color: #e3ff00;
    text-shadow: 1px 1px 0 #007052;
  }

  p {
    font-size: 1.8rem;
    color: #f7f5eb;
    margin-top: 1rem;
  }

  h1, p {
    transition: transform 0.2s ease;
    will-change: transform;
    position: relative;
  }

  @media (max-width: 600px) {
    h1 {
      font-size: 2.2rem;
    }
    p {
      font-size: 1.4rem;
    }
  }
</style>

