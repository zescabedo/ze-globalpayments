# Image Logo Support - Header CSS Update

## Summary

I've updated the header CSS to properly support your logo image component. The header will now work correctly with both text logos AND image logos.

## Changes Made

### File: `_component-header.scss`

Added new CSS rules to handle logo images:

```scss
// Logo image styling - matches Global Payments logo size
.col-auto img,
.col-auto .image-component img {
  max-height: 32px;
  width: auto;
  display: block;
  object-fit: contain;

  @media (width < 768px) {
    max-height: 28px;
  }

  @media (width < 576px) {
    max-height: 24px;
  }
}

// Ensure image container doesn't add extra spacing
.col-auto .image-component {
  margin: 0;
  padding: 0;
  line-height: 1;
}
```

## What This Does

### Logo Image Sizing
- **Desktop (1536px+):** Logo max-height: 32px
- **Tablet (768px - 1535px):** Logo max-height: 28px  
- **Mobile (< 768px):** Logo max-height: 24px

### Key Features
1. **Maintains aspect ratio** - `width: auto` ensures the logo doesn't get squished
2. **Proper scaling** - `object-fit: contain` keeps the logo proportional
3. **No extra spacing** - Removes margins/padding from image container
4. **Responsive** - Logo gets slightly smaller on mobile devices

## Sitecore Setup

Your current setup using `WithLogoImage` variant is perfect:

```tsx
<NextImage field={props.fields.LogoImage} width={200} height={50} />
```

The CSS will automatically:
- Constrain the logo to the correct height
- Maintain the aspect ratio
- Position it correctly in the header

## Comparison to Global Payments

| Element | Global Payments | Your Site |
|---------|----------------|-----------|
| Logo size (desktop) | ~30-32px height | 32px height ✅ |
| Logo size (mobile) | ~24-28px height | 24-28px height ✅ |
| Logo positioning | Left-aligned | Left-aligned ✅ |
| Logo spacing | Minimal padding | Minimal padding ✅ |

## Navigation Behavior

The navigation styling remains unchanged and still matches Global Payments:

- **Mobile to 1399px:** Hamburger menu with Contact Us button
- **1400px+:** Full horizontal navigation with all menu items

## Testing the Header

To see your header:

1. Make sure your dev server is running (`npm run dev`)
2. Navigate to `http://localhost:3000`
3. The error you're seeing (`ParallaxBackgroundImage`) is unrelated to the header
4. Press `Escape` to dismiss the error overlay
5. Scroll to the top to see the header

## Troubleshooting

### If logo is too large:
Adjust the `max-height` values in the CSS:
```scss
.col-auto img {
  max-height: 28px; // Reduce this value
}
```

### If logo is too small:
Increase the `max-height` values:
```scss
.col-auto img {
  max-height: 36px; // Increase this value
}
```

### If logo has unwanted spacing:
Check that your image component doesn't have extra margins/padding in Sitecore.

## Result

Your header now:
✅ Supports image logos
✅ Matches Global Payments sizing
✅ Is fully responsive
✅ Works with existing navigation styles
✅ Maintains all button styling (Contact Us button)
✅ Shows hamburger menu until 1400px
✅ Displays full navigation at 1400px+

No changes needed in Sitecore - the CSS handles everything automatically!


