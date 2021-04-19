<script lang="ts">
  import { trackData } from './data'
  const nameList = trackData.map((v) => v.abbr)
  let selected = 1
  $: imagePath = `assets/atbl_${('0' + selected).slice(-2)}.png`
	$: cor = {x: 0, y: 0}
  const toggleImage = () => {}
	const clickImage = (e: MouseEvent) => {
		cor.x = e.offsetX
		cor.y = e.offsetY
	}
</script>

<main>
  <select bind:value={selected}>
    {#each trackData as track}
      <option value={track.id}>
        {track.name_en}
      </option>
    {/each}
  </select>
  <div class="canvas-wrapper">
    <div class="image" style="background-image: url('{imagePath}');"  on:click={clickImage} />
  </div>
  <div class="button-wrapper">
    <button class="toggle" on:click={toggleImage}>Toggle Image</button>
    <button id="clear">Clear Canvas</button>
  </div>
  <div class="text">{cor.x},{cor.y}</div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 700px;
    margin: 0 auto;
  }

  .image {
    width: 350px;
    height: 350px;
    margin: 0 auto;
    background-size: 350px;
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
