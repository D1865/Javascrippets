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

_This JavaScript snippet creates a parallax scrolling effect, where background images move at a different speed than the foreground content as you scroll down the page. Each element with the class parallax will have the parallax effect applied. The data-parallax-speed attribute determines the speed of the background's movement relative to the scroll speed._

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

## Custom Post Type Slider

_For creating a slider, useful for showcasing custom post types like testimonials or portfolio items. To complement this JavaScript, you need an HTML structure with elements for the slides and navigation controls, like next/previous buttons and dots for slide indication._

```javascript

// JavaScript for Custom Post Type Slider

var slideIndex = 1;
showSlides(slideIndex);

// Next/previous controls
function plusSlides(n) {
  showSlides(slideIndex += n);
}

// Thumbnail image controls
function currentSlide(n) {
  showSlides(slideIndex = n);
}

function showSlides(n) {
  var i;
  var slides = document.getElementsByClassName('mySlides');
  var dots = document.getElementsByClassName('dot');
  if (n > slides.length) {slideIndex = 1}
  if (n < 1) {slideIndex = slides.length}
  for (i = 0; i < slides.length; i++) {
      slides[i].style.display = 'none';
  }
  for (i = 0; i < dots.length; i++) {
      dots[i].className = dots[i].className.replace(' active', '');
  }
  slides[slideIndex-1].style.display = 'block';
  dots[slideIndex-1].className += ' active';
}
```


## WordPress AJAX Search

_A live search feature for WordPress sites, where search results are dynamically updated as the user types in the search input. This script sends the user's search term to a WordPress AJAX handler `(typically defined in your theme's functions.php)`. The server then processes the search and returns the results, which are dynamically displayed. For full functionality, set up the corresponding AJAX handler in your WordPress theme and ensure you have a search input and a container to display the results._


```javascript
// JavaScript for Custom WordPress AJAX Search

function performSearch() {
    var searchTerm = document.getElementById('searchInput').value;
    var resultsContainer = document.getElementById('searchResults');
    var ajaxurl = '/wp-admin/admin-ajax.php';

    var data = {
        'action': 'custom_search', // The action hook in functions.php
        'search_term': searchTerm
    };

    fetch(ajaxurl, {
        method: 'POST',
        body: JSON.stringify(data),
        headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
        }
    })
    .then(response => response.json())
    .then(data => {
        resultsContainer.innerHTML = '';
        data.forEach(item => {
            resultsContainer.innerHTML += '<li>' + item.title + '</li>';
        });
    });
}

// Attach this function to the search input's oninput event
// Example: <input type="text" id="searchInput" oninput="performSearch()">
```

# (RBAC) 
## Role Based Content Display 

_This JavaScript snippet is designed to display different content on a WordPress site based on the user's role, like showing premium content only to certain user roles. To use this script, you need to pass the user role from PHP to JavaScript. This can be done using `wp_localize_script()` in WordPress, which allows you to create a global JavaScript variable containing the user role. The script then uses this information to display the appropriate content._


```javascript
// JavaScript for User Role Based Content Display in WordPress

// This example assumes you have a way to pass the user role from PHP to JavaScript
// For instance, using wp_localize_script in WordPress to create a 'userRole' variable

function displayContentBasedOnRole() {
    var userRole = window.userRole; // Example: 'administrator', 'subscriber', etc.
    var premiumContent = document.getElementById('premiumContent');
    var regularContent = document.getElementById('regularContent');

    if (userRole === 'administrator' or userRole === 'subscriber') {
        premiumContent.style.display = 'block';
        regularContent.style.display = 'none';
    } else {
        premiumContent.style.display = 'none';
        regularContent.style.display = 'block';
    }
}

// Run this function on page load
window.onload = displayContentBasedOnRole;
```

## Dynamic Sidebar Content 

_Changes the content of the sidebar in a WordPress site based on the current post or page. This code checks the current page's URL and updates the sidebar content accordingly. For instance, if the user is viewing a news category page, the sidebar will display news-related content. This approach enhances the relevance and user engagement of sidebar content. Ensure you have an element with the ID `sidebar` in your WordPress theme for this script to work effectively.


```javascript
// JavaScript for Dynamic Sidebar Content in WordPress

function updateSidebarContent() {
    var currentPage = window.location.pathname;
    var sidebar = document.getElementById('sidebar');

    // Example: Update sidebar based on the current page
    if (currentPage.includes('/category/news')) {
        sidebar.innerHTML = '<p>News related content here</p>';
    } else if (currentPage.includes('/category/sports')) {
        sidebar.innerHTML = '<p>Sports related content here</p>';
    }
    // Add more conditions as needed
}

// Run this function when the page loads
window.onload = updateSidebarContent;
```

## Shortcode Creator for WordPress

_Conceptual example for creating shortcodes in WordPress. Typically, shortcode functionality is handled server-side in PHP, but here's a basic idea of how it might be structured. Provides a basic structure for a custom shortcode function. In actual WordPress usage, you would define this functionality in PHP within your theme's functions.php file or a custom plugin. The shortcode can then be used in posts or pages to insert custom content or functionality. Since shortcode functionality is primarily a server-side feature in WordPress, remember to implement the actual logic in PHP._

```javascript
// JavaScript for Shortcode Creator in WordPress
// Note: This is a conceptual example as shortcodes are typically handled in PHP on the server side.

function myCustomShortcode(attrs) {
    // Example shortcode functionality
    return '<div class="my-custom-class">' + attrs.content + '</div>';
}

// Usage in WordPress PHP: add_shortcode('myshortcode', 'myCustomShortcode');
// Usage in posts: [myshortcode]Your content here[/myshortcode]
```

```php
<?php
// Add the following code to your theme's functions.php file or a custom plugin.

// Shortcode handler function
function my_custom_shortcode($atts = [], $content = null) {
    // Normalize attribute keys, lowercase
    $atts = array_change_key_case((array)$atts, CASE_LOWER);

    // Define default attributes and override with user attributes
    $atts = shortcode_atts([
        'class' => 'my-custom-class', // Default class if none provided
    ], $atts);

    // Enclose content with a div and apply class from attributes
    $output = '<div class="' . esc_attr($atts['class']) . '">' . do_shortcode($content) . '</div>';

    return $output;
}

// Register the shortcode with WordPress
add_shortcode('myshortcode', 'my_custom_shortcode');

?>
```














