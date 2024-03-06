# Javascrippets
## _JavaScript snippets for various website functionalities._

## Scroll to Top Button

_"Scroll to Top" button that appears when the user scrolls down the page. Clicking this button smoothly scrolls the page back to the top. This code dynamically creates a button and adds it to the page. The button becomes visible when the user scrolls down the page and, upon clicking, smoothly scrolls back to the top. You can customize the button's styles as per your website's design._


```javascript
// JavaScript for Scroll to Top Button

    function scrollToTop() {
    window.scrollTo({ top: 0, behavior: 'smooth' });
    }

// Create a scroll to top button dynamically

  var scrollToTopButton = document.createElement('button');
    scrollToTopButton.textContent = 'Scroll to Top';
    scrollToTopButton.style.position = 'fixed';
    scrollToTopButton.style.bottom = '20px';
    scrollToTopButton.style.right = '20px';
    scrollToTopButton.style.display = 'none';
  
// Show the button when scrolling down
window.onscroll = function() {
    if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
        scrollToTopButton.style.display = 'block';
    } else {
        scrollToTopButton.style.display = 'none';
    }
};

// Add click event to the button
scrollToTopButton.addEventListener('click', scrollToTop);

// Append the button to the body
document.body.appendChild(scrollToTopButton);
```

## Accordion Menu

_accordion menu, ideal for FAQs or similar content._

```javascript

// JavaScript for Accordion Menu

var acc = document.getElementsByClassName('accordion');
var i;

for (i = 0; i < acc.length; i++) {
    acc[i].addEventListener('click', function() {
        this.classList.toggle('active');
        var panel = this.nextElementSibling;
        if (panel.style.display === 'block') {
            panel.style.display = 'none';
        } else {
            panel.style.display = 'block';
        }
    });
}
```
```html
<button class="accordion">Section 1</button>
<div class="panel">
    <p>Content for Section 1.</p>
</div>

<button class="accordion">Section 2</button>
<div class="panel">
    <p>Content for Section 2.</p>
</div>

<!-- Repeat for more sections -->
```

## Lazy Load

_This JavaScript snippet enables lazy loading of images, which means images will load as they come into view in the browser window, improving page load performance. The data-src attribute holds the path to the image, which gets loaded only when the image is about to enter the viewport. For older browsers without IntersectionObserver support, the images will load normally._

```javascript

// JavaScript for Lazy Loading Images

document.addEventListener('DOMContentLoaded', function() {
    var lazyImages = [].slice.call(document.querySelectorAll('img.lazy'));

    if ('IntersectionObserver' in window) {
        let lazyImageObserver = new IntersectionObserver(function(entries, observer) {
            entries.forEach(function(entry) {
                if (entry.isIntersecting) {
                    let lazyImage = entry.target;
                    lazyImage.src = lazyImage.dataset.src;
                    lazyImage.classList.remove('lazy');
                    lazyImageObserver.unobserve(lazyImage);
                }
            });
        });

        lazyImages.forEach(function(lazyImage) {
            lazyImageObserver.observe(lazyImage);
        });
    } else {
        // Fallback for browsers without IntersectionObserver support
        lazyImages.forEach(function(lazyImage) {
            lazyImage.src = lazyImage.dataset.src;
            lazyImage.classList.remove('lazy');
        });
    }
});
```
```html
<img class="lazy" data-src="path/to/image.jpg" alt="description">
```

## Parallax

This JavaScript snippet creates a parallax scrolling effect, where background images move at a different speed than the foreground content as you scroll down the page. Each element with the class parallax will have the parallax effect applied. The data-parallax-speed attribute determines the speed of the background's movement relative to the scroll speed.

```javascript
// JavaScript for Parallax Scrolling Effect

function parallaxEffect() {
    var parallax = document.querySelectorAll('.parallax');

    parallax.forEach(function(element) {
        var speed = element.getAttribute('data-parallax-speed');
        var yPos = -(window.scrollY * speed);
        var coords = '50% ' + yPos + 'px';

        element.style.backgroundPosition = coords;
    });
}

window.addEventListener('scroll', parallaxEffect);
```
```html
<div class="parallax" data-parallax-speed="0.5" style="background-image: url('image-path.jpg');">
    <!-- Content here -->
</div>
```







