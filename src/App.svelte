<script lang="ts">
</script>

<main>
  <div class="canvas-wrapper">
    <div class="image" />
    <div class="image2" />
    <canvas class="canvas" />
  </div>
  <div class="button-wrapper">
    <button id="show">Show Answer</button>
    <button id="clear">Clear Canvas</button>
  </div>
  <div class="text" />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 700px;
    margin: 0 auto;
  }

  .image,
  .image2 {
    width: 350px;
    height: 350px;
    margin-right: 10px;
    background-size: 350px;
  }

  .image {
    background-image: url('https://i.imgur.com/DQeyuzY.png');
  }
  .image2 {
    background-image: url('https://i.imgur.com/6d22VN2.png');
    opacity: 0;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
