<script lang="ts">
  import { onMount } from "svelte";
  let color: string = "#000000";
  let bgcolor: string = "#ffffff";
  let ctx: CanvasRenderingContext2D | null | undefined;
  let canvas: HTMLCanvasElement | null;
  let size: number = 500;
  function drawCanvas() {
    ctx!.font = `${canvas!.height / 2}px Noto Emoji`;
    ctx!.fillStyle = color;
    ctx!.textAlign = "center";
    ctx!.textBaseline = "middle";
    ctx!.fillText("🚀", canvas!.width / 2, canvas!.height / 2);
  }
  function changeCanvas() {
    canvas = document?.querySelector("#ctx");
    canvas!.width = 500;
    canvas!.height = 500;
    ctx = canvas?.getContext("2d");
    ctx!.fillStyle = bgcolor;
    ctx!.fillRect(0, 0, canvas!.width, canvas!.height);
    drawCanvas();
  }
  function saveCanvas() {
    canvas = document?.querySelector("#ctx");
    canvas!.width = 500;
    canvas!.height = 500;
    ctx = canvas?.getContext("2d");
    ctx!.fillStyle = bgcolor;
    ctx!.fillRect(0, 0, canvas!.width, canvas!.height);
    drawCanvas();
    let downloader = document.createElement("a");
    downloader.download = `image${size}.png`;
    downloader.href = canvas!.toDataURL();
    downloader.click();
    changeCanvas();
  }
  onMount(() => {
    changeCanvas();
  });
</script>

<main>
  <div class="screen">
    <div class="options">
      <label for="colordes">아이콘 색</label>
      <input type="color" bind:value={color} on:change={drawCanvas} />
      <label for="colordes">배경 색</label>
      <input type="color" bind:value={bgcolor} on:change={changeCanvas} />
      <label for="sizedes">아이콘 이미지 크기</label>
      <input class="size-input" type="number" bind:value={size} />
      <button on:click={saveCanvas}>아이콘 저장</button>
    </div>
    <canvas id="ctx" width="500" height="500" />
  </div>
</main>

<style>
  .options {
    font-size: 1.25rem;
    display: grid;
    align-items: center;
    grid-template-rows: repeat(4, 1fr);
    grid-template-columns: repeat(2, 1fr);
  }
  .screen {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: 1fr;
  }
  .size-input {
    font-size: 1.25rem;
    width: fit-content;
  }
  button {
    font-size: 2rem;
  }
</style>
