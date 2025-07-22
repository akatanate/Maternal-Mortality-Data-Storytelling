<!--for the image heavy \ centric sections-->

<script lang="ts">
  import { onMount } from 'svelte';

  // pass these in from declaration
  export let images: string[] = [];
  export let texts: string[][] = [];
  export let alignments: string[] = []; // left or right align each section

  let sections: HTMLElement[] = [];
  let visibleIndex = 0;

  // onMount - when first rendered, track when sections enter and leave view
  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            const index = sections.findIndex((el) => el === entry.target);
            if (index !== -1) visibleIndex = index;
          }
        });
      },
      { threshold: 0.8 }
    );

    sections.forEach((section) => section && observer.observe(section));
    return () => observer.disconnect();
  });
</script>

<div class="scroller">
  <!--loop through each passed entries corresponding img, text, alignment-->
  {#each texts as articleGroup, i}
    <section
      class="scroller-section"
      bind:this={sections[i]}
      style={`background-image: url(${images[i]})`}
    >
      <div
        class="text-overlay {alignments[i] === 'left' ? 'left' : 'right'}"
        class:selected={i === visibleIndex}
      >
        {#each articleGroup as paragraph}
          <p>{@html paragraph}</p>
        {/each}
      </div>
    </section>
  {/each}
</div>

<style>
  .scroller-section {
    position: relative;
    height: 100vh;
    background-size: contain;
    background-position: center center;
    background-repeat: no-repeat;
    background-color: black;
    padding: 7%;
    display: flex;
    align-items: center;
    justify-content: center;
    scroll-snap-align: start;
    transition: background-image 0.5s ease-in-out;
  }

  .text-overlay {
    position: absolute;
    bottom: 2rem;
    background-color: black;
    padding: 1rem 1.5rem;
    max-width: 300px;
    border-radius: 0.75rem;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    font-size: 1.2rem;
    font-family: Arial, Helvetica, sans-serif;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.8s ease, transform 0.8s ease;
    pointer-events: auto;
    z-index: 10;
    text-align: left;
    right: 2rem; 
    color: white;
  }

  .text-overlay.left {
    left: 2rem;
    right: auto;
    text-align: left;
  }

  .text-overlay.right {
    right: 2rem;
    left: auto;
    text-align: left;
  }

  .text-overlay.selected {
    opacity: 1;
    transform: translateY(0);
  }
</style>