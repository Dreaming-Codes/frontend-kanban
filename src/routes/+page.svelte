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

	let task: string;

	let connected = false;

	onMount(async () => {
		const peerModule = await import('peerjs');
		const Peer = peerModule.Peer;

		const response = await fetch("https://dreamingcodes.metered.live/api/v1/turn/credentials?apiKey=ae83c67b424b2898cb83fe90545822b812de");

		// Saving the response in the iceServers array
		const iceServers = await response.json();

		peer = new Peer({
			config: {
				'iceServers': iceServers
			}
		});

		peer.once('open', ()=>{
			console.log('Connecting to', data.id);
			dataConnection = peer.connect(data.id as string);

			dataConnection.on('data', (data) => {
				console.log('Received', data);
			})

			dataConnection.on('error', (err) => {
				console.error('Error', err);
			})

			dataConnection.once('open', ()=> {
				console.log('Connected to', data.id);
				connected = true;
			})
		})
	});

	function sendTask() {
  if (task.lenght < 5) {
     return;
  }
		dataConnection.send(task);
		task = '';
	}


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
		<div class="flex flex-col items-center content-center justify-items-center h-screen w-screen px-5" transition:blur>
			<div class="input-group input-group-divider my-auto">
				<input type="search" placeholder="Inserisci task" class="py-4" minlength="8" maxlength="30" bind:value={task} />
				<button class="variant-filled-secondary py-2" on:click={sendTask}><span class="w-full">Invia</span></button>
			</div>
		</div>
	{/if}
{/if}

