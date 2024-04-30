<script>
	//Binding Text
	const teamName = 'Vue Team'

	//Binding HTML
	const channel = '<b>Training Session</b>'
  const hack = `<a href="#" onclick="alert('You need to attend session on-time!')">get to know about svelte!<a/>`

	//Binding to Attribute
	const headingId = 'heading'
	const id = 'heading'
  const disabled = false //boolean attribute

	// Class Binding
	const status = 'danger'
  const promoted = true

	// Conditional Rendering
	const num = 'Hi'
	// const num = 0

	//List Rendering 
	const names = ['Bruce', 'Clark', 'Diana']
  const fullNames = [
    { first: 'Bruce', last: 'Wayne' },
    { first: 'Clark', last: 'Kent' },
    { first: 'Princess', last: 'Diana' }
  ]

	//Event Handling 
	let count = 0
  function handleClick(event, stepSize) {
    console.log(event)
    count += stepSize
  }
	$: doubled = count * 2

	// Form controls
	const formValues = {
    name: '',
    profileSummary: '',
    country: '',
    jobLocation: [],
    remoteWork: false,
    skillSet: [],
    yearsOfExperience: ''
  }

	function submitForm() {
		// event.preventDefault() //to avoid whole page refresh on submission
    console.log('form values', formValues)
  }

	// Reactivity - Reactive Declarations
	let firstName = 'Mansi'
  let lastName = 'Nakrani'
  $: fullName = `${firstName} ${lastName}`
 
	// Reactivity - Reactive Statements
	// $: console.log(`Fullname is ${firstName} ${lastName}`)
	$: {
    const greet = `Fullname is ${firstName} ${lastName}`
    console.log(greet)
  }

  let items = [
    {
      id: 1,
      title: 'TV',
      price: 100
    },
    {
      id: 2,
      title: 'Phone',
      price: 200
    },
    {
      id: 3,
      title: 'Laptop',
      price: 300
    }
  ]
  $: total = items.reduce((total, curr) => (total = total + curr.price), 0)

	// Reactivity - Reactive Statements
	let volume = 0
  $: if (volume < 0) {
    alert(`Can't go lower`)
    volume = 0
  } else if (volume > 20) {
    alert(`Can't go higher`)
    volume = 20
  }

</script>

<main>
	<!-- Binding Text -->
	<h1>Hello {teamName}!</h1>
	<hr/>
	<!-- Binding HTML: input value into read only mode, use prefix '@html', don't use for third-party API -->
	<div>{@html channel}</div>
  <div>{@html hack}</div>
	<hr/>

	<!-- Binding/Dynamic Attribute -->
	<h2 id={headingId}>This is a heading</h2>
	<h2 {id}>This is a heading using shorthand</h2> <!--shorthand if attribute name = value i.e, id={id}  -->
  <button {disabled}>Bind</button>
	<hr/>

	<!-- Binding class -->
	<h2 class="underline">Underlined Text</h2>
  <h2 class={status}>Status</h2>
  <h2 class={promoted ? 'promoted' : ''}>Movie Title</h2> <!--Conditional binding--->
  <h2 class:promoted>Movie Title</h2>
  <!-- <h2 class:promoted={promoted}>Movie Title</h2> -->
	<hr/>

	<!-- Conditional Rendering -->
	{#if num === 0}
	<h2>The number is zero</h2>
	{:else if num < 0}
		<h2>The number is negative</h2>
	{:else if num > 0}
		<h2>The number is positive</h2>
	{:else}
		<h2>Not a number</h2>
	{/if}
	<hr/>

	<!--List Rendering -->
  {#each names as name, index (name)}
    <h2>{index + 1} {name}</h2>
  {/each}

  {#each fullNames as name, index (name.first)}
    <h2>{index + 1} {name.first} {name.last}</h2>
  {/each}
	<hr/>

	<!-- Event Handling -->
	<button on:click={e => handleClick(e, 5)}> Count {count} </button>
  <button on:click={e => handleClick(e, 10)}> Count {count} </button>
	<p>Doubled : {doubled}</p>
	<hr/>

	<!-- Form controls -->
	<div>
    <pre>
      { JSON.stringify(formValues, null, 2) }
    </pre>
  </div>

  <form on:submit|preventDefault={submitForm}>
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={formValues.name} />
    </div>
    <div>
      <label for="profile">Profile Summary</label>
      <textarea id="profile" bind:value={formValues.profileSummary} />
    </div>
    <div>
      <label for="country">Country</label>
      <select id="country" bind:value={formValues.country}>
        <option value="">Select a country</option>
        <option value="india">India</option>
        <option value="vietnam">Vietnam</option>
        <option value="singapore">Singapore</option>
      </select>
    </div>
    <div>
      <label for="job-location">Job location</label>
      <select id="job-location" bind:value={formValues.jobLocation} multiple>
        <option value="india">India</option>
        <option value="vietnam">Vietnam</option>
        <option value="singapore">Singapore</option>
      </select>
    </div>
    <div>
      <input
        type="checkbox"
        id="remoteWork"
        bind:checked={formValues.remoteWork}
      />
      <label for="remoteWork">Open to remote work?</label>
    </div>
    <div>
      <label>Skill set</label>
      <input
        type="checkbox"
        id="html"
        value="html"
        bind:group={formValues.skillSet}
      />
      <label for="html">HTML</label>
      <input
        type="checkbox"
        id="css"
        value="css"
        bind:group={formValues.skillSet}
      />
      <label for="css">CSS</label>
      <input
        type="checkbox"
        id="javascript"
        value="javascript"
        bind:group={formValues.skillSet}
      />
      <label for="javascript">JavaScript</label>
    </div>
    <div>
      <label>Years of Experience</label>
      <input
        type="radio"
        id="0-2"
        value="0-2"
        bind:group={formValues.yearsOfExperience}
      />
      <label for="0-2">0-2</label>
      <input
        type="radio"
        id="3-5"
        value="3-5"
        bind:group={formValues.yearsOfExperience}
      />
      <label for="3-5">3-5</label>
      <input
        type="radio"
        id="6-10"
        value="6-10"
        bind:group={formValues.yearsOfExperience}
      />
      <label for="6-10">6-10</label>
      <input
        type="radio"
        id="10+"
        value="10+"
        bind:group={formValues.yearsOfExperience}
      />
      <label for="10+">10+</label>
    </div>
		<div>
      <button>Submit</button>
    </div>
  </form>
	<hr/>

	<!-- Reactivity - Reactive Declarations -->
	<h2>{firstName} {lastName}</h2>
  <h2>Reactive Fullname - {fullName}</h2>
  <button
    on:click={() => {
      firstName = 'M'
      lastName = 'N'
    }}>Change Name</button
  >

  <h2>Reactive Total - {total}</h2>
  <button
    on:click={() =>
      (items = [...items, { id: 4, title: 'Keyboard', price: 50 }])}
  >
    Add item
  </button>
	<!-- Reactivity - Reactive Statements -->
  <div>
    <h2>Current Volume {volume}</h2>
    <button on:click={() => (volume += 2)}>Increase Volume</button>
    <button on:click={() => (volume -= 2)}>Decrease Volume</button>
  </div>
	<hr/>


	<hr/>


	<hr/>


	<hr/>

</main>

<style>
	main {
		/* text-align: center; */
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

	.underline {
    text-decoration: underline;
  }
  .danger {
    color: red;
  }
  .success {
    color: olivedrab;
  }
  .promoted {
    font-style: italic;
  }

	input + label {
    display: inline-flex;
  }
</style>