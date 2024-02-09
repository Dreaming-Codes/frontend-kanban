<script>
	import { Slide, Vertical } from '@dreamingcodes/svelte-revealjs';
	import vortex from '$lib/assets/vortex.jpg?url';
</script>

<Vertical>
	<Slide image="{vortex}" data-background-opacity="0.3" data-background-color="black" >
		<div class="slide-container">
			<div class="text-6xl">Vantaggi del metodo Kanban</div>
			<div class="mt-20 h-1/2 w-[80%] flex gap-6">
				<div class="card variant-glass p-4">
					<header class="card-header">Efficienza Operativa</header>
					<div class="p-4 desc">Il Kanban consente un flusso di lavoro più fluido, riducendo i tempi di attesa e
						aumentando l'efficienza complessiva.
					</div>
				</div>
				<div class="card variant-glass p-4">
					<header class="card-header">
						Riduzione degli sprechi
					</header>
					<div class="p-4 desc">
						Elimina sprechi di risorse attraverso una gestione ottimizzata delle attività, garantendo che le risorse
						siano allocate solo quando necessario.
					</div>
				</div>
				<div class="card variant-glass p-4">
					<header class="card-header">
						Adattabilità
					</header>
					<div class="p-4 desc">
						Il Kanban si adatta facilmente a cambiamenti e nuove esigenze, fornendo una flessibilità essenziale per
						affrontare dinamiche di mercato in continua evoluzione.
					</div>
				</div>
			</div>
		</div>
	</Slide>
	<Slide image="{vortex}" data-background-opacity="0.3" data-background-color="black">
		<div class="slide-container">
			<div class="text-6xl">Svantaggi del metodo Kanban</div>
			<div class="mt-20 h-1/2 w-[80%] flex gap-6">
				<div class="card variant-glass-error p-4">
					<header class="card-header">Comprensione Incompleta</header>
					<div class="p-4 desc">L'implementazione del Kanban richiede una comprensione approfondita e la cooperazione di tutti i membri del team, il che potrebbe rappresentare una sfida iniziale.
					</div>
				</div>
				<div class="card variant-glass-error p-4">
					<header class="card-header">
						Rischio di Sovraccarico di Lavoro
					</header>
					<div class="p-4 desc">
						Senza un controllo adeguato, c'è il rischio di sovraccaricare i membri del team con troppe attività simultanee, compromettendo la qualità del lavoro.
					</div>
				</div>
			</div>
		</div>
	</Slide>
</Vertical>

<style lang="postcss">
    .slide-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100vw;
    }

		.desc {
			font-size: 1.6rem;
		}

    header {
        font-size: 2.3rem;
        font-weight: 600;
    }

    .card {
        flex-basis: 0;
        flex-grow: 1;
    }

		.variant-glass {
				@apply transform-gpu;
		}

    .variant-glass-error {
        @apply transform-gpu;
    }
</style>
