<script>
    let { children } = $props();
</script>

<div class="article-text">
    <p>
        {@render children()}
    </p>
</div>

<style>
    .article-text {
        margin: 30vh auto;
        width: 50%;
        border: solid #6b97ef .5px;
        box-shadow: 4px 4px #8aa6df;
        background-image: url('/scrollytelling-starter/paper.png');
        background-size: cover;
    }

    p {
        font-family: 'NikeFont', sans-serif;
        margin: 5%;
    }
</style>
