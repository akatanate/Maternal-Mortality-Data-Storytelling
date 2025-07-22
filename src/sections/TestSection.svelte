<script>
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";
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

        .duck-img {
        width: 90%;
        margin: 0px auto;
    }
</style>