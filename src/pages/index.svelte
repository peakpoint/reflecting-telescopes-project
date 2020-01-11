<script>
	import { fade } from 'svelte/transition'
	export let scoped
	const d = scoped.duration
	
</script>

    
<main
	in:fade={{delay: d, duration: d}}
	out:fade={{duration: d}}
>
	<h1>Refracting telescopes</h1>
	<p>The start <strike>and end</strike> of my web development career</p>
	<p>SNC2DW individual physics project</p>
</main>

<style lang='less'>
	@import 'styles.less';
	
    main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}
	
	p {
		color: @darker-text-colour;
		user-select: none;
		font-size: 16px;
	}
	
	h1 {
		color: @orange;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>