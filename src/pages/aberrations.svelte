<script>
    import { fade } from 'svelte/transition'
    import { onMount } from 'svelte'
    
    export let scoped
    const d = scoped.duration
    
    let fadeOut = {duration: d}
    let fadeIn = {duration: d, delay: d}
    let otherFadeIn = {duration: d, delay: d + 100}
    
    let bgCol = window.getComputedStyle(document.body).getPropertyValue('background-color')
    
    let sketch1 = p5 => {
        let rad = 100, off = 50, hh, sc = 20
        
        p5.setup = () => {
            p5.createCanvas(600, 300)
            
            hh = p5.height / 2
        }
        
        p5.draw = () => {
            p5.background(bgCol)
            p5.noFill()
            p5.strokeWeight(2)
            
            p5.stroke(60)
            p5.drawingContext.setLineDash([10, 10])
            p5.line(0, hh, p5.width, hh)
            
            p5.stroke('#FF0000')
            if (p5.mouseY > hh - rad && p5.mouseY < hh + rad) {
                p5.drawingContext.setLineDash([])
                let y = p5.mouseY - hh, inter = p5.width - rad - off + Math.sqrt(rad ** 2 - y ** 2)
                p5.line(0, p5.mouseY, inter, p5.mouseY)
                
                let s = y / rad
                
                let refl = [
                    2 * y * s * Math.sqrt(1 - s ** 2) + p5.width - rad - off, 
                    y * (2 * s ** 2 - 1) + hh
                ]
                
                let scaled = [
                    sc * (refl[0] - inter) + inter,
                    sc * (refl[1] - p5.mouseY) + p5.mouseY
                ]
                
                let coll = p5.collideLineLine(
                    0, hh, p5.width, hh,
                    inter, p5.mouseY, ...scaled, true
                )
                
                if (coll.x) {
                    p5.line(inter, p5.mouseY, coll.x, coll.y)
                    p5.drawingContext.setLineDash([3, 6])
                    p5.line(coll.x, coll.y, ...scaled)
                } else {
                    p5.line(inter, p5.mouseY, ...scaled)
                }
                
                p5.stroke(150)
                p5.strokeWeight(6)
                if (coll.x) p5.point(coll.x, coll.y)
                else if (p5.mouseY == hh) p5.point(p5.width - rad / 2 - off, hh)
            }
            
            p5.stroke(150)
            p5.strokeWeight(2)
            
            p5.drawingContext.setLineDash([5, 10])
            p5.arc(p5.width - rad - off, p5.height / 2, 2 * rad, 2 * rad, p5.HALF_PI, -p5.HALF_PI)
            
            p5.drawingContext.setLineDash([])
            p5.arc(p5.width - rad - off, p5.height / 2, 2 * rad, 2 * rad, -p5.HALF_PI, p5.HALF_PI)
            
            // p5.point()
        }
    }
    
    let sketch2 = p5 => {
        let hh, vertices = {}, mag = 500, off = 1, foc, calc
        let init = [], step = 30
        let offScreen = 100, sc = 10
        
        p5.setup = () => {
            p5.createCanvas(600, 400)
            
            hh = p5.height / 2
            
            calc = i => (i - hh) ** 2 / -mag + p5.width - off
            
            foc = p5.width - off - mag / 4
            
            for (let i = -offScreen; i <= p5.height + offScreen; i += 1) vertices[i] = calc(i)
            
            for (let i = hh - step / 2; i > 0; i -= step) {
                init.push(i, p5.height - i)
            }
        }
        
        p5.draw = () => {
            let c = calc(p5.mouseY)
            let r = [c, p5.mouseY]
            let f = [foc, p5.height / 2]
            
            p5.background(bgCol)
            p5.noFill()
            p5.strokeWeight(2)
            
            p5.stroke(60)
            p5.drawingContext.setLineDash([10, 10])
            p5.line(0, hh, p5.width - off, hh)
            
            p5.drawingContext.setLineDash([])
            p5.stroke('#FF000066')
            if (
                // true ||
                0 <= p5.mouseY && p5.mouseY <= p5.height
            ) {
                // p5.line(0, p5.mouseY, c, p5.mouseY)
                
                
                for (let y of init) {
                    p5.stroke('#FF000066')
                    p5.strokeWeight(2)
                    let l = [p5.width, y, 0, y - hh + p5.mouseY]
                    // p5.line(...l)
                    
                    let i = -offScreen, refLines = []
                    while (true) {
                        let coll = p5.collideLineLine(...l, vertices[i], i, vertices[i+1], i+1)
                        
                        if (coll) {
                            coll = p5.collideLineLine(
                                ...l,
                                vertices[i], i, vertices[i+1], i+1,
                                true
                            )
                            
                            // p5.strokeWeight(6)
                            // p5.stroke('green')
                            // p5.point(coll.x, coll.y)
                            
                            let dx = coll.x, dy = l[3] - coll.y
                            let hy = Math.hypot(dx, dy)
                            
                            // p5.stroke('yellow')
                            let ref = [
                                dx/hy * (foc - coll.x) - dy/hy * (hh - coll.y) + coll.x,
                                dy/hy * (foc - coll.x) + dx/hy * (hh - coll.y) + coll.y
                            ]
                            
                            let scaled = [
                                sc * (ref[0] - coll.x) + coll.x,
                                sc * (ref[1] - coll.y) + coll.y
                            ]
                            
                            // p5.point(...ref)
                            // p5.strokeWeight(2)
                            // p5.line(coll.x, coll.y, ...ref)
                            // p5.line(coll.x, coll.y, ...scaled)
                            refLines.push([coll.x, coll.y, ...scaled])
                            p5.line(0, l[3], coll.x, coll.y)
                            
                            break
                        }
                        
                        i++
                        
                        if (i > p5.height + offScreen) break
                    }
                    
                    p5.stroke('#FF0000')
                    for (let line of refLines) p5.line(...line)
                }
            }
            
            p5.strokeWeight(2)
            p5.stroke(150)
            p5.beginShape()
            for (let i = -offScreen; i <= p5.height + offScreen; i += 1) p5.vertex(vertices[i], i)
            p5.endShape()
            
            // p5.stroke(150)
            p5.strokeWeight(6)
            p5.point(foc, hh)
        }
    }
    
    onMount(() => {
        new p5(sketch1, 'holder-sphere')
        new p5(sketch2, 'holder-coma')
    })
    
</script>

<style lang='less'>
    @import 'styles.less';
    
    #holder-sphere {
        width: 600px;
    }
    
    #holder-coma {
        width: 600px;
    }
</style>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Chromatic Aberration
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Chromatic aberration is an effect of dispersion. 
    
    Lenses refract different wavelengths of light by different amounts. 
    
    This causes a subtle smearing of colours when viewing an image.
</p>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Spherical Aberration
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    A sphere (circle) doesn't reflect parallel light rays though a focus unlike a parabola. 
    
    This is called spherical aberration and it causes distortion when using a spherical mirror. 
    
    The effect is small when using only a small section of the sphere.
</p>

<div
    id='holder-sphere'
    class='holder'
    in:fade={otherFadeIn}
    out:fade={fadeOut}
></div>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Coma
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Parabolas only focus incoming light rays when they are parallel to its principal axis. 
    
    Parallel off-axis light rays don't focus. 
    
    This causes stars to smear and look like they have a cometary tail.
</p>

<div
    id='holder-coma'
    class='holder'
    in:fade={otherFadeIn}
    out:fade={fadeOut}
></div>
