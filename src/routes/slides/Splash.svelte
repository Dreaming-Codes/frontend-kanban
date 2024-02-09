<script>
import postIt from '$lib/assets/postit.png';
import { Slide, Vertical } from '@dreamingcodes/svelte-revealjs';
</script>

<Vertical>
	<Slide animate animateId="what">
		<div class="absolute h-screen w-screen place-content-center grid">
			<div class="text-[18rem] z-40" data-id="title">
				KANBAN
			</div>
		</div>
	</Slide>
	<Slide animate animateId="what">
		<div class="absolute h-screen w-screen place-content-center grid">
			<div class="text-[18rem]" data-id="title">
				KANBAN
			</div>
			<div class="absolute right-[15%] top-[45%] w-50 h-50">
				<img src="{postIt}" alt="post-it">
				<div class="absolute top-10 left-5 -rotate-[3deg] text-black text-2xl font-dancing-script">
					<div class="text-left font-bold">
						By:
					</div>
					<ul class="list-disc pl-3 font-light">
						<li>Lorenzo Rizzotti</li>
						<li>Matteo Faginali</li>
						<li>Lorenzo Chelini</li>
						<li>Rida Carola</li>
					</ul>
				</div>
			</div>
		</div>
	</Slide>

</Vertical>
