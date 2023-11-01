<script>
    export let selectedVideo = null;
    export let loadMore;
    const shareVideo = () => {
    if (selectedVideo) {
        console.log(selectedVideo)
      const videoUrl = `https://www.youtube.com/watch?v=${selectedVideo.id.videoId}`;
      navigator.clipboard.writeText(videoUrl)
        .then(() => {
          alert('Video URL copied to clipboard!');
        })
        .catch(err => {
          console.error('Could not copy text: ', err);
        });
    }
  };
  </script>
  
  {#if selectedVideo}
    <div class="video-wrapper">
      <h2>{selectedVideo.snippet.title}</h2>
      <iframe
        src={`https://www.youtube.com/embed/${selectedVideo.id.videoId}`}
        frameborder="0"
        allowfullscreen
      />
      <p>{selectedVideo.snippet.description}</p>
    </div>
    <div class="actions">
    <button class="share" on:click={shareVideo}>Share</button>
      {#if loadMore}
        <button on:click={loadMore} class="load-more">Load More</button>
      {/if}
    </div>
  {:else}
    <p>Please select a video</p>
  {/if}
  
  <style>
    .video-wrapper {
      border-bottom: 1px solid #ccc;
      padding-bottom: 16px;
      margin-bottom: 16px;
    }
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
      color: #333;
    }
    .actions {
      display: flex;
      justify-content: space-between;
    }
    button {
      padding: 8px 16px;
      font-size: 14px;
      cursor: pointer;
      border: none;
      border-radius: 4px;
      background-color: #f9f9f9;
      color: #333;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .load-more {
      background-color: #4CAF50;
      color: white;
    }
  </style>
  