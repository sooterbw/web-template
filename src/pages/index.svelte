<script>
    import Block from '../components/Block.svelte'

    let data = {
        "text": "Welcome!",
        "class": "heading"
        }
</script>

<div class="temp-index">
    <Block contentType={data.class} content={data.text} />
</div>

<style>
    .temp-index {
        display: flex;
        height: 100vh;
        width: 100vw;
        color: aliceblue;
        justify-content: center;
        align-items: center;
        background-image: url("https://pressstart.vip/images/uploads/assets/cityskyline.png");
    }
</style>