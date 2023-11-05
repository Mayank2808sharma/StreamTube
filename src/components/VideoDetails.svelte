<script>
  export let selectedVideo = null;
  export let loadMore;
  const shareVideo = () => {
    if (selectedVideo) {
      console.log(selectedVideo);
      const videoUrl = `https://www.youtube.com/watch?v=${selectedVideo.id.videoId}`;
      navigator.clipboard
        .writeText(videoUrl)
        .then(() => {
          alert("Video URL copied to clipboard!");
        })
        .catch((err) => {
          console.error("Could not copy text: ", err);
        });
    }
  };
</script>

{#if selectedVideo}
  <div class="video-wrapper">
    <h2 class="vidoetitle">{selectedVideo.snippet.title}</h2>
    <div class="aspect-ratio">
      <iframe
        src={`https://www.youtube.com/embed/${selectedVideo.id.videoId}`}
        frameborder="0"
        allowfullscreen
      />
    </div>
    <p class="vidoedesc">{selectedVideo.snippet.description}</p>
    <div class="actions">
      <button class="share" on:click={shareVideo}>Share</button>
      {#if loadMore}
        <button on:click={loadMore} class="load-more">Load More</button>
      {/if}
    </div>
  </div>
{:else}
  <p>Please select a video</p>
{/if}

<style>
 .video-wrapper {
  max-width: 100%;
  margin: auto;
  border-bottom: 1px solid #ccc;
  padding-bottom: 16px;
  margin-bottom: 16px;
  background: #fff;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.1); /* subtle shadow around the video wrapper */
}

/* Maintain aspect ratio for the iframe video */
.aspect-ratio {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
  height: 0;
}

iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%; /* Use absolute positioning and 100% width and height for responsiveness */
  border: 0;
}

.vidoetitle {
  color: #030303;
  font-family: 'Roboto', Arial, sans-serif;
  font-size: 18px;
  font-weight: 500;
  margin-bottom: 0.6em;
}

.vidoedesc {
  font-size: 14px;
  color: #484747;
  font-family: 'Roboto', Arial, sans-serif;
  line-height: 1.6em;
}

.actions {
  display: flex;
  justify-content: flex-start;
  margin-top: 12px;
}

button {
  padding: 10px 16px;
  font-size: 14px;
  cursor: pointer;
  border: 1px solid #d3d3d3;
  border-radius: 2px;
  background-color: #f8f8f8;
  color: #030303;
  text-transform: uppercase;
  font-family: 'Roboto', Arial, sans-serif;
  margin-right: 8px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: rgb(115, 3, 3); /* Red button hover effect */
}

.load-more {
  background-color: #cc181e; /* YouTube red color */
  color: white;
  border-color: #cc181e;
}

button:focus {
  outline: none;
  box-shadow: 0 0 2px #7c0000; /* Red focus shadow */
}

.share:hover {
  background-color: rgb(162, 159, 159);
}

</style>
