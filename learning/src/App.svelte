<script lang="ts">
import Modal from './Modal.svelte'
import AddPersonForm from './AddPersonForm.svelte'

let showModal = false;

	let people = [
		{ name: 'Leif', beltColor: 'black', age: 19, id: 1 },
		{ name: 'Frank', beltColor: 'brown', age: 53, id: 2 },
		{ name: 'Frode', beltColor: 'blue', age: 17, id: 3}
	]

	const handleClick = (id: number) => {
		people = people.filter((person) => person.id !== id);
	}

	const toggleModal = () => {
		showModal = !showModal;
	}

	const addPerson = (e) => {
		const person = e.detail;
		people = [person, ...people];
		showModal = false;
	}
</script>

<Modal {showModal} on:click={toggleModal}>
	<AddPersonForm on:addPerson={addPerson} />
</Modal>
<main>
	<button on:click={toggleModal}>Open Modal</button>
	{#each people as person (person.id)}
		<div>
			<h4>{person.name}</h4>
			{#if person.beltColor === "black"}
				<p><strong>Big Boy</strong></p>
			{/if}
			<p>{person.age} years old, {person.beltColor} belt.</p>
			<button on:click={() => (handleClick(person.id))}>delete</button>
		</div>
	{:else}
		<p>There are no people to show...</p>
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