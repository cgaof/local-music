<script>
	export let name;
</script>

<style>
	.body {
    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: repeat(1, 40px);
    justify-items: center;
    align-items: center;
    overflow: hidden;
    word-wrap: break-word;
  }
  h2 {
    width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
</style>

<div class="body">
	<input type="file" id="file" multiple>
	<audio id="audio_id" poster="http://img.lanrentuku.com/img/allimg/1810/15409966139768.jpg" controls autoplay>Your browser can't support HTML5 Audio</audio>
	<h2 id="name"></h2>
	<button id="next">next</button>
</div>