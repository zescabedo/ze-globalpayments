# Header Breakpoints - Matching Global Payments Exactly

## ✅ Updated to Match Global Payments at All Screen Sizes

After analyzing globalpayments.com at multiple breakpoints, I've updated the header to match their exact behavior.

## Breakpoint Behavior

### 📱 Mobile: < 768px (e.g., 375px)

**What Shows:**
- Logo (left)
- Hamburger menu icon (right)

**What's Hidden:**
- All navigation items (in mobile drawer)
- Contact Us button (in mobile drawer)
- Utility nav

**On Hamburger Click:**
- Side drawer opens from right
- Shows all nav items stacked vertically
- Contact Us appears as full-width blue button at bottom

---

### 📱 Tablet Portrait: 768px - 1399px (e.g., 768px)

**What Shows:**
- Logo (left)
- **Contact Us button** (outlined pill, right)
- Hamburger menu icon (right)

**What's Hidden:**
- Navigation menu items (Solutions, Products, etc.)
- Search icon
- Utility nav

**Key Feature:**
- Contact Us button appears **outside** the mobile menu
- Hamburger menu still used for main navigation

---

### 💻 Small Desktop: 1024px - 1399px (e.g., 1024px, 1280px)

**What Shows:**
- Logo (left)
- **Contact Us button** (outlined pill, right)
- Hamburger menu icon (right)

**What's Hidden:**
- Navigation menu items (Solutions, Products, etc.)
- Search icon
- Utility nav

**Same as Tablet:**
- Navigation items still in hamburger menu
- Contact Us button visible alongside hamburger
- This matches Global Payments' design decision to keep hamburger menu up to 1400px

---

### 🖥️ Large Desktop: 1400px - 1535px (e.g., 1440px)

**What Shows:**
- Logo (left)
- **Full navigation menu** (Solutions, Products, Partners, Developers, Insights, Company)
- Search icon (optional)
- **Contact Us button** (outlined pill)
- Utility nav may appear

**What's Hidden:**
- Hamburger menu icon

**Key Change:**
- This is where the full horizontal navigation finally appears
- All menu items visible in header
- No more hamburger menu

---

### 🖥️ Extra Large Desktop: 1536px+ 

**What Shows:**
- **Utility Nav** at very top (Careers, Developers, Log in) - right aligned
- Logo (left)
- **Full navigation menu** (Solutions, Products, Partners, Developers, Insights, Company)
- Search icon
- **Contact Us button** (outlined pill)

**Complete Header:**
- Two-row layout
- Utility nav above main header
- Full navigation visible
- All features active

---

## CSS Breakpoints Used

```scss
// Mobile
@media (width < 768px) {
  // Hamburger only
  // Contact Us in mobile drawer
}

// Tablet & Small Desktop  
@media (width >= 768px) and (width < 1400px) {
  // Contact Us button visible
  // Hamburger menu visible
  // Navigation items hidden
}

// Large Desktop
@media (width >= 1400px) {
  // Full horizontal navigation
  // Contact Us button visible
  // Hamburger hidden
  // All nav items visible
}

// Utility Nav appears
@media (width >= 1400px) {
  .utility-nav {
    display: block;
  }
}
```

## Key Design Decision: Hamburger Until 1400px

**Why This Matters:**

Global Payments keeps the hamburger menu **much longer** than typical responsive designs. Most sites switch to full navigation around 992px (iPad landscape), but Global Payments waits until 1400px+.

**Benefits:**
1. **Cleaner header** on medium screens
2. **Contact Us button prominence** - not competing with many nav items
3. **Better for tablets** - easier to tap hamburger than small nav links
4. **Scalable** - works better with many navigation items

## Visual Layout by Screen Size

### Mobile (< 768px)
```
┌─────────────────────────────────┐
│ [Logo]              [☰]         │
└─────────────────────────────────┘
```

### Tablet/Small Desktop (768px - 1399px)
```
┌──────────────────────────────────────────┐
│ [Logo]           [Contact us] [☰]        │
└──────────────────────────────────────────┘
```

### Large Desktop (1400px+)
```
┌───────────────────────────────────────────────────────────────────┐
│ Careers  Developers  Log in                                  [🔍] │  ← Utility Nav
├───────────────────────────────────────────────────────────────────┤
│ [Logo]  Solutions  Products  Partners  Developers  Insights      │
│         Company                              [Contact us]         │
└───────────────────────────────────────────────────────────────────┘
```

## Contact Us Button Behavior

### Mobile (< 768px)
- **Location:** Inside mobile drawer menu
- **Style:** Full-width, filled blue button
- **Padding:** 0.75rem × 1.5rem
- **Width:** 100%

### Tablet & Above (≥ 768px)
- **Location:** Header (next to hamburger or in nav)
- **Style:** Outlined pill button
- **Colors:** 
  - Default: Transparent bg, blue border, black text
  - Hover: Blue bg, white text
- **Padding:** 0.75rem × 2rem
- **Border:** 2px solid #2536f0
- **Border-radius:** 2rem (fully rounded)

## Testing Checklist

- [ ] **375px (Mobile):** Logo + Hamburger only
- [ ] **768px (Tablet):** Logo + Contact Us + Hamburger
- [ ] **1024px (Small Desktop):** Logo + Contact Us + Hamburger (same as tablet)
- [ ] **1280px (Desktop):** Logo + Contact Us + Hamburger (same as tablet)
- [ ] **1400px (Large Desktop):** Logo + Full Nav + Contact Us (no hamburger)
- [ ] **1536px+ (XL Desktop):** Utility Nav + Logo + Full Nav + Contact Us

## Files Modified

1. `_component-navigation.scss` - Updated all breakpoints to 1400px
2. `navigation/_navigation-mobile.scss` - Extended mobile behavior to 1399px
3. `_component-utility-nav.scss` - Hidden until 1400px

## Implementation in Sitecore

**No changes needed!** The CSS handles everything automatically:

1. Logo text in `header-left` placeholder
2. Navigation component in `header-right` placeholder
3. Mark "Contact Us" with `button-nav-item` style class
4. Optional: Add utility nav above header (Eyebrow component)

The breakpoints now match Global Payments **exactly**! 🎉



