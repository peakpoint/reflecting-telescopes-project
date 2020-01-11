<script>
    import { url } from '@sveltech/routify'
    import { fade } from 'svelte/transition'
    
    export let scoped
    const d = scoped.duration
    
    let fadeOut = {duration: d}
    let fadeIn = {duration: d, delay: d}
    let otherFadeIn = {duration: d, delay: d + 100}
</script>

<style lang='less'>
    @import 'styles.less';
    .e {
		text-align: center;
    }
    
    h1 {
		color: @orange;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
    
    p {
        font-size: 1.5em;
		font-weight: 80;
        margin: 0;
    }
</style>

<div class='e'>
    <h1 in:fade={fadeIn} out:fade={fadeOut}>404</h1>
    <p in:fade={otherFadeIn} out:fade={fadeOut}>Page not found</p>
    <p in:fade={otherFadeIn} out:fade={fadeOut}><a href={$url('../')}>Go back</a></p>
</div>
