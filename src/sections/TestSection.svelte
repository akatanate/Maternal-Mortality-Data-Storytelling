<script>
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";
</script>

<div class = "nike-text">
<Scroller layout="left">
    {#snippet sticky()}
      <h1 class = "nike-text">Sticky Content</h1>
      <p class = "nike-text">This stays in place while scrolling.</p>
    {/snippet}

    {#snippet scrolly()}
      <ArticleText>
        <p>This is the first scrollable section of text.</p>
      </ArticleText>
      <ArticleText>
        <p>This is the second scrollable section of text.</p>
      </ArticleText>
      <ArticleText>
        <p>This is the third scrollable section of text.</p>
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
    }
</style>