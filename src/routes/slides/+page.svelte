<script lang="ts">
	import { Presentation, type PresentationOptions, Slide, Vertical } from '@dreamingcodes/svelte-revealjs';
	import RevealMarkdown from 'reveal.js/plugin/markdown/markdown';
	import RevealNotes from 'reveal.js/plugin/notes/notes';
	import RevealSearch from 'reveal.js/plugin/search/search';
	import 'reveal.js/dist/theme/black.css';
	import postIt from '$lib/assets/postit.png';
	import Splash from './Splash.svelte';
	import What from './What.svelte';
	import Principi from './Principi.svelte';
	import Come from './Come.svelte';
	import Vantaggi from './Vantaggi.svelte';
	import Esempi from './Esempi.svelte';
	import Interactive from './Interactive.svelte';

	const revealjsOptions: PresentationOptions = {
		// presentation size respecting aspect ratio
		width: 1920,
		height: 1080,
		// content padding
		margin: 0,
		// smallest and largest possible scale
		minScale: 0.2,
		maxScale: 2.0,
		// plugins
		//TODO: Fix disabled plugins to work with ssr
		plugins: [RevealMarkdown, RevealNotes, RevealSearch/*, RevealZoom, RevealHighlight, RevealMath*/],
		// syntax highlight options
		highlight: {
			// add new languages
			//beforeHighlight: registerLanguages,
		},
		// slide controls
		controls: true,
		// slide progress bar
		progress: false,
		// slide transition
		transition: 'slide',
		// bring your own layout
		disableLayout: true,
		// display mode used to show slides
		display: 'block',
		// center slides on the screen
		center: true,
		// auto-animate duration
		autoAnimateDuration: 1,
		// auto-animate easing
		autoAnimateEasing: 'ease',
		// animate unmatched elements
		autoAnimateUnmatched: true,
		// hide cursor
		hideInactiveCursor: true,
		autoSlideStoppable: false,
		// time before cursor is hidden (ms)
		hideCursorTime: 5000,
		navigationMode: 'linear',
	};
</script>

<Presentation options="{revealjsOptions}">
  <Splash/>
	<What />
	<Principi />
	<Come />
	<Vantaggi />
	<Esempi />
	<Interactive/>
</Presentation>
