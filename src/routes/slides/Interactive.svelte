<script lang="ts">
	import { flip } from 'svelte/animate';
	import { Slide } from '@dreamingcodes/svelte-revealjs';
	import { dndzone } from 'svelte-dnd-action';
	import { onMount } from 'svelte';
	import { browser } from '$app/environment';

	import QR from '@svelte-put/qr/svg/QR.svelte';

	let connectionId = '';

	$: connectionUrl = `${import.meta.env.VITE_APP_URL}/?id=${connectionId}`;

	let incrementalId = 0;

	let ingressItems: {id: number, name: string}[] = [];

	let todoItems: {id: number, name: string}[] = [];

	let inProgressItems: {id: number, name: string}[] = [];

	let doneItems: {id: number, name: string}[] = [];

	const flipDurationMs = 300;

	function handleDndIngressConsider(e) {
		ingressItems = e.detail.items;
	}

	function handleDndIngressFinalize(e) {
		ingressItems = e.detail.items;
	}

	function handleDndTodoConsider(e) {
		todoItems = e.detail.items;
	}

	function handleDndTodoFinalize(e) {
		todoItems = e.detail.items;
	}

	function handleDndInProgressConsider(e) {
		inProgressItems = e.detail.items;
	}

	function handleDndInProgressFinalize(e) {
		inProgressItems = e.detail.items;
	}

	function handleDndDoneConsider(e) {
		doneItems = e.detail.items;
	}

	function handleDndDoneFinalize(e) {
		doneItems = e.detail.items;
	}

	function handleDeleteItem(id) {
		ingressItems = ingressItems.filter(item => item.id !== id);
		todoItems = todoItems.filter(item => item.id !== id);
		inProgressItems = inProgressItems.filter(item => item.id !== id);
		doneItems = doneItems.filter(item => item.id !== id);
	}

	onMount(async () => {
		if (!browser) return;

		const peerJsModule = await import('peerjs');
		const Peer = peerJsModule.Peer;

		const peer = new Peer();

		peer.addListener('open', (id)=> {
			connectionId = id;
			console.log('My peer ID is: ' + id);
		})

		peer.addListener('connection', (data) => {
			console.log('connection', data);
			data.addListener('open', () => {
				data.send('Hello, world!');
			});
			data.addListener('data', (data) => {
				ingressItems.push({ id: incrementalId++, name: data as string });
			});
		});
	});
</script>

<Slide>
	<div class="absolute slide-container z-50 fragment fade-out bg-black/70 backdrop-blur">
		<QR class="max-h-[70%] mx-auto" data="{connectionUrl}"/>
	</div>
	<div class="slide-container">
		<div class="w-full h-full p-20 flex gap-4">
			<div class="card flex flex-col">
				<header class="card-header my-4">
					INGRESS
				</header>
				<hr>
				<div class="flex-col grow hide-scrollbar overflow-y-scroll"
						 use:dndzone="{{items: ingressItems, flipDurationMs}}" on:consider="{handleDndIngressConsider}"
						 on:finalize="{handleDndIngressFinalize}">
					{#each ingressItems as item(item.id)}
						<div on:dblclick={()=>handleDeleteItem(item.id)} class="card mt-4 p-4 mx-2 inner-card"
								 animate:flip="{{duration: flipDurationMs}}">{item.name}</div>
					{/each}
				</div>
			</div>
			<div class="card flex flex-col">
				<header class="card-header my-4">
					TODO
				</header>
				<hr>
				<div class="flex-col grow hide-scrollbar overflow-y-scroll" use:dndzone="{{items: todoItems, flipDurationMs}}"
						 on:consider="{handleDndTodoConsider}" on:finalize="{handleDndTodoFinalize}">
					{#each todoItems as item(item.id)}
						<div on:dblclick={()=>handleDeleteItem(item.id)} class="card mt-4 p-4 mx-2 inner-card"
								 animate:flip="{{duration: flipDurationMs}}">{item.name}</div>
					{/each}
				</div>
			</div>
			<div class="card flex flex-col">
				<header class="card-header my-4">
					IN PROGRESS
				</header>
				<hr>
				<div class="flex-col grow hide-scrollbar overflow-y-scroll"
						 use:dndzone="{{items: inProgressItems, flipDurationMs}}" on:consider="{handleDndInProgressConsider}"
						 on:finalize="{handleDndInProgressFinalize}">
					{#each inProgressItems as item(item.id)}
						<div on:dblclick={()=>handleDeleteItem(item.id)} class="card mt-4 p-4 mx-2 inner-card"
								 animate:flip="{{duration: flipDurationMs}}">{item.name}</div>
					{/each}
				</div>
			</div>
			<div class="card flex flex-col">
				<header class="card-header my-4">
					DONE
				</header>
				<hr>
				<div class="flex-col grow hide-scrollbar overflow-y-scroll" use:dndzone="{{items: doneItems, flipDurationMs}}"
						 on:consider="{handleDndDoneConsider}" on:finalize="{handleDndDoneFinalize}">
					{#each doneItems as item(item.id)}
						<div on:dblclick={()=>handleDeleteItem(item.id)} class="card mt-4 p-4 mx-2 inner-card"
								 animate:flip="{{duration: flipDurationMs}}">{item.name}</div>
					{/each}
				</div>
			</div>
		</div>
	</div>
</Slide>

<style lang="postcss">
    .slide-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100vw;
    }

    .card {
        flex-basis: 0;
        flex-grow: 1;
    }

    .inner-card {
        @apply variant-glass-primary;
    }
</style>
