
<!--
<script>
    import TitleCard from "../lib/TitleCard.svelte";
    
    const title = "WOMEN OF AMERICA";
    const subtitle = "felix. gardner. bartoletta. bowie.";
</script>

<TitleCard {title} {subtitle} />
-->

<script>
  import { onMount, onDestroy } from 'svelte';

  let scrollXTitle = 0;
  let scrollXSubtitle = 0;

  function handleScroll() {
    const scrollTop = window.scrollY;
    const docHeight = document.documentElement.scrollHeight - window.innerHeight;
    const scrollFraction = docHeight ? scrollTop / docHeight : 0;

    scrollXTitle = scrollFraction * 20000;      
    scrollXSubtitle = -scrollFraction * 20000; 

    // For debugging - check location calculating
    // console.log('scrollTop:', scrollTop, 'scrollXTitle:', scrollXTitle);
  }

  onMount(() => {
    window.addEventListener('scroll', handleScroll);
    handleScroll();
  });

  onDestroy(() => {
    window.removeEventListener('scroll', handleScroll);
  });
</script>

<style>
  @font-face {
    font-family: 'NikeFont';
    src: url('/scrollytelling-starter/fonts/NIKE.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
  }

  .nike-text {
    font-family: 'NikeFont', sans-serif;
    font-size: 2rem;
  }

  .title-card {
    background-image: url('/scrollytelling-starter/handoff1.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    height: 150vh; 
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 2rem;
    box-sizing: border-box;
  }

  h1, p {
    transition: transform 0.3s ease;
    will-change: transform;
    position: relative;
    margin: 0.5rem 0;
    color: #e3ff00;
    text-shadow: 1px 1px 0 #007052;
  }

  p {
    color: #f7f5eb;
  }

  p {
  margin-left: 1.5rem; 
  margin-bottom: 0.5rem; 
}

</style>

<div class="title-card nike-text">
  <h1 style="transform: translateX({scrollXTitle}px);">
    WOMEN OF AMERICA
  </h1>
  <p style="transform: translateX({scrollXSubtitle}px);">
    felix. gardner. bartoletta. bowie.
  </p>
</div>
