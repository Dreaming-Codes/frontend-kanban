<script>
	import { Slide, Vertical } from '@dreamingcodes/svelte-revealjs';

	const principi = {
		'Trasparenza': 'La visualizzazione chiara delle attività promuove la trasparenza e favorisce una migliore comprensione del lavoro in corso.',
		'Adattabilità': "Il Kanban si basa sull'adattabilità per gestire i cambiamenti repentini nel flusso di lavoro e nelle priorità del progetto.",
		'Qualità': "Il controllo del flusso di lavoro consente al team di concentrarsi sulla qualità anziché sulla quantità, migliorando l'efficienza complessiva."
	};
</script>

<Vertical>
	<Slide animate animateId="principi">
		<div class="slide-container">
			<h1>I principi</h1>
		</div>
	</Slide>
	<Slide animate animateId="principi">
		<div class="slide-container">
			<h1>I principi</h1>
			<dl class="list-dl">
				{#each Object.entries(principi) as principio, index}
					<div class="fragment highlight-current-green custom blur" data-fragment-index="{index}">
						<span class="flex-auto">
							<dt>
								<span>{index+1}.</span>
								<span class="flex=auto">{principio[0]}</span>
							</dt>
							<dd class="fragment" data-fragment-index="{Object.entries(principi).length+index}">
								{principio[1]}
							</dd>
						</span>
					</div>
				{/each}
			</dl>
		</div>
	</Slide>
</Vertical>

<style>
    .slide-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100vw;
    }

    .fragment.blur {
        filter: blur(5px);
    }

    :global(.fragment.blur.visible) {
        filter: none;
    }
</style>
