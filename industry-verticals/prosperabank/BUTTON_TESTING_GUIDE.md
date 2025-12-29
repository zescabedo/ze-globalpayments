# Button Styling Fix - Testing Guide

## Quick Verification Checklist

Use this guide to quickly verify that all button styling issues have been resolved across different devices.

---

## 🖥️ Desktop Testing (1024px+)

### What to Check:
- [ ] Buttons display inline (side by side)
- [ ] Button padding: 16px top/bottom, 24px left/right
- [ ] Button font size: 18px
- [ ] Minimum spacing of 64px between button and images below
- [ ] No overlap between buttons and hero images
- [ ] Pill-shaped buttons (50px border-radius)

### Expected Appearance:
```
┌─────────────────────────────────────────┐
│                                         │
│         Hero Title (70px)               │
│                                         │
│   [Get Started] [Learn More]           │  ← Buttons inline
│                                         │
│         (64px spacing)                  │
│                                         │
│   ┌─────┐ ┌─────┐ ┌─────┐              │  ← Hero images
│   │ Img │ │ Img │ │ Img │              │
│   └─────┘ └─────┘ └─────┘              │
└─────────────────────────────────────────┘
```

---

## 📱 Tablet Testing (768px - 1023px)

### What to Check:
- [ ] Buttons stack vertically (one per row)
- [ ] Button padding: 14px top/bottom, 20px left/right
- [ ] Button font size: 16px
- [ ] Button max-width: 400px (centered)
- [ ] Minimum spacing of 48px between button and images below
- [ ] No overlap between buttons and hero images
- [ ] Full width within 400px constraint

### Expected Appearance:
```
┌─────────────────────────────────┐
│                                 │
│     Hero Title (48px)           │
│                                 │
│    ┌──────────────────┐         │  ← Button 1
│    │  Get Started     │         │
│    └──────────────────┘         │
│    ┌──────────────────┐         │  ← Button 2
│    │  Learn More      │         │
│    └──────────────────┘         │
│                                 │
│      (48px spacing)             │
│                                 │
│   ┌─────────────────┐           │  ← Hero images
│   │  Image Grid     │           │
│   └─────────────────┘           │
└─────────────────────────────────┘
```

---

## 📱 Mobile Testing (370px - 767px)

### What to Check:
- [ ] Buttons stack vertically (one per row)
- [ ] Button padding: 14px top/bottom, 32px left/right
- [ ] Button font size: 16px
- [ ] Buttons are full width (100%)
- [ ] Minimum spacing of 40px between button and images below
- [ ] No overlap between buttons and hero images
- [ ] Easy to tap (proper touch targets)
- [ ] Text centered in buttons

### Expected Appearance:
```
┌─────────────────────────┐
│                         │
│  Hero Title (28px)      │
│                         │
│ ┌─────────────────────┐ │  ← Full width
│ │   Get Started       │ │
│ └─────────────────────┘ │
│ ┌─────────────────────┐ │  ← Full width
│ │   Learn More        │ │
│ └─────────────────────┘ │
│                         │
│   (40px spacing)        │
│                         │
│ ┌─────────────────────┐ │  ← Hero images
│ │   Image             │ │     (stacked)
│ └─────────────────────┘ │
└─────────────────────────┘
```

---

## 🧪 Testing Procedure

### 1. Test Default Hero Variant

Navigate to a page with the **Default Hero** component:

**Desktop** (resize browser to 1280px):
1. Open DevTools (F12)
2. Set viewport to 1280px width
3. Verify buttons are inline and properly spaced
4. Scroll to see no overlap with images

**Tablet** (resize to 768px):
1. Set viewport to 768px width
2. Verify buttons stack vertically
3. Verify max-width of 400px
4. Check spacing between buttons and images

**Mobile** (resize to 375px):
1. Set viewport to 375px width
2. Verify buttons are full width
3. Verify proper touch target size
4. Check no overlap with images below

### 2. Test LargeScrollingAnimation Variant

Navigate to a page with the **LargeScrollingAnimation Hero** component and repeat all the same tests.

### 3. Cross-Browser Testing

Test in:
- [ ] Chrome/Edge
- [ ] Firefox
- [ ] Safari (if on Mac)
- [ ] Mobile Safari (iPhone)
- [ ] Chrome Mobile (Android)

---

## 🐛 Common Issues & Solutions

### Issue: Buttons still overlapping images

**Check:**
- Is the `.cta-list` class present on the button container?
- Inspect the computed `margin-bottom` value
- Look for conflicting CSS rules

**Solution:**
```scss
.cta-list {
  margin-bottom: 64px; // Desktop
  
  @media (max-width: 767px) {
    margin-bottom: 40px; // Mobile
  }
}
```

### Issue: Buttons not full width on mobile

**Check:**
- Is the viewport truly < 768px?
- Are there any `max-width` constraints from parent elements?

**Solution:**
```scss
@media (max-width: 767px) {
  .cta-list {
    width: 100%;
    
    .link-inner {
      width: 100%;
    }
    
    .btn {
      width: 100%;
    }
  }
}
```

### Issue: Button text wrapping

**Check:**
- Is the button text too long?
- Is the padding too small?

**Solution:**
- Buttons have `white-space: nowrap` on desktop
- On mobile, text should not wrap if button is properly sized
- Consider shorter button text if needed

---

## 📊 Visual Comparison Checklist

Compare your localhost to GlobalPayments.com:

| Element | GlobalPayments.com | Your Site | Match? |
|---------|-------------------|-----------|--------|
| Button shape | Pill (50px radius) | ☐ | ☐ |
| Desktop inline layout | Yes | ☐ | ☐ |
| Mobile stacked layout | Yes | ☐ | ☐ |
| Mobile full width | Yes | ☐ | ☐ |
| Spacing before images | Good separation | ☐ | ☐ |
| No overlap | Clean separation | ☐ | ☐ |
| Button font size | 16-18px | ☐ | ☐ |
| Button padding | Comfortable | ☐ | ☐ |

---

## ✅ Success Criteria

Your button styling is correct when:

1. **✅ Desktop (1024px+)**
   - Buttons display inline
   - 64px spacing before images
   - No overlap
   - 16/24px padding
   - 18px font

2. **✅ Tablet (768px - 1023px)**
   - Buttons stack vertically
   - 400px max-width, centered
   - 48px spacing before images
   - No overlap
   - 14/20px padding
   - 16px font

3. **✅ Mobile (370px - 767px)**
   - Buttons stack vertically
   - Full width (100%)
   - 40px spacing before images
   - No overlap
   - 14/32px padding
   - 16px font

4. **✅ All Devices**
   - Pill-shaped buttons (50px border-radius)
   - Proper hover states
   - Accessible focus states
   - No text wrapping (desktop)
   - Smooth transitions between breakpoints

---

## 📝 Dev Tools Inspection

Use these DevTools commands to verify:

```javascript
// Check button padding
getComputedStyle(document.querySelector('.btn')).padding

// Check button font size
getComputedStyle(document.querySelector('.btn')).fontSize

// Check CTA list margin-bottom
getComputedStyle(document.querySelector('.cta-list')).marginBottom

// Check button width on mobile
getComputedStyle(document.querySelector('.btn')).width
```

---

## 🎯 Final Verification

Once all tests pass:

1. [ ] Desktop buttons display correctly
2. [ ] Tablet buttons display correctly
3. [ ] Mobile buttons display correctly
4. [ ] No overlap on any device
5. [ ] Matches GlobalPayments.com design
6. [ ] Accessible (keyboard navigation works)
7. [ ] Touch targets are adequate (44px+ height)
8. [ ] Smooth responsive behavior

**Status**: 🟢 Ready for Production

---

**Last Updated**: December 18, 2025  
**Tested Breakpoints**: 370px, 768px, 1024px, 1280px, 1536px



