<script>
	import SearchBar from './components/SearchBar.svelte';
	import VideoList from './components/VideoList.svelte';
	import VideoDetail from './components/VideoDetails.svelte';
	
	let videos = [];
	let selectedVideo = null;
	
	const searchYouTube = async (searchTerm) => {
	  const response = await fetch(`https://www.googleapis.com/youtube/v3/search?part=snippet&maxResults=5&q=${encodeURIComponent(searchTerm)}&key=${process.env.API_KEY}`);
	  const data = await response.json();
	  console.log(data);
	  videos = data.items;
	  selectedVideo = videos[0];
	};
  
	const selectVideo = (video) => {
	  selectedVideo = video;
	};
  </script>
  
  <SearchBar on:click={(event) => searchYouTube(event.detail.searchTerm)} />
  <VideoDetail {selectedVideo} />
  <VideoList {videos} {selectVideo} />
  