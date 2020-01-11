<svelte:head>
	 <title>Reflecting Telescopes</title>
</svelte:head>

<script>
    // import { onMount } from 'svelte'
    import { url, isActive } from "@sveltech/routify"
	
	AOS.init()
    
    const _links = [
        ["./index", "Home"],
        ["./history", "History"],
        ["./types", "Types"],
        ["./aberrations", "Aberrations"],
        ["./conics", "Conics"],
        ["./sources", "Sources"],
    ]
    
    $: links = _links.map(([path, name]) => {
        return {
            href: $url(path, {}),
            name,
            active: $isActive(path)
        }
	})
	
	let navHeight
</script>

<style lang='less'>
    @import 'styles.less';
    
	@header-height: 3em;
	@hover-colour: #303030;
	
	
	:global(.image) {
        text-align: center;
        margin-bottom: 2em;   
	}
	
	:global(.image p) {
			font-size: 16px;
            display: block;
            margin: 0 auto;
            color: @darkish-text-colour;
            padding-top: 0.5em;
	}
	
	:global(::-webkit-scrollbar) {
		width: 0px;
		background: transparent;
	}
	
    :global(h2) {
        text-align: center;
        color: @text-colour;
        font-weight: 400;
		font-size: 40px;
		margin: 0.8em 15%;
	}
	
	:global(h3) {
		text-align: center;
        color: @text-colour;
        font-weight: 340;
		font-size: 30px;
		margin: 0.7em 15%;
	}
	
	:global(p) {
		margin: 1em 10%;
		color: @text-colour;
		font-size: 20px;
	}
	
	:global(body) {
		padding: 0;	
	}
	
	:global(.holder) {
        display: block;
        margin: 0 auto;
	}
	
	@link-colour: #588cc0;
	
	:global(a) {
		color: @link-colour;
		transition-duration: 0.5s;
		
		&:visited {
			color: @link-colour;
		}
		
		&:hover {
			text-decoration: underline;
			color: saturate(@link-colour, 40%);
		}
	}
    
    .nav {
		width: 100%;
		/* height: @header-height; */
        background: #292929;
		user-select: none;
		z-index: 10;
		
		display: inline-block;
        text-align: center;
		
        position: fixed;
		top: 0;
		left: 0;
		right: 0;
		
        
        .link {
            padding: 0 30px;
            /* width: 64px; */
			display: inline-block;
			color: @darkish-text-colour;
			
			line-height: @header-height;
			white-space: nowrap;
			transition-duration: 0.2s;
            
            &.active {
				color: @lighter-text-colour;
                /* font-weight: bold; */
            }
			
			&:hover {
				color: @lighter-text-colour;
				background-color: @hover-colour;
				text-decoration: none;
			}
			
			&:active {
				color: @lighter-text-colour;
				background-color: #424242;
			}
        }	
    }
	
    #page-container {
		position: relative;
		min-height: 100vh;
	}
	
	@footer-height: 4em;
	
	#content-wrap {
		/* padding-top: @header-height; */
		padding-bottom: @footer-height + 1em;
	}
	
	#footer {
		position: absolute;
		bottom: 0;
		width: 100%;
		height: calc(@footer-height + 1px);
		/* opacity: 50%; */
		user-select: none;
		
		/* display: flex; */
		/* align-items: center; */
		
		& p {
			border-top: 1px solid @darker-text-colour;
			color: @darker-text-colour;
			line-height: @footer-height;
			font-size: 16px;
			
			margin: 0;
			padding-left: 10%;
			
			transition-duration: 0.3s;
			
			&:hover {
				border-top: 1px solid @dark-text-colour;
				color: @dark-text-colour;
			}
		}
		
	}
</style>

<div id="page-container">
	<aside>
		<div class="nav" bind:clientHeight={navHeight}>
			{#each links as { href, name, active }}
				<a class="link" class:active {href}>{name}</a>
			{/each}
		</div>
	</aside>
	
	<div style={'height: ' + navHeight + 'px;'}></div>
	
	<div id="content-wrap">
        <slot scoped={{duration: 200}}></slot>
	</div>

	<footer id="footer">
		<p>Made by Tian Chen</p>
	</footer>
</div>

