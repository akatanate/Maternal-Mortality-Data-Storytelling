<script>
    let { title, subtitle , sub2, sub3} = $props();
</script>


<div class="title-card">
    <div class="content nike-text">
        <h1>{title}</h1>
        <p>{subtitle}</p>
        <p>{sub2}</p>
        <p>{sub3}</p>
    </div>
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

    .title-card {
        /*background-color: #007052;*/
        background-image: url('/scrollytelling-starter/tori3.jpg');
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        height: 100vh;
        width: 100%;
        height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        padding: 2rem;
        box-sizing: border-box;
        /*font-family: "Inter", sans-serif;*/
    }

    .content {
        /*max-width: 700px;
        background-color: #034c36;
        padding: 2rem;
        border: 6px solid #e3ff00;
        border-radius: 2rem;
        box-shadow: 16px 16px #188f70;*/
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

    @media (max-width: 600px) {
        h1 {
            font-size: 2.2rem;
        }

        p {
            font-size: 1.1rem;
        }
    }
</style>
