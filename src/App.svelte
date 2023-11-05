<script>
	import SearchBar from './components/SearchBar.svelte';
	import VideoList from './components/VideoList.svelte';
	import VideoDetail from './components/VideoDetails.svelte';
  
	let videos = [];
	let selectedVideo = null;
	let nextPageToken = null;
	let currentSearchTerm = '';
  
	const searchYouTube = async (searchTerm, pageToken = '') => {
    try {
      const response = await fetch(`https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=5&q=${encodeURIComponent(searchTerm)}&pageToken=${pageToken}&key=${process.env.API_KEY}`);
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      const data = await response.json();
      nextPageToken = data.nextPageToken || '';
      videos = pageToken ? [...videos, ...data.items] : data.items;
      if (!selectedVideo || !pageToken) selectedVideo = videos[0];
    } catch (error) {
      console.error('Error during YouTube API request:', error);
    }
  };
  
	const loadMore = () => {
	  if (nextPageToken) {
		searchYouTube(currentSearchTerm, nextPageToken);
	  }
	};
  
	const selectVideo = (video) => {
	  selectedVideo = video;
	};
  </script>
  
  <div class="app">
	<div class="Nav">
		<div class="logoName">StreamTube</div>
	</div>
	<div class="parent">
	<div class="video-display">
	  <VideoDetail {selectedVideo} {loadMore} />
	</div>
	<div class="video-list">
	  <VideoList {videos} {selectVideo} />
	</div>
</div>
	<div class="search-bar">
	  <SearchBar on:click={(event) => searchYouTube(event.detail.searchTerm)} />
	</div>
  </div>
  
  <style>
	.parent{
		display: flex;
	}
	.app {
	height: 100%;
	}
	.Nav{
		display: flex;
		justify-content: space-between;
		height: 100px;
	}
	.logoName{
		font-size: xx-large;
		margin-left: 25px;
		font-weight: bolder;
	}
	.changeTheme{
		font-size: xx-large;
		margin-right: 25px;
	}
	.video-display, .video-list {
	  flex: 1;
	}
	.video-list {
	  overflow-y: scroll;
	  max-height: 500px;
	  padding: 8px;
	  border-bottom: 1px solid #ccc;
	}
	.search-bar {
	  padding: 8px;
	  background: #fff;
	  box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.1);
	}
  </style>
  