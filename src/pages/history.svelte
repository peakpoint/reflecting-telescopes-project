<script>
    import { url } from "@sveltech/routify"
    import { fade } from 'svelte/transition'
    export let scoped
    const d = scoped.duration
    
    let fadeIn = {duration: d, delay: d}
    let fadeOut = {duration: d}
    
    let eventList = [
        ['1632', 'Bonaventura Cavalieri proposed a telescope design similar to Newton\'s in his book, <em>Lo Specchio Ustorio</em>.'],
        ['1636', 'Marin Mersenne pulished <em>Harmonie Universelle</em> which contains reflecting telescope configurations. He never built any of his designs and was discouraged by René Descartes who saw the difficulty in making accurate curved mirrors.'],
        ['1663', 'James Gregory published a design for a reflecting telescope in his <em>Optica Promota</em>.'],
        ['1668', 'Isaac Newton created the first reflecting telescope.',
            '/images/NewtonsTelescopeReplica.jpg', 'A replica of Newton\'s second reflecting telescope made in 1672.'],
        ['1671', 'Newton\'s telescope is shown to the Royal Society of London.'],
        ['1672', 'The Cassegrain telescope design is published in an issue of <em>Journal des s&ccedil;avans</em>.'],
        ['1673', 'Robert Hooke built a Gregorian telescope.'],
        ['1721', 'John Hadley built a Newtonian telescope with a diameter of about 15 cm. His mirror was polished into a rough parabolic shape.'],
        ['1781', 'William Herschel discovered the planet Uranus with his 16 cm diameter Newtonian telescope.'],
        ['1783', 'Herschel completed his 20-foot telescope (6 m) with a 48.5 cm diameter mirror. It was converted from a Newtonian to a Herschelian type in 1786.'],
        ['1789', 'Herschel\'s 40-foot telescope (12 m) is completed with a mirror 120 cm in diameter. Using this, he discovered Enceladus and Mimas, the sixth and seventh moon of Saturn in order of discovery. <br> <br> Herschel prefered his smaller 20-foot telescope.', 
            '/images/40-foot_telescope_mirror.jpg', 'Herschel\'s 40-foot telescope mirror.'],
        ['1845', 'William Parsons, third Earl of Rosse created a Newtonian telescope with a 1.83 m diameter mirror. He discovered spiral "nebulae", which were later classified as galaxies.'],
        ['1908', 'The 60-inch reflecting telescope (1.5 m) was completed on Mount Wilson, Califonia.'],
        ['1917', 'The 100-inch (2.5 m) Hooker Telescope was completed on Mount Wilson.'],
        ['1927', 'George Willis Ritchey built the first Ritchey-Chr&eacute;tien telescope.'],
        ['1990', 'The Hubble Space Telescope is launched into orbit.'],
        ['The future', 'The James Webb Space Telescope is <a href=\'https://xkcd.com/2014/\' target=\'_blank\'>launched</a>.'],
    ]
    
    let dateSwitch = false
    setTimeout(() => dateSwitch = true, d + 50)
</script>

<style lang='less'>
    @import 'styles.less';

    div {
        color: @text-colour;
    }
    
    @offset: 15%;
    @spacing: 12em;
    
    .event {
        position: relative;
        margin: 0 20%;
        
        & .text {
            overflow-wrap: break-word;
            margin-left: @offset + @spacing;
            margin-right: 0;
            margin-bottom: 2em;
        }
    }
    
    .date {
        position: absolute;
        top: 0;
        bottom: 0;
        /* float: right; */
        text-align: right;
        /* 25% of the div */
        width: @offset;
    }
</style>

<h2
    in:fade={fadeIn}
	out:fade={fadeOut}
>Timeline of Refracting Telescopes</h2>

{#if dateSwitch}
    {#each eventList as [date, text, src, desc], i}
        <div class='event' out:fade={fadeOut}>
            <div
                data-aos='fade'
                data-aos-easing='ease-in-out-cubic'
                data-aos-anchor-placement='bottom-bottom'
            >
                <span class='date'>{date}</span>
                <p class='text'>{@html text}</p>
            </div>
            {#if src}
                <div
                    data-aos='fade'
                    data-aos-easing='ease-in-out-cubic'
                    data-aos-anchor-placement='bottom-bottom'
                    class='image'
                >
                    <img src={src} alt='' height='200'/>
                    <p>{desc}</p>
                </div>
            {/if}
        </div>
    {/each}
{/if}
