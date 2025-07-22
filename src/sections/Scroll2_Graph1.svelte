<!--
<script>
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";
  import PaperText from "../lib/PaperText.svelte";
</script>

<div class = "nike-text">
<Scroller layout="right">
    {#snippet sticky()}
      <img class="duck-img" src = "maternal_mortality.png" alt ="graph1">
    {/snippet}

    {#snippet scrolly()}
      <PaperText>
        <p>According to the National Institutes of Health, Black Americans have an elevated risk of preeclampsia and eclampsia 
          - which involve high blood pressure, and in the most serious cases cause pregnant women to develop seizures or coma.</p>
      </PaperText>
      <PaperText>
        <p>In 2021 it was 69.9 per 100,000, which is 2.6 times higher than the rate for White women.</p>
      </PaperText>
    {/snippet}
</Scroller>
</div>
-->

<script lang="ts">
  import { onMount } from 'svelte';
  import Scroller from "../lib/Scroller.svelte";
  import PaperText from "../lib/PaperText.svelte";
  import { fade } from 'svelte/transition';

  let showUnderlinePreeclampsia = false;
  let showUnderlineEclampsia = false;
  let showCircle = false;

  // Targets to highlight
  let observePreeclampsia: HTMLSpanElement;
  let observeEclampsia: HTMLSpanElement;
  let observeCircleTarget: HTMLSpanElement;

  // Delay timers
  let delayTimeoutPreeclampsia: ReturnType<typeof setTimeout>;
  let delayTimeoutEclampsia: ReturnType<typeof setTimeout>;
  let delayTimeoutCircle: ReturnType<typeof setTimeout>;

  // used ChatGPT to implement / debug this section (since there were multiple DOM elements)

    // Waits until each element is at least 70% visible
    //If visible for 1 second, it shows a corresponding UI effect (like underline or circle)
    // If the element scrolls out of view, cancel effect or timeout (immediate).
    // Cleans up everything when the component is done

  onMount(() => {
    if (typeof window === 'undefined') return;

    function createObserver(
      target: HTMLElement,
      setShowFn: (show: boolean) => void,
      delayTimeoutRef: { current?: ReturnType<typeof setTimeout> }
    ) {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach(entry => {
            if (entry.isIntersecting) {
              delayTimeoutRef.current = setTimeout(() => {
                setShowFn(true);
              }, 1000);
            } else {
              clearTimeout(delayTimeoutRef.current);
              setShowFn(false);
            }
          });
        },
        { threshold: 0.7 }
      );
      observer.observe(target);
      return () => {
        observer.unobserve(target);
        clearTimeout(delayTimeoutRef.current);
      };
    }

    // Create observers for preeclampsia, eclampsia, circle
    const cleanupPreeclampsia = observePreeclampsia
      ? createObserver(observePreeclampsia, (v) => (showUnderlinePreeclampsia = v), { current: delayTimeoutPreeclampsia })
      : () => {};
    const cleanupEclampsia = observeEclampsia
      ? createObserver(observeEclampsia, (v) => (showUnderlineEclampsia = v), { current: delayTimeoutEclampsia })
      : () => {};
    const cleanupCircle = observeCircleTarget
      ? createObserver(observeCircleTarget, (v) => (showCircle = v), { current: delayTimeoutCircle })
      : () => {};

    return () => {
      cleanupPreeclampsia();
      cleanupEclampsia();
      cleanupCircle();
    };
  });
</script>

<div class="nike-text">
  <Scroller layout="left">
    {#snippet sticky()}
      <img class="duck-img" src="maternal_mortality.png" alt="maternal_mortality" />
    {/snippet}

    <!--underline text accordingly-->
    {#snippet scrolly()}
      <PaperText>
        <div class="text-wrapper" style="position: relative;">
          <p>
            According to the National Institutes of Health, or NIH, Black Americans have an elevated risk of 
            <span bind:this={observePreeclampsia} class="highlighted-underline" style="position: relative;">
              preeclampsia
              {#if showUnderlinePreeclampsia}
                <img
                  src="underline.png"
                  alt="underline preeclampsia"
                  class="underline-overlay"
                  transition:fade
                />
              {/if}
            </span>
            {' '}and{' '}
            <span bind:this={observeEclampsia} class="highlighted-underline" style="position: relative;">
              eclampsia
              {#if showUnderlineEclampsia}
                <img
                  src="underline.png"
                  alt="underline eclampsia"
                  class="underline-overlay"
                  transition:fade
                />
              {/if}
            </span>
            -- which involve high blood pressure, and in the most serious cases cause pregnant women to develop seizures or coma.
          </p>
        </div>
      </PaperText>

      <PaperText>
        <div class="text-wrapper" style="position: relative;">
          <p>
            In 2021, the maternal mortality rate of Black women was 69.9 per 100,000, which is a rate
            <span bind:this={observeCircleTarget} class="highlighted-number" style="position: relative;">
              2.6 times higher
            </span>
            than the rate of White women.
          </p>

          {#if showCircle}
            <img
              src="circle.png"
              alt="circle highlight"
              class="circle-overlay"
              transition:fade
              style="top: {observeCircleTarget?.offsetTop}px; left: {observeCircleTarget?.offsetLeft}px;"
            />
          {/if}
        </div>
      </PaperText>
    {/snippet}
  </Scroller>
</div>

<style>

  .nike-text {
    font-family: 'NikeFont', sans-serif;
    font-size: 2rem;
    background-color: black;
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
    transform: translate(-20%, -20%);
  }

  .highlighted-number {
    position: relative;
    z-index: 1;
  }

  .circle-overlay {
    position: absolute;
    width: 100px;
    pointer-events: none;
    z-index: 2;
    transform: translate(-20%, -20%);
  }
</style>
