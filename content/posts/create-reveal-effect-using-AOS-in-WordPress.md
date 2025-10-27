---
date: 2025-10-28T07:44:55+08:00
# description: ""
# image: ""
lastmod: 2025-10-28
showTableOfContents: true
tags: ["WordPress",]
title: "Create Reveal Effect Using AOS in WordPress"
type: "post"
---

## Step 1: Install and Setup AOS Library

### Method 1: Using CDN (Recommended)
Add the following code to your theme's `functions.php` file or use a code snippet plugin:

```php
function add_aos_library() {
    // AOS CSS
    wp_enqueue_style('aos-css', 'https://unpkg.com/aos@2.3.1/dist/aos.css');
    
    // AOS JS
    wp_enqueue_script('aos-js', 'https://unpkg.com/aos@2.3.1/dist/aos.js', array(), '2.3.1', true);
    
    // Initialize AOS
    wp_add_inline_script('aos-js', 'AOS.init({
        duration: 1000,
        once: true,
        offset: 100
    });');
}
add_action('wp_enqueue_scripts', 'add_aos_library');
```

### Method 2: Using Bricks Builder Header/Footer Scripts
1. Go to **Bricks > Settings > Custom Code**
2. Add to **Header Scripts**:
```html
<link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
```

3. Add to **Footer Scripts**:
```html
<script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
<script>
  AOS.init({
    duration: 1000,
    once: true,
    offset: 100,
    easing: 'ease-in-out'
  });
</script>
```

## Step 2: Configure AOS Settings

### Basic AOS Configuration Options:
```javascript
AOS.init({
  duration: 1000,        // Animation duration (ms)
  delay: 0,             // Delay before animation starts (ms)
  once: true,           // Animation happens only once
  mirror: false,        // Elements animate out while scrolling past them
  offset: 100,          // Offset (in px) from original trigger point
  easing: 'ease-in-out' // Easing function
});
```

## Step 3: Apply AOS Attributes in Bricks Builder

### Using Custom Attributes
1. Select any element in Bricks Builder
2. Go to **Advanced > Attributes**
3. Add custom attributes:
   - **Name**: `data-aos`
   - **Value**: Choose from available animations (see list below)

### Optional Additional Attributes:
- **data-aos-duration**: `500` (custom duration)
- **data-aos-delay**: `200` (custom delay)
- **data-aos-offset**: `120` (custom offset)
- **data-aos-easing**: `ease-in-sine` (custom easing)

## Step 4: Available AOS Animations

### Fade Animations
- `fade-up`
- `fade-down`
- `fade-left`
- `fade-right`
- `fade-up-left`
- `fade-up-right`
- `fade-down-left`
- `fade-down-right`

### Flip Animations
- `flip-up`
- `flip-down`
- `flip-left`
- `flip-right`

### Slide Animations
- `slide-up`
- `slide-down`
- `slide-left`
- `slide-right`

### Zoom Animations
- `zoom-in`
- `zoom-in-up`
- `zoom-in-down`
- `zoom-in-left`
- `zoom-in-right`
- `zoom-out`
- `zoom-out-up`
- `zoom-out-down`
- `zoom-out-left`
- `zoom-out-right`

## Step 5: Practical Examples

### Example 1: Hero Section with Staggered Animations
```
Headline: data-aos="fade-up" data-aos-delay="0"
Subtitle: data-aos="fade-up" data-aos-delay="200"
Button: data-aos="fade-up" data-aos-delay="400"
```

### Example 2: Card Grid with Sequential Reveals
```
Card 1: data-aos="fade-up" data-aos-delay="0"
Card 2: data-aos="fade-up" data-aos-delay="100"
Card 3: data-aos="fade-up" data-aos-delay="200"
Card 4: data-aos="fade-up" data-aos-delay="300"
```

### Example 3: Image Gallery with Zoom Effects
```
Image 1: data-aos="zoom-in" data-aos-duration="800"
Image 2: data-aos="zoom-in" data-aos-duration="800" data-aos-delay="100"
Image 3: data-aos="zoom-in" data-aos-duration="800" data-aos-delay="200"
```

## Step 6: Best Practices

### Performance Optimization
- Use `once: true` to prevent repeated animations
- Limit the number of animated elements per page
- Use appropriate offsets to trigger animations at the right time

### Design Tips
- Keep animations subtle and purposeful
- Use consistent easing and duration across similar elements
- Consider your audience and device performance
- Test on mobile devices for smooth performance

### Common Element Combinations
- **Headlines**: `fade-up` with 0ms delay
- **Paragraphs**: `fade-up` with 200ms delay
- **Images**: `zoom-in` or `fade-left/right`
- **Cards/Boxes**: `fade-up` with staggered delays
- **Buttons**: `fade-up` with slight delay after text

## Step 7: Advanced Customization

### Custom CSS for Enhanced Effects
Add this to your theme's style.css or Bricks custom CSS:

```css
/* Custom AOS modifications */
[data-aos] {
  transition-property: transform, opacity;
}

/* Custom reveal effect */
.custom-reveal {
  overflow: hidden;
}

.custom-reveal [data-aos] {
  transform: translateY(50px);
  opacity: 0;
}

.custom-reveal [data-aos].aos-animate {
  transform: translateY(0);
  opacity: 1;
}
```

### Refresh AOS After Dynamic Content
If you're loading content dynamically, refresh AOS:
```javascript
AOS.refresh();
```

## Step 8: Troubleshooting

### Common Issues:
1. **Animations not working**: Check if AOS library is loaded properly
2. **Animations too fast/slow**: Adjust duration values
3. **Animations triggering too early/late**: Modify offset values
4. **Mobile performance issues**: Reduce number of animations or disable on mobile

### Debug Mode:
Add this to temporarily see AOS triggers:
```javascript
AOS.init({
  duration: 1000,
  once: true,
  offset: 100,
  disable: false, // Set to 'mobile' to disable on mobile
  startEvent: 'DOMContentLoaded'
});
```

## Conclusion

AOS provides an easy way to add professional reveal effects to your Bricks Builder site. Start with simple fade-up animations and gradually experiment with more complex combinations. Always test on different devices and screen sizes to ensure optimal user experience.