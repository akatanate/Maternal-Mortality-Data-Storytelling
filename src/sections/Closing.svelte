<script>
  import Scroller from "../lib/Scroller.svelte";
  import PaperText from "../lib/PaperText.svelte";
</script>

<div class="page-container">
  <img class="background-image" src="/Maternal-Mortality-Data-Storytelling/closing.png" alt="Background" />

  <div class="content">
    <Scroller>
      {#snippet sticky()}
        <!-- leave this or not? -->
      {/snippet}

      {#snippet scrolly()}
        <PaperText>
          <p>The higher likelihood of pregnancy complications among Black women is not a coincidence—it’s the result of deeply rooted healthcare inequities, limited financial assets, and disproportionate debt. These systemic factors create compounding harm.</p>
        </PaperText>

        <PaperText>
          <p>Even when Black women do access care, racial bias within the medical system—such as the dangerous myth that Black women have a higher pain tolerance—can lead to inadequate or delayed treatment.</p>
        </PaperText>

        <PaperText>
          Black women represent this country on the global stage—in sports, leadership, and beyond.. They lead the finish line. It’s time for something more than “JUST DO IT.”
        </PaperText>
      {/snippet}
    </Scroller>
  </div>
</div>

<style>
  .page-container {
    position: relative;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .background-image {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    z-index: -1;
    pointer-events: none;
  }

  .content {
    position: relative;
    z-index: 1;
    max-width: 1500px;


    font-family: 'NikeFont', sans-serif;
    font-size: 1.8rem;
    color: #222;
    border-radius: 12px;
  }
</style>
