<script lang="ts">
  import { xlink_attr } from 'svelte/internal'
  import { trackData } from './data'
  let selected = 1
  $: imagePath = `assets/atbl_${('0' + selected).slice(-2)}.png`
  $: cor = { x: 0, y: 0 }
  let corList = []
  $: currentColor = colorList[corList.length % 3]
  const colorList = ['#f00', '#0f0', '#00f']
  const toggleImage = () => {}
  const clickImage = (e: MouseEvent) => {
    e.preventDefault()
    corList = [...corList, { x: e.offsetX, y: e.offsetY, color: currentColor }]
  }
  const onMouseImage = (e: TouchEvent) => {
    e.preventDefault()
    cor.x = e.offsetX
    cor.y = e.offsetY
  }

  const clearCanvas = () => {
    corList = []
    corList = corList
  }
</script>

<main>
  <!-- svelte-ignore a11y-no-onchange -->
  <select bind:value={selected} on:change={clearCanvas}>
    {#each trackData as track}
      <option value={track.id}>
        {track.name_en}
      </option>
    {/each}
  </select>
  <div class="canvas-wrapper">
    <div class="image" style="background-image: url('{imagePath}');" />
    {#each corList as cord}
      <div
        class="circle"
        style="left: {cord.x - 16}px; top: {cord.y -
          16}px; background-color: {cord.color};"
      />
    {/each}
    <div
      class="circle"
      style="opacity: 0.5; left: {cor.x - 16}px; top: {cor.y -
        16}px; background-color: {currentColor};"
    />
    <div
      class="image2"
      style="opacity:0;"
      on:click={clickImage}
      on:touchmove={onMouseImage}
    />
  </div>
  <div class="button-wrapper">
    <button class="toggle" on:click={toggleImage}>Toggle Image</button>
    <button id="clear" on:click={clearCanvas}>Clear Canvas</button>
  </div>
  <div class="text">{cor.x},{cor.y}</div>
  <div class="text">{corList.map((e) => `${e.x}, ${e.y}`)}</div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 700px;
    margin: 0 auto;
  }

  .canvas-wrapper {
    position: relative;
    width: 350px;
    height: 350px;
    margin: 16px auto;
    border: 2px solid #ccc;
  }
  .circle {
    position: absolute;
    width: 32px;
    height: 32px;
    border: black solid 2px 2px;
    background-color: #f00;
    display: inline-block;
    border-radius: 50%;
  }
  .image {
    position: absolute;
    width: 350px;
    height: 350px;
    top: 0;
    left: 0;
    background-size: 350px;
  }
  .image2 {
    position: absolute;
    width: 350px;
    height: 350px;
    top: 0;
    left: 0;
  }
  .image {
    background-image: url('https://i.imgur.com/DQeyuzY.png');
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
