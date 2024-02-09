<script lang="ts">
	import { Slide, Vertical } from '@dreamingcodes/svelte-revealjs';
	import { onMount } from 'svelte';
	import type JSConfetti from 'js-confetti';
	import { delay } from '$lib';

	let confettiCanvas: HTMLCanvasElement;

	let jsConfetti: JSConfetti;

	onMount(async () => {
		if (confettiCanvas) {
			confettiCanvas.width = window.outerWidth;
			confettiCanvas.height = window.innerHeight;
		}

		const confettiModule = await import('js-confetti');
		const JSConfetti = confettiModule.default;

		jsConfetti = new JSConfetti({ canvas: confettiCanvas });
	});

	async function throwConfetti() {
		await delay(1000);

		const emojis = jsConfetti.addConfetti({
			confettiNumber: 10,
			emojis: ['🍁']
		});
		const confetti = jsConfetti.addConfetti({
			confettiNumber: 200,
			confettiRadius: 10
		});
		await Promise.all([emojis, confetti]);
	}

	function resizeCanvas() {
		if (confettiCanvas) {
			confettiCanvas.width = window.outerWidth;
			confettiCanvas.height = window.innerHeight;
		}
	}

</script>

<svelte:window on:resize={resizeCanvas} />
<div class="absolute w-screen h-screen z-50">
	<canvas bind:this="{confettiCanvas}" />
</div>

<Vertical>
	<Slide animate>
		<div class="slide-container">
			<h1>Di cosa si tratta?</h1>

			<div class="table-container">
				<table class="table">
					<thead data-id="table-header">
					<tr>
						<th class="fragment highlight-current-green">To Do</th>
						<th class="fragment highlight-current-green">Doing</th>
						<th class="fragment highlight-current-green">Done</th>
					</tr>
					</thead>
					<tbody data-id="table-body">
					<tr class="fragment">
						<td data-id="design-frontend">Design frontend</td>
					</tr>
					<tr class="fragment">
						<td data-id="realizazione-frontend">Realizazione frontend</td>
					</tr>
					<tr class="fragment">
						<td data-id="realizazione-backend">Realizazione backend</td>
					</tr>
					</tbody>
				</table>
			</div>
		</div>
	</Slide>
	<Slide animate>
		<div class="slide-container">
			<h1>Di cosa si tratta?</h1>

			<div class="table-container">
				<table class="table">
					<thead data-id="table-header">
					<tr>
						<th>To Do</th>
						<th>Doing</th>
						<th>Done</th>
					</tr>
					</thead>
					<tbody data-id="table-body">
					<tr>
						<td data-id="realizazione-frontend">Realizazione frontend</td>
						<td data-id="design-frontend">Design frontend</td>
					</tr>
					<tr>
						<td data-id="realizazione-backend">Realizazione backend</td>
					</tr>
					<tr>
						<td />
					</tr>
					</tbody>
				</table>
			</div>
		</div>
	</Slide>
	<Slide animate>
		<div class="slide-container">
			<h1>Di cosa si tratta?</h1>

			<div class="table-container">
				<table class="table">
					<thead data-id="table-header">
					<tr>
						<th>To Do</th>
						<th>Doing</th>
						<th>Done</th>
					</tr>
					</thead>
					<tbody data-id="table-body">
					<tr>
						<td data-id="realizazione-frontend">Realizazione frontend</td>
						<td />
						<td data-id="design-frontend">Design frontend</td>
					</tr>
					<tr>
						<td data-id="realizazione-backend">Realizazione backend</td>
					</tr>
					<tr>
						<td />
					</tr>
					</tbody>
				</table>
			</div>
		</div>
	</Slide>
	<Slide animate data-autoslide="1500">
		<div class="slide-container">
			<h1>Di cosa si tratta?</h1>

			<div class="table-container">
				<table class="table">
					<thead data-id="table-header">
					<tr>
						<th>To Do</th>
						<th>Doing</th>
						<th>Done</th>
					</tr>
					</thead>
					<tbody data-id="table-body">
					<tr>
						<td />
						<td data-id="realizazione-frontend">Realizazione frontend</td>
						<td data-id="design-frontend">Design frontend</td>
					</tr>
					<tr>
						<td />
						<td data-id="realizazione-backend">Realizazione backend</td>
					</tr>
					<tr>
						<td />
					</tr>
					</tbody>
				</table>
			</div>
		</div>
	</Slide>
	<Slide animate on:in={throwConfetti}>
		<div class="slide-container">
			<h1>Di cosa si tratta?</h1>

			<div class="table-container">
				<table class="table">
					<thead data-id="table-header">
					<tr>
						<th>To Do</th>
						<th>Doing</th>
						<th>Done</th>
					</tr>
					</thead>
					<tbody data-id="table-body">
					<tr>
						<td />
						<td />
						<td data-id="design-frontend">Design frontend</td>
					</tr>
					<tr>
						<td />
						<td />
						<td data-id="realizazione-frontend">Realizazione frontend</td>
					</tr>
					<tr>
						<td />
						<td />
						<td data-id="realizazione-backend">Realizazione backend</td>
					</tr>
					</tbody>
				</table>
			</div>
		</div>
	</Slide>
</Vertical>


<style lang="postcss">
    th {
        @apply text-6xl text-center;
        width: 33.33%;
    }

    td {
        @apply !text-3xl;
        height: 70px;
    }

		.table {
				table-layout: fixed;
		}

		.table tbody tr:not(:last-child) {
				border-color: #e5e7eb;
		}

    .table-container {
        width: 90%;
        margin: 0 auto;
    }

		.slide-container {
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				height: 100vh;
				width: 100vw;
		}
</style>
