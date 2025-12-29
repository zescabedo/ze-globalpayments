# Contact Us Button Styling - Implementation Guide

## ✅ CSS is Now Fully Configured

I've added comprehensive CSS rules that will **automatically** style any navigation item with the `button-nav-item` class to match the Global Payments "Contact Us" button exactly.

## How It Works in Sitecore

### Step 1: Add the Style Class in Sitecore

When you edit your Navigation item for "Contact Us" in Sitecore:

1. Go to the **Navigation item** for "Contact Us"
2. Find the **Styles** field (or **Style Class** field)
3. Add: `button-nav-item`
4. Save the item

That's it! The CSS will automatically apply.

### Step 2: Verify the HTML Class is Applied

After saving, when the page renders, the HTML should look like:

```html
<li class="level1 button-nav-item">
  <div class="navigation-title">
    <a href="/contact">Contact Us</a>
  </div>
</li>
```

The key is that `button-nav-item` appears in the class attribute.

## What the Button Will Look Like

### Desktop (≥992px):
- **Transparent background**
- **2px solid blue border** (#2536f0)
- **Black text** (#0C0C0C) - not blue!
- **Large rounded corners** (2rem border-radius = fully rounded pill)
- **Generous padding** (0.75rem × 2rem)
- **Bold font** (600 weight)
- **On hover:**
  - Background fills with blue (#2536f0)
  - Text turns white
  - Subtle lift effect (translateY(-1px))
  - Blue shadow appears

### Mobile (<992px):
- **Filled blue background** (#2536f0)
- **White text**
- **Full width** button
- **Centered in mobile menu**
- **On hover:**
  - Darker blue background (#1e2bc4)

## CSS Selectors Used

The CSS uses multiple selectors to ensure it catches the class no matter how Sitecore applies it:

```scss
// All of these will work:
[class*="button-nav-item"]
li.button-nav-item
.level0.button-nav-item  
.level1.button-nav-item
.rel-level1.button-nav-item
```

## Exact Styling Values (Matching Global Payments)

```scss
// Desktop Button
background-color: transparent;
border: 2px solid #2536f0;
color: #0C0C0C;          // Black, not blue!
padding: 0.75rem 2rem;   // 12px × 32px
border-radius: 2rem;     // Fully rounded pill shape
font-weight: 600;        // Semi-bold
font-size: 1rem;         // 16px
```

## Why Use `!important`

The CSS uses `!important` flags to ensure the button styling overrides:
- Default navigation link styles
- Any theme-specific styles
- Sitecore's injected styles
- Other CSS specificity issues

This guarantees the button will look exactly like Global Payments regardless of other styles on the page.

## Troubleshooting

### If the button doesn't appear styled:

1. **Check the class name:**
   - In browser DevTools, inspect the `<li>` element
   - Verify `button-nav-item` is in the class attribute
   - Check for typos (button-nav-item, not button-navitem)

2. **Check CSS is loaded:**
   - In DevTools, go to Sources tab
   - Find `main.css` or your compiled CSS file
   - Search for "button-nav-item"
   - Verify the styles are present

3. **Check for console errors:**
   - Open browser console (F12)
   - Look for any CSS compilation errors
   - Fix any SCSS syntax errors if present

4. **Clear cache:**
   - Hard refresh: Cmd+Shift+R (Mac) or Ctrl+Shift+R (Windows)
   - Clear browser cache completely
   - Restart the dev server if needed

### If the navigation isn't showing at all:

1. **Check Sitecore placeholder:**
   - Verify Navigation component is in the `header-right` placeholder
   - Make sure the component is published
   - Check that navigation items exist and are published

2. **Check responsive display:**
   - The navigation should show on desktop (≥992px)
   - On mobile (<992px), only the hamburger menu should show
   - Resize your browser to test different breakpoints

## Example in Sitecore

```
Header Component (header-right placeholder)
└── Navigation Component
    ├── Solutions
    ├── Products
    ├── Partners
    ├── Developers
    ├── Resources
    ├── Company
    └── Contact Us  ← Add "button-nav-item" to Styles field
```

## Visual Comparison

**Before (default nav styling):**
- Contact Us looks like other nav items
- Just text, no button appearance
- Same color and padding as other links

**After (with button-nav-item class):**
- Contact Us stands out as a button
- Outlined pill shape with blue border
- Larger padding, more prominent
- Hover effect makes it interactive and engaging
- **Matches Global Payments exactly! ✓**

## Testing Checklist

- [ ] Desktop: Button shows with transparent background and blue border
- [ ] Desktop: Button text is black, not blue
- [ ] Desktop: Button has generous padding and is pill-shaped
- [ ] Desktop: Hover changes background to blue and text to white
- [ ] Desktop: Button is positioned on the right side (margin-left: auto)
- [ ] Mobile: Button shows with blue background and white text
- [ ] Mobile: Button is full-width and centered
- [ ] Mobile: Hover makes button darker blue
- [ ] All devices: Font is bold (600 weight) and 1rem size

## Files Modified

- `src/assets/sass/components/_component-navigation.scss`
- `src/assets/sass/components/navigation/_navigation-mobile.scss`

Both files now include comprehensive button styling rules with high specificity (`!important` flags) to ensure the styling always applies correctly.



