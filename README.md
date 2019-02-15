# Sitegeist.Lazybones
## Image Lazy Loading based on Sitegeist.Kaleidoscope (Responsive Images for Neos - with Atomic.Fusion & Monocle in mind)

This package implements Lazy Loading for Responsive Images from the Sitegeist.Kaleidoscope package.

This is implemented by rendering the `src`, `srcset` and `sizes` attributes as `data-src`, `data-srcset`
and `data-sizes`. The img- or pPicture-tag is then marked with the class `lazyload` to
be replaced via js once the image comes into view. If you like you can render a very lowres
src-attribute or leave the src attribute empty (default).

### Authors & Sponsors

* Martin Ficzel - ficzel@sitegeist.de

*The development and the public-releases of this package is generously sponsored
by our employer http://www.sitegeist.de.*

## Installation

Sitegeist.Lazybones is available via packagist run `composer require sitegeist/lazybones`.
We use semantic-versioning so every breaking change will increase the major-version number.

## Usage

### LazyloadJS

To enable lazy loading you have to integrate a script that will detect the `lazyload` class
and convert `data-src`, `data-srcset` and `data-sizes` to the correct attributes once they come
into view.

*This package includes the `lazysizes` library from https://github.com/aFarkas/lazysizes
but it is probably better to include the js into your own fe-build.*

To include the bundled js you can use the following snippet:

```
lazyloadJS = Neos.Fusion:Tag {
    tagName = 'script'
    attributes.async = true
    attributes.src = Neos.Fusion:ResourceUri {
        path = 'resource://Sitegeist.Lazybones/Public/JavaScript/lazysizes.min.js'
    }
}
```

### `Sitegeist.Lazybones:Image`

Render an img-tag with optional srcset based on sizes or resolutions.

This prototype is a drop in replacement for `Sitegeist.Kaleidoscope:Image` with
optional props to control the lazy loading.

See: https://github.com/sitegeist/Sitegeist.Kaleidoscope#sitegeistkaleidoscopeimage

Props:
- `lazy`: Enable lazy loading (boolean, default true).
   Use this to control whether contents should be lazy loaded or not. If this value
   is false the `Sitegeist.Kaleidoscope:Image` is used directly.
- `lazyClass`: The class to attach to the img-tags (string, default "lazyload").
   Has to fit your js-library.
- `lazyWidth`: The width of the thumbnail src that is loaded first (int, default null).
   If this value is null no initial src is rendered to avoid any unneeded http-requests.

Props from `Sitegeist.Kaleidoscope:Image`:
- `imageSource`: the imageSource to render
- `srcset`: media descriptors like '1.5x' or '600w' of the default image (string ot array)
- `sizes`: sizes attribute of the default image (string or array)
- `alt`: alt-attribute for the img tag
- `title`: title attribute for the img tag
- `class`: class attribute for the img tag

### `Sitegeist.Lazybones:Picture`

Render apicture`-tag with various sources.

This prototype is a drop in replacement for `Sitegeist.Kaleidoscope:Picture` with
optional props to control the lazy loading.

See: https://github.com/sitegeist/Sitegeist.Kaleidoscope#sitegeistkaleidoscopepicture

Props:
- `lazy`: Enable lazy loading (boolean, default true).
   Use this to control whether contents should be lazy loaded or not. If this value
   is false the `Sitegeist.Kaleidoscope:Picture` is used directly.
- `lazyClass`: The class to attach to the img-tags (string, default "lazyload").
   Has to fit your js-library.
- `lazyWidth`: The width of the thumbnail-src that is loaded first (int, default null).
   If this value is null no initial src is rendered to avoid any unneeded http-requests.

Props from `Sitegeist.Kaleidoscope:Picture`:
- `imageSource`: the imageSource to render
- `sources`: an array of source definitions that supports the following keys
   - `media`: the media query of this source
   - `imageSource`: alternate image-source for art direction purpose
   - `srcset`: media descriptors like '1.5x' or '600w' (string ot array)
   - `sizes`: sizes attribute (string ot array)
- `srcset`: media descriptors like '1.5x' or '600w' of the default image (string ot array)
- `sizes`: sizes attribute of the default image (string ot array)
- `alt`: alt-attribute for the picture tag
- `title`: title attribute for the picture tag
- `class`: class attribute for the picture tag

## Contribution

We will gladly accept contributions. Please send us pull requests.
