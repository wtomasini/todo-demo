<script>
    let number;

    async function roll() {
        const response = await fetch('/api/roll');
        number = await response.json();
    }

    export let data;
</script>

<h1>The API Zone (under construction)</h1>

<h3>Roll the dice with API power</h3>

<button on:click={roll}>Roll the dice</button>

{#if number !== undefined}
    <p>You rolled a {number}</p>
{:else}
    <p>Waiting for dice roll...</p>
{/if}

<br>
<div class="centered">
    <h1>To-do: figure out why this breaks</h1>

    <label>
        add a todo:
        <input
                type="text"
                autocomplete="off"
                on:keydown={async (e) => {
				if (e.key !== 'Enter') return;

				const input = e.currentTarget;
				const description = input.value;

				const response = await fetch('/api', {
                    method: 'POST',
                    body: JSON.stringify({ description }),
                    headers: {
                        'Content-Type': 'application/json'
                    }
				});

                const {id} = await response.json()

                data.todos = [...data.todos, {
                    id,
                    description
                }];

				input.value = '';
			}}
        />
    </label>

    <ul class="todos">
        {#each data.todos as todo (todo.id)}
            <li>
                <label>
                    <input
                            type="checkbox"
                            checked={todo.done}
                            on:change={async (e) => {
							const done = e.currentTarget.checked;

							await fetch(`/api/${todo.id}`, {
                                method: 'PUT',
                                body: JSON.stringify({done}),
                                headers: {'Content-Type': 'application/json'}
							});
						}}
                    />
                    <span>{todo.description}</span>
                    <button
                            aria-label="Mark as complete"
                            on:click={async (e) => {
							await fetch(`/api/${todo.id}`, {
                                method: 'DELETE'
							});

                            data.todos = data.todos.filter((t) => t !== todo);
						}}
                    >Remove</button>
                </label>
            </li>
        {/each}
    </ul>
</div>

<style>
    .centered {
        max-width: 40em;
        margin: 0 auto;
    }

    label {
        display: flex;
        width: 100%;
    }

    input[type="text"] {
        flex: 1;
    }

    span {
        flex: 1;
    }

    /*button {*/
    /*    border: none;*/
    /*    background: url(/remove.svg) no-repeat 50% 50%;*/
    /*    background-size: 1rem 1rem;*/
    /*    cursor: pointer;*/
    /*    height: 100%;*/
    /*    aspect-ratio: 1;*/
    /*    opacity: 0.5;*/
    /*    transition: opacity 0.2s;*/
    /*}*/

    button:hover {
        opacity: 1;
    }
</style>
