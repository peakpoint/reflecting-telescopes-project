<script>
    import { fade } from 'svelte/transition'
    import { onMount } from 'svelte'
    
    export let scoped
    const d = scoped.duration
    
    let fadeOut = {duration: d}
    let fadeIn = {duration: d, delay: d}
    let otherFadeIn = {duration: d, delay: d + 100}
    
    let bgCol = window.getComputedStyle(document.body).getPropertyValue('background-color')
    
    let sketch3 = p5 => {
        let vertices = [], mag = 120, off = 1, foc, calc, hh
        
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
                p5.line(...r, ...f)
            }
            
            p5.stroke(150)
            p5.beginShape()
            for (let i in vertices) p5.vertex(vertices[i], i)
            p5.endShape()
            
            // p5.stroke(150)
            p5.strokeWeight(6)
            p5.point(foc, hh)
            
            // p5.strokeWeight(4)
            // if (coll.x) p5.point(coll.x, coll.y)
        }
    }
    
    onMount(() => {
        new p5(sketch3, 'holder-parabola')
    })
    
</script>

<style lang='less'>
    @import 'styles.less';
    
    #holder-parabola {
        width: 600px;
    }
</style>

<h2 in:fade={fadeIn} out:fade={fadeOut}>
    Conics
</h2>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Conics are a family of curves that are the possible intersections of a plane with a (double) cone. Click <a href='https://www.geogebra.org/t/conic-sections' target='_blank'>here</a> to experiment with conic sections.
</p>

<h3 in:fade={fadeIn} out:fade={fadeOut} id='parabola'>
    Parabolas
</h3>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    There are many ways of defining a parabola. One common example is graphing the equation <em>y = x<sup>2</sup></em>. 
    
    The useful property of a parabola is that incoming light rays parallel to it's princpal axis always reflect though a point called the parabola's focus.
    
    All parabolas are <a href='https://www.youtube.com/watch?v=hoh4TmPzu1w' target='_blank'>self similar</a>.
</p>

<div
    id='holder-parabola'
    class='holder'
    in:fade={otherFadeIn}
    out:fade={fadeOut}
></div>

<h3 in:fade={fadeIn} out:fade={fadeOut} id='ellipse'>
    Ellipses
</h3>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    There are many ways of defining an ellipse. One way is to 'stretch' a circle.
    
    Another way to create an ellipse is to chose two points called the <em>foci</em> (plural of focus) and find all points with a constant sum of distances to them.
    
    This can be modeled using two thumbtacks and a loop of string.
</p>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    The useful property of ellipses is that incoming light rays going though a focus will always reflect though the other <a href='https://www.youtube.com/watch?v=4KHCuXN2F3I' target='_blank'>focus</a>.
    
    A parabola may be considered an ellipse with a focus at infinity.
</p>

<h3 in:fade={fadeIn} out:fade={fadeOut} id='hyperbola'>
    Hyperbolas
</h3>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    An example of a hyperbola is the graph of <em>y = <sup>1</sup>&frasl;<sub>x</sub></em>. Hyperbolas have two <em>foci</em>. 
    
    A way to create a hyperbola is to chose two <em>foci</em> and find all points with a constant difference of distances to them.
    
    Like an ellipse, an incoming light ray going though a focus will always reflect though the other focus.
    
    A parabola may be considered a hyperbola with a focus at infinity.
</p>

<h3 in:fade={fadeIn} out:fade={fadeOut}>
    Circles
</h3>

<p in:fade={otherFadeIn} out:fade={fadeOut}>
    Surprise. A circle may be considered an ellipse with both <em>foci</em> being the same point.
</p>
