<script>
  export let selectedVideo = null;
</script>

{#if selectedVideo}
<h2>{selectedVideo.snippet.title}</h2>
<iframe
src={`https://www.youtube.com/embed/${selectedVideo.id.videoId}`}
frameborder="0"
allowfullscreen
/>
  <p>{selectedVideo.snippet.description}</p>
{:else}
  <p>Please select a video</p>
{/if}

<style>
  iframe {
    width: 100%;
    height: 300px;
    margin-bottom: 10px;
  }
  h2 {
    font-size: 20px;
    margin-bottom: 10px;
  }
  p {
    font-size: 14px;
  }
</style>
