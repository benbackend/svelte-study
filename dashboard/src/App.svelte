<script>
	import Modal from './Modal.svelte';
	import AddPersonForm from './AddPersonForm.svelte';
	let showModal = false;

	const toggleModal = () => {
		showModal = !showModal;
	};

	let people = [
		{name:'yoshi', beltColor:'black' , age:25, id: 1},
		{name:'mario', beltColor:'orange' , age:45, id: 2},
		{name:'luigi', beltColor:'brown' , age:35, id: 3}
	];

	const handleClick = (id) => {
		people = people.filter((person) => person.id != id);	
	}

	const addPerson = (e) => {
		const person = e.detail;
		// ... = for all person in people
		people = [person, ...people];
		showModal = false;
	}

</script>

<Modal showModal={showModal} on:click={toggleModal} >
	<AddPersonForm on:addPerson={addPerson}/>
</Modal>

<main>
	<button on:click={toggleModal}> Show Modal </button>
	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColor === 'black'}
				<p><strong> Master Ninja </strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColor} belt.</p>
			<button on:click={ () => handleClick(person.id)}> delete </button>
		</div>
	{:else}
		<p>no people to show LOL</p>
	{/each}
</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>