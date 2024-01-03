<script>
	import { onMount } from 'svelte'
	let title = 'New Note'
	let text = ''
	let items = []
    function getallNotes() {
        return Object.keys(localStorage)
    }
	onMount(() => {
		items =getallNotes()
	})
	const saveToStore = () => {
		localStorage.setItem(title.trim(), text)
        if (!items.includes(title.trim())){
            items = getallNotes()
        }
	}
    const handleClick = (event) => {
        title = event.target.textContent
        text = localStorage.getItem(title)
    }
    const clearNote = () =>{
        localStorage.removeItem(title)
        items = getallNotes()
        title = "New Note"
        text = ""
    }
</script>

<div class="super-parent">
	<aside>
		<p class="heading-1">Your Previous Notes</p>
		<ul>
			{#each items as item}
				<li>
                    <button on:click={handleClick}>

                        {item}
                    </button> 
                </li>
			{/each}
		</ul>
	</aside>
	<main class="container">
		<div class="controls">
			<div class="title">
				<input type="text" bind:value={title} class="title-text" />
			</div>
			<div class="btns">
				<a href="/" role="button" on:click={saveToStore}>Save</a>
				<a href="/" role="button" on:click={clearNote}>Clear</a>
			</div>
		</div>
		<textarea id="notepad-area" bind:value={text}></textarea>
	</main>
</div>

<style>
</style>
