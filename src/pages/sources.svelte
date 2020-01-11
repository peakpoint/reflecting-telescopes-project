<script>
    import { fade } from 'svelte/transition'
    import { onMount } from 'svelte'
    
    export let scoped
    const d = scoped.duration
    let fadeIn = {duration: d, delay: d}
    let fadeOut = {duration: d}
    let otherFadeIn = {duration: d, delay: d + 100}
    
    let sourceList = [
        ['MacEvoy, Bruce.']
    ]
    
    onMount(() => {
        document.querySelectorAll('#content-wrap a').forEach(a => a.setAttribute('target', '_blank'))
    })
</script>

<h2
    in:fade={fadeIn}
    out:fade={fadeOut}
>
    Websites
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    MacEvoy, Bruce. "Astronomical Optics, Part 2: Telescope & Eyepiece Combined." <em>handprint</em>, Nov 26, 2013, 
    <a href='http://www.handprint.com/ASTRO/ae2.html'>www.handprint.com/ASTRO/ae2.html</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    ---. "Astronomical Optics, Part 4: Optical Aberrations." <em>handprint</em>, Nov 26, 2013, 
    <a href='http://www.handprint.com/ASTRO/ae4.html'>www.handprint.com/ASTRO/ae4.html</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Sacek, Vladimir. "The Newton reflector." <em>Amateur Telescope Optics</em>, July 14, 2006, 
    <a href='https://www.telescope-optics.net/reflecting.htm'>www.telescope-optics.net/reflecting.htm</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    ---. "Two-mirror telescopes: Cassegrain, Gregorian and variants." <em>Amateur Telescope Optics</em>, July 14, 2006, 
    <a href='https://www.telescope-optics.net/two-mirror.htm'>www.telescope-optics.net/two-mirror.htm</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    ---. "Classical and aplanatic two-mirror telescopes." <em>Amateur Telescope Optics</em>, July 14, 2006, 
    <a href='https://www.telescope-optics.net/classical_and_aplanatic.htm'>www.telescope-optics.net/classical_and_aplanatic.htm</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Maurer, Andreas. "William Herschel's Astronomical Telescopes." <em>Journal of the British Astronomical Association</em>, vol. 81, pp. 284-291, May 1971, 
    <a href='https://ui.adsabs.harvard.edu/abs/1971JBAA...81..284M'>ui.adsabs.harvard.edu/abs/1971JBAA...81..284M</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    "Early Reflectors." <em>Cosmic Journey: A History of Scientific Cosmology</em>, Center for History of Physics, 
    <a href='https://history.aip.org/history/exhibits/cosmology/tools/tools-early-reflectors.htm'>history.aip.org/history/exhibits/cosmology/tools/tools-early-reflectors.htm</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Bond, Peter. "Telescopes in History." <em>Encyclopedia of Astronomy and Astrophysics</em>, November 2000, 
    <a href='http://www.astro.caltech.edu/~george/ay20/telescopes-history.pdf'>www.astro.caltech.edu/~george/ay20/telescopes-history.pdf</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Murdin, Paul and Patrick Moore. "Reflecting Telescopes." <em>Encyclopedia of Astronomy and Astrophysics</em>, November 2000, 
    <a href='http://www.astro.caltech.edu/~george/ay20/reflecting-telescopes.pdf'>www.astro.caltech.edu/~george/ay20/reflecting-telescopes.pdf</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Sant, Joseph. "The Early Reflecting Telescope:Cassegrain and Mersenne." <em>scientus</em>, 
    <a href='http://www.scientus.org/Reflecting-Telescope-History.html'>www.scientus.org/Reflecting-Telescope-History.html</a>.
</p>


<p in:fade={otherFadeIn} out:fade={fadeOut}>
    "In depth: Telescope." <em>Museo Galileo</em>, 
    <a href='https://catalogue.museogalileo.it/indepth/Telescope.html'>catalogue.museogalileo.it/indepth/Telescope.html</a>.
</p>

<!-- 
{#each sourceList as [author, title, date]}
    <p in:fade={otherFadeIn} out:fade={fadeOut}>
        {source}
    </p>
{/each} -->

<h2
    in:fade={fadeIn}
    out:fade={fadeOut}
>
    Images
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    User:Geni. Hershel's 40-foot telescope mirror on display. <em>Wikimedia Commons</em>, September 2008,
    <a href='https://commons.wikimedia.org/wiki/File:40-foot_telescope_mirror.jpg'>commons.wikimedia.org/wiki/File:40-foot_telescope_mirror.jpg</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    User:Kowloonese. Ritchey's reflecting telescope. <em>Wikimedia Commons</em>, July 2004,
    <a href='https://commons.wikimedia.org/wiki/File:RitcheyTelescope.jpg'>commons.wikimedia.org/wiki/File:RitcheyTelescope.jpg</a>.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Dunn, Andrew. Replica of Newton's second reflecting telescope. <em>Wikimedia Commons</em>, November 5, 2004,
    <a href='https://commons.wikimedia.org/wiki/File:NewtonsTelescopeReplica.jpg'>commons.wikimedia.org/wiki/File:NewtonsTelescopeReplica.jpg</a>.
</p>
