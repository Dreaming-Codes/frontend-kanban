<script lang="ts">
	import { ProgressRadial } from '@skeletonlabs/skeleton';
	import { blur } from 'svelte/transition';
	import type { PageData } from './$types';
	import { onMount } from 'svelte';
	import type Peer from 'peerjs';
	import type { DataConnection } from 'peerjs';

	export let data: PageData;
	let peer: Peer;
	let dataConnection: DataConnection;

	let connected = false;

	onMount(async () => {
		const peerModule = await import('peerjs');
		const Peer = peerModule.Peer;

		peer = new Peer();

		peer.once('open', ()=>{
			console.log('Connecting to', data.id);
			dataConnection = peer.connect(data.id as string);

			dataConnection.once('open', ()=> {
				console.log('Connected to', data.id);
				connected = true;
			})
		})


	});


</script>

{#if !data.id}
	<div class="flex flex-col items-center content-center justify-items-center h-screen w-screen" transition:blur>
		<div class="my-auto mx-auto flex flex-col items-center">
			<div class="text-4xl text-center">Errore durante la connessione</div>
		</div>
	</div>
{:else}
	{#if !connected}
		<div class="flex flex-col items-center content-center justify-items-center h-screen w-screen" transition:blur>
			<div class="my-auto mx-auto flex flex-col items-center">
				<ProgressRadial class="mb-12" stroke="{100}" strokeLinecap="round" meter="stroke-primary-500" />
				<div class="text-4xl text-center">Calcolando l'ipertraiettoria...</div>
				<div class="text-2xl text-center">Ricordati: non dimenticare il tuo asciugamano!</div>
			</div>
		</div>
	{:else}
		<div></div>
	{/if}
{/if}

