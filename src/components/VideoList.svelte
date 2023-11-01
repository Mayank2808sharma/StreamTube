<script>
    export let videos = [];
    export let selectVideo;
  </script>
  
  <ul>
    {#each videos as { id, snippet } (id.videoId)}
      <li on:click={() => selectVideo({ id, snippet })}>
        <img src={snippet.thumbnails.default.url} alt={snippet.title} />
        <h3>{snippet.title}</h3>
      </li>
    {/each}
  </ul>
  
  <style>
    ul {
      list-style-type: none;
      padding: 0;
    }
    li {
      cursor: pointer;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
    }
    img {
      margin-right: 10px;
    }
    h3 {
      font-size: 14px;
      margin: 0;
    }
  </style>
  