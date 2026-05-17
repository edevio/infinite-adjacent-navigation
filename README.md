# Infinite Adjacent Navigation
A WordPress plugin that adds wraparound next and previous post links. When a visitor reaches the first or last post, navigation loops back to the other end instead of disappearing.

## Note

This was originally written in 2016 and is therefore very old. See Compatibility notes for more info

## Features
- Previous and next links wrap infinitely with no dead ends at either end of the post archive.
- Automatic output: optionally injects navigation after post content with no template changes required.
- Optional middle slot for inserting a custom element (e.g. a back-to-index link) between the two buttons.
- Bootstrap support: optionally applies `btn btn-default` classes to both links.
- Custom CSS classes: add your own classes to the links via the settings page.
- Settings page under **Settings > Infinite Panel** in the WordPress admin.

## Usage
Call the function directly in your theme templates:
```php
echo edev_io\edev_get_infinite_adjacent_navigation();
```

With custom button text and a middle element:
```php
echo edev_io\edev_get_infinite_adjacent_navigation(
    '<a href="/blog">Back to blog</a>',
    'Previous',
    'Next'
);
```

Or enable **Automatically Place** in the settings page to append the navigation after all post content without touching any template files.

## CSS classes
Each link receives the following classes by default:

| Element | Classes |
|---|---|
| Previous link | `edev-post-link edev-previous-link` |
| Next link | `edev-post-link edev-next-link` |
| Wrapper | `edev-navigation` |

The wrapper includes a clearfix. Additional classes can be appended via the settings page.

## Settings
All options are under **Settings > Infinite Panel**.

- **Automatically Place** - appends navigation after post content site-wide.
- **Automatically Position Left and Right** - floats previous left and next right (on by default via inline CSS).
- **CSS Classes** - extra classes added to both link elements.
- **Bootstrap support** - adds `btn btn-default` to both links.

## Requirements
- WordPress 4.0 or later (no declared minimum, but uses standard WP query functions throughout)
- PHP 7.0 or later

## Installation
1. Download or clone this repository.
2. Copy `infinite-adjacent-navigation.php` into `wp-content/plugins/infinite-adjacent-navigation/`.
3. In the WordPress admin go to **Plugins** and activate **Infinite Adjacent Navigation**.
4. Configure options under **Settings > Infinite Panel**, or call `edev_get_infinite_adjacent_navigation()` directly in your templates.

## Compatibility notes
A few things are worth knowing before using it on a current WordPress install.

The core navigation logic still works. `get_adjacent_post()` and `WP_Query` are not deprecated and WordPress has no built-in equivalent for wraparound navigation, so the plugin still does something useful on classic themes.

The settings page uses a pre-Settings API pattern (`options.php` with hidden `page_options` fields). This predates the `register_setting()` / `add_settings_field()` approach. It still functions but is not the recommended pattern.

The Bootstrap option outputs `btn btn-default`. That class was removed in Bootstrap 4, replaced by `btn btn-secondary`. On any Bootstrap 4 or 5 project the button styling will not apply.

On block themes (WordPress 5.9+, Full Site Editing) the plugin's `the_content` filter approach can behave unexpectedly. The Query Loop block handles post navigation at the block level and this plugin is not aware of that. It is not recommended for use with block themes as-is.

For a classic theme with no Bootstrap dependency, the wraparound logic itself is small enough to move into `functions.php` and drop the plugin and settings page entirely.

## License
GPL-3.0-or-later.
