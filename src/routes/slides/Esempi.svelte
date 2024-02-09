<script>
	import { Slide } from '@dreamingcodes/svelte-revealjs';

	import twitter from '$lib/assets/twitter.png';
	import zara from '$lib/assets/zara.png';
	import toyota from '$lib/assets/toyota.png';
</script>

<Slide>
	<div class="slide-container">
		<div class="text-6xl">Aziende che hanno avuto successo usando Kanban</div>
		<div class="w-screen h-[70%] flex">
			<div class="img-container transform-gpu fragment custom blur-xl">
				<img src="{twitter}" alt="twitter">
			</div>
			<div class="img-container transform-gpu fragment custom blur-xl">
				<img src="{zara}" alt="zara">
			</div>
			<div class="img-container transform-gpu fragment custom blur-xl">
				<img src="{toyota}" alt="toyota">

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

		.img-container {
				@apply flex;
				flex-grow: 1;
				padding: 5rem;
				flex-basis: 0;
		}

    img {
        object-fit: contain;
    }

    .fragment.blur {
        filter: blur(5px);
    }

    :global(.fragment.blur-xl.visible) {
        filter: none;
    }
</style>
