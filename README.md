# Elementor Form Date Format Changer

A simple JavaScript solution to change the date format in Elementor forms from YYYY-MM-DD to DD/MM/YYYY.

## Problem

By default, Elementor Pro forms use the YYYY-MM-DD date format for date fields, which may not be the preferred format in many regions where DD/MM/YYYY is the standard.

## Solution

This lightweight script modifies the Flatpickr date picker used by Elementor to display and submit dates in the DD/MM/YYYY format.

## Installation

### Method 1: Using Elementor Custom Code

1. In your WordPress dashboard, go to **Elementor > Custom Code**
2. Click **Add New Code**
3. Give your custom code a name (e.g., "Elementor Form Date Format")
4. Set the location to `<head>`
5. Set the priority to 1
6. Paste the following code:

```javascript
<script>
window.addEventListener('DOMContentLoaded', function() {
   jQuery(document).ready(function($){
      setTimeout(function(){
         $('.flatpickr-input').each(function(){ 
            flatpickr($(this)[0]).set('dateFormat', 'd/m/Y');
         }); 
      }, 1000);
   });
});
</script>
```

7. Click **Publish**

### Method 2: Add to Theme's functions.php

Add the following code to your theme's `functions.php` file:

```php
// Change Elementor date format to DD/MM/YYYY
function elementor_date_format_changer() {
    ?>
    <script>
    window.addEventListener('DOMContentLoaded', function() {
       jQuery(document).ready(function($){
          setTimeout(function(){
             $('.flatpickr-input').each(function(){ 
                flatpickr($(this)[0]).set('dateFormat', 'd/m/Y');
             }); 
          }, 1000);
       });
    });
    </script>
    <?php
}
add_action('wp_head', 'elementor_date_format_changer');
```

### Method 3: Using a Code Snippets Plugin

1. Install and activate a code snippets plugin like [Code Snippets](https://wordpress.org/plugins/code-snippets/)
2. Create a new HTML snippet
3. Paste the script code above
4. Set it to load in the header
5. Save and activate the snippet

## How It Works

1. The script waits for the DOM content to be fully loaded
2. It then waits for jQuery to be ready
3. It sets a 1-second timeout to ensure all Elementor form elements are properly initialized
4. It finds all elements with the class 'flatpickr-input' (used by Elementor's date inputs)
5. For each date input, it initializes the Flatpickr date picker and sets the date format to 'd/m/Y' (DD/MM/YYYY)

## Customization

### Different Date Format

To use a different date format, change the `'d/m/Y'` part:

- `'d-m-Y'` for DD-MM-YYYY (with hyphens)
- `'d.m.Y'` for DD.MM.YYYY (with periods)
- `'m/d/Y'` for MM/DD/YYYY (US format)

### Adjusting the Timeout

If your site loads slowly and the script isn't working, you may need to increase the timeout value:

```javascript
setTimeout(function(){ ... }, 2000); // 2 seconds instead of 1
```

## Troubleshooting

### Date Format Not Changing

1. Check if the script is loading correctly (no JavaScript errors in the browser console)
2. Verify that jQuery is loaded on your site
3. Check if your Elementor form's date fields use the 'flatpickr-input' class (inspect the page)
4. Try increasing the timeout value
5. Clear your browser cache and any caching plugins

## Compatibility

- Works with Elementor Pro forms
- Compatible with WordPress 5.0+
- Compatible with Elementor Pro 3.0+

## License

This solution is provided under the MIT License. Feel free to use, modify, and distribute as needed.

## Credits

This solution works by leveraging the Flatpickr library used by Elementor Pro for its date inputs.
