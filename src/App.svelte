<script>
	import CreatePoll from "./components/CreatePoll.svelte";
	import Footer from "./components/Footer.svelte";
	import Header from "./components/Header.svelte";
	import Tabs from "./shared/tabs.svelte";
	import PollList from './components/PollList.svelte';

	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = 'Current Polls';
	const tabChange = (e) => activeItem = e.detail; 

	const handleAdd = (e) =>  {
		activeItem = 'Current Polls';
	}	 

</script>

<Header />
<main>
<Tabs {items} {activeItem} on:tabChange={tabChange}/>
{#if activeItem === 'Current Polls'}
	<!-- svelte-ignore missing-declaration -->
	<PollList  />  
{:else if activeItem === 'Add New Poll'}
	<!-- svelte-ignore missing-declaration -->
	<CreatePoll on:add={handleAdd} />
	{/if}
</main>
<Footer />
<style>
	main {
		width: 100%;
		max-width: 960px;
		margin: 40px auto;
	}
</style>