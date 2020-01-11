<script>
    import { fade } from 'svelte/transition'
    import { url } from '@sveltech/routify'
    import { onMount } from 'svelte'
    
    export let scoped
    const d = scoped.duration
    
    let fadeOut = {duration: d}
    let fadeIn = {duration: d, delay: d}
    let otherFadeIn = {duration: d, delay: d + 100}
    
    let bgCol = window.getComputedStyle(document.body).getPropertyValue('background-color')
    
    let sketch0 = p5 => {
        let vertices = [], mag = 2000, off = 1, foc, calc
        let mAmp = 20, mOff = 100, hh
        
        p5.setup = () => {
            p5.createCanvas(600, 300)
            
            hh = p5.height / 2
            
            calc = i => (i - hh) ** 2 / -mag + p5.width - off
            
            foc = p5.width - off - mag / 4
            
            for (let i = 0; i <= p5.height; i += 1) vertices.push(calc(i))
        }
        
        p5.draw = () => {
            let c = calc(p5.mouseY)
            let r = [c, p5.mouseY]
            let f = [foc, p5.height / 2]
            let oFoc = [foc + mOff, hh - mOff]
            
            let mirror = [
                foc + mOff - mAmp, hh - mAmp, 
                foc + mOff + mAmp, hh + mAmp
            ]
            
            p5.background(bgCol)
            p5.noFill()
            p5.strokeWeight(2)
            
            p5.stroke(60)
            p5.drawingContext.setLineDash([10, 10])
            p5.line(0, hh, p5.width - off, hh)
            
            p5.drawingContext.setLineDash([])
            p5.stroke('#FF0000')
            if (0 <= p5.mouseY && p5.mouseY <= p5.height) {
                p5.line(0, p5.mouseY, c, p5.mouseY)
                
                let coll = p5.collideLineLine(...mirror, ...r, ...f, true)
                if (coll.x) {
                    p5.line(...oFoc, coll.x, coll.y)
                    p5.line(...r, coll.x, coll.y)
                    
                    p5.drawingContext.setLineDash([3, 6])
                    p5.line(...f, coll.x, coll.y)
                    
                    p5.drawingContext.setLineDash([])
                } else {
                    p5.line(...r, ...f)
                }
            }
            
            p5.stroke(150)
            p5.beginShape()
            for (let i in vertices) p5.vertex(vertices[i], i)
            p5.endShape()
            
            // p5.stroke(150)
            p5.strokeWeight(6)
            p5.point(foc, hh)
            p5.point(...oFoc)
            
            p5.strokeWeight(2)
            p5.line(...mirror)
            
            // p5.strokeWeight(4)
            // if (coll.x) p5.point(coll.x, coll.y)
        }
    }
    
    onMount(() => {
        new p5(sketch0, 'holder-newton')
    })
    
</script>

<style lang='less'>
    @import './styles.less';
    
    #holder-newton {
        width: 600px;
    }
    
</style>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Newtonian Telescope
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    The newtonian reflector uses a parabolic primary mirror and a flat secondary mirror placed 45 degrees diagonally.
     
    This has the effect of moving the focus 90 degrees from the telescope.
    
    This design is popular among amateur reflectors.
</p>

<div
    id='holder-newton'
    class='holder'
    in:fade={otherFadeIn}
    out:fade={fadeOut}
></div>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Newton created a reflector because refractors suffer from chromatic abberation. 
    
    He originally used a spherical mirror since it was easier to make than a parabolic one, despite spherical abberation. 
    
    With a parabolic mirror, this design suffers from optical coma.
    
    If the focus of the primary mirror is very long, a ladder is necessary to use the eyepiece. 
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    See <a href={$url('/aberrations')}>aberrations</a>.
</p>

<h3 in:fade={fadeIn} out:fade={fadeOut}>
    Mirror Offset
</h3>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Playing around with the canvas, you may have noticed when the ray is reflected off the secondary mirror. 
    
    The range above the principal axis where the ray is reflected is larger than the range below.
    
    This is due to the tilt of the secondary mirror the fact that it is centered on the principal axis. 
    
    It causes an uneven distrubution of light.
    
    The problem is fixed by offsetting the secondary mirror towards the back and away from the eyepiece (moving it down and to the right in the diagram).
</p>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Herschelian telescope
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    The speculum metal (an alloy of copper and tin) used to make mirrors historically only reflected about 60% of the light. 
    
    The metal would also rapidly tarnish.
    
    Two mirror designs would then reflect about 40% of the light. 
    
    William Herschel would use one off-axis parabolic mirror for his large telescopes for better luminosity. 
    
    The location for observation would be on the side of the telescope similar to the Newtonian design. This design inherently suffers from optical coma, however.
</p>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Gregorian Telescope
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    The Gregorian telescope design uses a parabolic primary mirror and a elliptical secondary mirror. 
    
    The parabolic mirror reflects parallel rays though its focus which, by design, is also a focus of the elliptical mirror. 
    
    The ray then goes through the second focus of the ellipse where the eyepiece is located.
    
    The image is upright and located behind the primary mirror. 
    
    Since the secondary miror has to be placed outside the focus of the primary mirror, telescopes of this design have to be longer than the focus length.
    
    This design is not used anymore.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    See <a href={$url('/conics')}>conics</a>.
</p>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Cassegrain Telescope
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    The Cassegrain telescope design uses a parabolic primary mirror and a (convex) hyperbolic secondary mirror. 
    
    Similar to the Gregorian design, the mirrors share a focus and the image if formed behind the primary mirror.
    
    This configuration, and variations of it, are still widely used.
    
    Since the secondary miror has to be placed inside the focus of the primary mirror, telescopes of this design are shorter than the focus length making this a more convenient design than the Gregorian telescope.
    
    This design is widely used.
</p>
<!-- – -->
<h3 in:fade={fadeIn} out:fade={fadeOut}>
    Ritchey-Chr&eacute;tien Telescope
</h3>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    The Ritchey-Chr&eacute;tien design is a variation of the Cassegrain that eliminates optical coma.
    
    It was proposed by Henri Chr&eacute;tien and first built by George Willis Ritchey. 
    
    It uses a hyperbolic primary mirror instead of a parabolic one.
    
    This design is popular for professional telescopes, for example, the Hubble Space Telescope.
</p>

<div class='image'>
    <img src='/images/RitcheyTelescope.jpg' alt='Ritchey&#39;s 24 inch (61 cm) reflecting telescope' height='400'/>
    <p>George W. Ritchey's 24 inch (61 cm) reflecting telescope on display.</p>
</div>
