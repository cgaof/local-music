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

<h1>Hello {name}!</h1>
<h2>h2</h2>