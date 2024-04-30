<script>
	// export let name;
	import Greet from "./components/Greet.svelte";
	//context API
	import { setContext } from 'svelte'
	// Components events
	import Popup from "./components/Popup.svelte";
	// Event Forwarding
	import Outer from "./components/Outer.svelte";
	import Button from "./components/Button.svelte";
	// Slots
	import Card from "./components/Card.svelte";
	// Slot props
	import NameList from "./components/NameList.svelte";
	// Component Styles
	import ChildStyles from "./components/ChildStyles.svelte";
	// HTTP Requests
	import PostList from "./components/PostList.svelte";
	// this binding
	import AutoFocus from "./components/AutoFocus.svelte";
	// Dynamic Components
	import TabA from "./components/TabA.svelte";
	import TabB from "./components/TabB.svelte";
	import TabC from "./components/TabC.svelte";
	// Module context
	import Counter, { getTotalCount } from "./components/Counter.svelte";


  const name = 'Mansi'
  const team = 'Vue'
  const obj = {
    name: 'Mansi N',
    teamName: 'React'
  }

	//context API
	import ComponentA from "./components/ComponentA.svelte";
	const userName = "MN"
	setContext('username-context', userName)


	// Components events
  let showPopup = false
  function closePopup(event) {
    showPopup = false
    console.log(event.detail)
  }

	// Event Forwarding
	function handleGreet(event) {
    alert(event.detail)
  }

	// Dynamic Components
	let activeTab = TabA

</script>

<main>
	<!-- <h1>Hello {name}!</h1>
	<Greet/> -->
	<Greet name="Akash" teamName="Vue" />
  <Greet name="Dev" teamName="Python" />
  <Greet name="Vidhi" teamName="React" />
  <Greet {name} teamName={team} />
  <Greet {...obj} />
	<hr/>

	<!-- context API -->
	<h2>App component username - {userName}</h2>
  <ComponentA />
	<hr/>

	<!-- Component Events -->
	<button on:click={() => (showPopup = true)}>Show Popup</button>
  {#if showPopup}
    <Popup on:close={closePopup} />
  {/if}
	<hr/>

	<!-- Event Forwarding -->
	<Outer on:greet={handleGreet} />
  <Button on:click={() => alert('Clicked')}>Click</Button>
	<hr/>

	<!-- Slots -->
  <!-- <Card />
	<Card>Card Content</Card>
  <Card><h2>Card Content</h2></Card>
  <Card><img src="https://picsum.photos/200" alt /></Card>
	<hr/> -->

	<!-- Named slots , ex: layout-->
	<Card>
    <div slot="header">
      <h3>Header</h3>
    </div>
    <div slot="content">
      <img src="https://picsum.photos/200" alt />
    </div>
    <div slot="footer">
      <button>View Details</button>
    </div>
  </Card>

  <Card>
    <div slot="header">
      <h3>Header</h3>
    </div>
    <div slot="content">
      <img src="https://picsum.photos/200" alt />
    </div>
  </Card>
	<hr/>

	<!-- Slot props -->
	<NameList>
    <h3 slot="hero" let:firstName let:lastName>{firstName} {lastName}</h3>
  </NameList>

	<NameList>
    <h3 slot="hero" let:firstName let:lastName>{lastName} {firstName}</h3>
  </NameList>

  <NameList>
    <h3 slot="hero" let:lastName>{lastName}</h3>
  </NameList>
	<hr/>

	<!-- Component Styles , style added in <style> for h4 -->
	<!-- NOTE : In svelte  by default components styles are scoped to particular component-->
	<h4>App Component Text</h4>
  <ChildStyles />
  <h3>App component global style</h3>
	<hr/>

	<!-- HTTP Requests -->
  <!-- <PostList />
	<hr/> -->

	<!-- this binding -->
	<AutoFocus />
	<hr/>

	<!-- Dynamic Components -->
	<div>
    <button on:click={() => (activeTab = TabA)}>Tab A</button>
    <button on:click={() => (activeTab = TabB)}>Tab B</button>
    <button on:click={() => (activeTab = TabC)}>Tab C</button>
  </div>
  <!-- {#if activeTab === 'TabA'}
    <TabA />
  {/if}
  {#if activeTab === 'TabB'}
    <TabB />
  {/if}
  {#if activeTab === 'TabC'}
    <TabC />
  {/if} -->

  <svelte:component this={activeTab} /><!-- Special element -->
	<hr/>

	<!-- Module context :  share code across component instance , for data synchronization -->
  <button on:click={() => alert(getTotalCount())}>Alert total count</button>
  <Counter />
  <Counter />
  <Counter />

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
/*Component Styles */
  h4 {
    color: orange;
  }
</style>