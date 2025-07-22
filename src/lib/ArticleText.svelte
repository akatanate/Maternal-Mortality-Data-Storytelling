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
        background-color: navy;
        color: whitesmoke;
        border: solid #8427c9 3px;
        border-radius: 20px;
        padding: 20px;
        box-shadow: 16px 16px #8aa6df;
        
    }
</style>
