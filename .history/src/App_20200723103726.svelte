<div class="body">
	<input type="file" id="file" multiple on:change={handleChangeFile}>
	<audio id="audio_id" bind:this={audioDom} poster="http://img.lanrentuku.com/img/allimg/1810/15409966139768.jpg" controls autoplay on:ended={nextAudio} src={src} >Your browser can't support HTML5 Audio</audio>
	<h2 id="name">{name}</h2>
	<button id="next" on:click={nextAudio}>next</button>
</div>
<script>
			let audioDom = null;
			let name = "";
			let src = null;
      const audioList = [];
			let audioIdx = 0;
			function handleChangeFile () {
				const files = file.files;
        const len = files.length;
        let i = 0;
        while (i < len) {
          const obj = {
            title: files[i].name.replace(/\..*$/, ''),
            url: URL.createObjectURL(files[i])
          };
          audioList.push(obj);
          i++;
        };
        nextAudio();
        mediasession();
			}
      /**
       * pre 有值代表播放上一首
      */
      function nextAudio(pre) {
        if (audioIdx >= audioList.length) {
          audioIdx = 0;
        }
        if (audioIdx <= 0) {
          audioIdx = audioList.length - 1;
        }
        const { url, title } = audioList[audioIdx];
        src = url;
        name = title;
        if ('mediaSession' in navigator) {
          navigator.mediaSession.metadata = new MediaMetadata({
            title: title,
            artist: '未知',
            artwork: [
              {src: 'http://img.lanrentuku.com/img/allimg/1810/15409966139768.jpg', sizes: '192x192'}
            ]
          });
        }
        if (pre) {
          audioIdx += -1;
        } else {
          audioIdx++;
        }
      };
      function mediasession() {
        if ('mediaSession' in navigator) {
          const ms = navigator.mediaSession;
          ms.setActionHandler('play', function() {
            audioDom.play();
          });
          ms.setActionHandler('nexttrack', function() {
            nextAudio();
          });
          ms.setActionHandler('previoustrack', function() {
            nextAudio('pre');
          });
          ms.setActionHandler('pause', function() {
            audioDom.pause();
          });
        }
      }
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
		text-align: center
  }
</style>

