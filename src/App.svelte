<script>
import Header from "./components/Header.svelte";
import Footer from "./components/Footer.svelte";
import PollList from "./components/PollList.svelte";
import AddPollForm from "./components/AddPollForm.svelte";
import Tabs from "./shared/Tabs.svelte";

// tabs
let items = ["Current Polls", "Add New Poll"];
let activeItem = "Current Polls";

const tabChange = (e) => {
	activeItem = e.detail;
}

let polls = [
	{
		id: 1,
		question: "Python or JavaScript?",
		answerA:"Python",
		answerB: "JavaScript",
    votesA:9,
		votesB:15,
	}
]

const handleAdd = (e) => {
	let poll = e.detail;
	polls = [poll, ...polls];
	activeItem = "Current Polls";
}
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange}/>
	{#if activeItem === "Current Polls"}
		<PollList {polls}/>
	{:else if activeItem === "Add New Poll"}
		<AddPollForm on:add={handleAdd} />
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>