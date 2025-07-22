<!--
<script>
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";
  import NewsText from "../lib/NewsText.svelte";
</script>

<div class = "nike-text">
<Scroller layout="right">
    {#snippet sticky()}
      <img class="duck-img" src = "tv4.png" alt ="tv">
    {/snippet}

    {#snippet scrolly()}
      <ArticleText>
        <p>At just 32 years old, Olympic Gold Medalist Tori Bowie, passed due to complications with childbirth.</p>
      </ArticleText>
      <ArticleText>
        <p>Her story in one of many - involving otherwise healthy black women.</p>
      </ArticleText>
    {/snippet}
</Scroller>
</div>

-->

<script lang="ts">
  import { onMount } from 'svelte';
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";
  import { fade } from 'svelte/transition';

  let showUnderline = false;
  let observeUnderlineTarget: HTMLSpanElement;
  let delayTimeout: ReturnType<typeof setTimeout>;

  // draw the underline effect (delayed) after the page loads - mimic annotation
  onMount(() => {
    if (typeof window === 'undefined') return;

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            delayTimeout = setTimeout(() => {
              showUnderline = true;
            }, 1000); // delay here
          } else {
            clearTimeout(delayTimeout);
            showUnderline = false;
          }
        });
      },
      { threshold: 0.8 }
    );

    if (observeUnderlineTarget) observer.observe(observeUnderlineTarget);

    return () => {
      if (observeUnderlineTarget) observer.unobserve(observeUnderlineTarget);
      clearTimeout(delayTimeout);
    };
  });
</script>

<div class="nike-text">
  <Scroller layout="right">
    {#snippet sticky()}
      <img class="duck-img" src="tv4.png" alt="tv" />
    {/snippet}

    {#snippet scrolly()}
      <ArticleText>
        <p>At just 32 years old, Olympic Gold Medalist Tori Bowie, passed due to complications with childbirth.</p>
      </ArticleText>

      <ArticleText>
        <p>
          <span
            bind:this={observeUnderlineTarget}
            class="highlighted-underline"
            style="position: relative;"
          >
            Her story in one of many
            {#if showUnderline} <!--add underline here-->
              <img
                src="underline.png"
                alt="underline highlight"
                class="underline-overlay"
                transition:fade
              />
            {/if}
          </span>
          {' '} - involving otherwise healthy Black women.
        </p>
      </ArticleText>
    {/snippet}
  </Scroller>
</div>

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
    background-image: url('/Maternal-Mortality-Data-Storytelling/news4.jpeg');
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
  }

  .nike-text {
    position: relative;
    z-index: 0;
  }

  .duck-img {
    width: 90%;
    margin: 0 auto;
    display: block;
  }

  .highlighted-underline {
    display: inline-block;
  }

.underline-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  pointer-events: none;
  z-index: 2;
  transform-origin: left;
  animation: underline-draw 1.5s ease forwards;
}

</style>


