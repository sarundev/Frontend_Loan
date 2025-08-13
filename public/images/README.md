# Carousel Images

To use your own images in the HeroBanner carousel, place your image files in this directory with the following names:

## Required Image Files:

- `financial-solutions.jpg` - For the "Financial Solutions" slide
- `quick-loans.jpg` - For the "Quick Loans" slide
- `low-rates.jpg` - For the "Low Interest Rates" slide
- `flexible-terms.jpg` - For the "Flexible Terms" slide

## Image Specifications:

- **Recommended size**: 800x400 pixels (2:1 aspect ratio)
- **Format**: JPG, PNG, or WebP
- **File size**: Keep under 500KB for optimal loading

## Usage:

1. Add your image files to this directory with the exact names listed above
2. The carousel will automatically use your images
3. If images are not found, the component will fall back to gradient backgrounds

## Alternative:

You can also disable images and use gradients only by setting `useImages: false` when using the HeroBanner component:

```vue
<HeroBanner :useImages="false" />
```
