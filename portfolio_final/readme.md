## My Process

I started by looking at other portfolios, and decided to format my work on one long page with different sections that the user could jump to.
For this update, I decided to add elevator scrolling, a starfield effect, a magnetic hover effect over all images, a contact form, and various aesthetic improvements to the website.

---

## Code Highlights

### Starfield Canvas Effect  
Creating the starfield was particularly challenging and took a lot of trial and error. 
I started by generating two arrays: sparkle stars and circle stars—with randomized positions, speeds, sizes, and alpha values.
In the `update()` loop, each star moves downward and wraps to the top when it passes the bottom edge.
Sparkle shapes are drawn by stroking vertical and horizontal lines, while circle shapes use `ctx.arc()`. 
This taught me a lot about the Canvas API and animation loops.


function drawSparkle(x, y, size, alpha) {
  ctx.save();
  ctx.translate(x, y);
  ctx.globalAlpha = alpha;
  ctx.strokeStyle = "white";
  ctx.lineWidth = 1.2;
  // vertical line
  ctx.beginPath();
  ctx.moveTo(0, -size*2);
  ctx.lineTo(0, size*2);
  ctx.stroke();
  // horizontal line
  ctx.beginPath();
  ctx.moveTo(-size*2, 0);
  ctx.lineTo(size*2, 0);
  ctx.stroke();
  ctx.restore();
}


### GSAP Scroll & Magnetic Hover

I used GSAP’s `ScrollToPlugin` to animate anchor clicks with easing. 
For the magnetic hover, I captured the image’s bounding box on `mouseenter` and then in `mousemove` tween the image `x`/`y` to a fraction of the cursor offset:


img.addEventListener("mousemove", e => {
  const offsetX = e.clientX - bounds.left - bounds.width/2;
  const offsetY = e.clientY - bounds.top - bounds.height/2;
  gsap.to(img, { x: offsetX*0.1, y: offsetY*0.1, duration: 0.3, ease: "power2.out" });
});


---

## What I Learned

* HTML Canvas API and animation loops
* GSAP plugins (`ScrollToPlugin`, tweening complex properties)
* Responsive design/designing across screen sizes

---

## Next Steps

If I had more time and tools, I would:

1. Images fade in on scroll. I tried to implement it in my code initially, but I ended up breaking it somehow.
2. Parallax effect scrolling with background changes.
3. Hooking up contact form to a database. I didn't find it necessary since I'm not hosting the website anywhere.
