<script>
  import { onMount, onDestroy } from 'svelte';

  let { title, subtitle } = $props();

  let scrollXTitle = 0;
  let scrollXSubtitle = 0;

  function handleScroll() {
  const scrollTop = window.scrollY;
  const docHeight = document.documentElement.scrollHeight - window.innerHeight;
  const scrollFraction = docHeight ? scrollTop / docHeight : 0;

    scrollXTitle = scrollFraction * 300;  // 300px max shift right
    scrollXSubtitle = -scrollFraction * 300; // 300px max shift left


  console.log('scrollTop:', scrollTop, 'scrollFraction:', scrollFraction, 'scrollXTitle:', scrollXTitle);
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
    <h1 style="transform: translateX({scrollXTitle}px); transition: transform 0.1s ease;">
      {title}
    </h1>
    <p style="transform: translateX({scrollXSubtitle}px); transition: transform 0.1s ease;">
      {subtitle}
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
    background-image: url('/Maternal-Mortality-Data-Storytelling/handoff1.png');
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
  height: 150vh; /* instead of 100vh */
}


  h1 {
    font-size: 3rem;
    margin: 0;
    color: #e3ff00;
    text-shadow: 1px 1px 0 #007052;
  }

  p {
    font-size: 1.3rem;
    color: #f7f5eb;
    margin-top: 1rem;
  }

  h1, p {
  transition: transform 0.2s ease;
  will-change: transform;
  position: relative;


}
h1 {
  border: 2px solid yellow;
}

p {
  border: 2px solid cyan;
}


  @media (max-width: 600px) {
    h1 {
      font-size: 2.2rem;
    }

    p {
      font-size: 1.1rem;
    }
  }
</style>
