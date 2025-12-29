# Header GP Component - Sitecore Data Template Fields

## Overview
This document outlines all the fields needed for the **Header GP** component data template in Sitecore. The component recreates the Global Payments website header with full responsive support.

---

## Required Fields Structure

### Base Template
Create a new data template called **Header GP** (or similar) with the following fields:

---

### 1. Logo Section

| Field Name | Field Type | Description | Required |
|------------|-----------|-------------|----------|
| **LogoImage** | Image | The main logo image (Global Payments logo) | Yes |
| **LogoLink** | General Link | Link when clicking the logo (typically homepage) | Yes |

**Example Values:**
- LogoImage: Upload the Global Payments logo image
- LogoLink: Internal link to "/" (homepage)

---

### 2. Navigation Items

| Field Name | Field Type | Description | Required |
|------------|-----------|-------------|----------|
| **NavigationItems** | Multilist or Treelist | List of main navigation menu items | Yes |

**Navigation Item Template Structure:**
Create a separate template for **Navigation Item** with these fields:

| Field Name | Field Type | Description |
|------------|-----------|-------------|
| **Title** | Single-Line Text | Display text for the nav item (e.g., "Solutions", "Products") |
| **Link** | General Link | Target URL for the nav item |
| **Is Dropdown** | Checkbox | Whether this item has a dropdown menu |
| **Children** | Treelist | Child navigation items for dropdown menus |

**Example Navigation Items:**
1. Solutions (Is Dropdown: checked, has children)
2. Products (Is Dropdown: checked, has children)
3. Partners (Is Dropdown: checked, has children)
4. Developers (Is Dropdown: checked, has children)
5. Insights (Is Dropdown: unchecked, direct link)
6. Company (Is Dropdown: unchecked, external link)

---

### 3. Utility Links (Top Bar)

| Field Name | Field Type | Description | Required |
|------------|-----------|-------------|----------|
| **UtilityLinks** | Multilist or Treelist | Links for the top utility bar (desktop only) | No |

**Utility Link Template Structure:**
Create a separate template for **Utility Link** with these fields:

| Field Name | Field Type | Description |
|------------|-----------|-------------|
| **Title** | Single-Line Text | Display text for the link (e.g., "Careers", "Developers", "Log in") |
| **Link** | General Link | Target URL for the link |

**Example Utility Links:**
1. Careers → https://jobs.globalpayments.com/en/
2. Developers → https://developer.globalpay.com
3. Log in → https://myaccount.globalpayments.com/login

---

### 4. CTA Button

| Field Name | Field Type | Description | Required |
|------------|-----------|-------------|----------|
| **ButtonText** | Single-Line Text | Text for the primary CTA button | Yes |
| **ButtonLink** | General Link | Link for the CTA button | Yes |

**Example Values:**
- ButtonText: "Contact us"
- ButtonLink: Internal or external link to contact form/page

---

### 5. Mobile Menu

| Field Name | Field Type | Description | Required |
|------------|-----------|-------------|----------|
| **MobileMenuLabel** | Single-Line Text | Accessibility label for mobile menu toggle | No |

**Default Value:** "Open menu" / "Close menu"

---

## Content Structure Example

```
Header GP Datasource
├── LogoImage: [Image: global-payments-logo.svg]
├── LogoLink: [Link: /]
├── NavigationItems:
│   ├── Solutions
│   │   ├── Title: "Solutions"
│   │   ├── Link: [Link: /solutions]
│   │   ├── Is Dropdown: ✓
│   │   └── Children:
│   │       ├── Payment Processing
│   │       ├── Point of Sale
│   │       └── E-commerce Solutions
│   ├── Products
│   │   ├── Title: "Products"
│   │   ├── Link: [Link: /products]
│   │   ├── Is Dropdown: ✓
│   │   └── Children:
│   │       ├── Genius POS
│   │       ├── Payment Terminals
│   │       └── Software Solutions
│   ├── Partners
│   │   ├── Title: "Partners"
│   │   ├── Link: [Link: /partners]
│   │   ├── Is Dropdown: ✓
│   │   └── Children:
│   │       ├── Become a Partner
│   │       └── Partner Portal
│   ├── Developers
│   │   ├── Title: "Developers"
│   │   ├── Link: [Link: /developers]
│   │   ├── Is Dropdown: ✓
│   │   └── Children:
│   │       ├── API Documentation
│   │       ├── SDKs
│   │       └── Developer Tools
│   ├── Insights
│   │   ├── Title: "Insights"
│   │   ├── Link: [Link: /insights]
│   │   └── Is Dropdown: ☐
│   └── Company
│       ├── Title: "Company"
│       ├── Link: [External Link: https://company.globalpayments.com]
│       └── Is Dropdown: ☐
├── UtilityLinks:
│   ├── Careers
│   │   ├── Title: "Careers"
│   │   └── Link: [External Link: https://jobs.globalpayments.com/en/]
│   ├── Developers
│   │   ├── Title: "Developers"
│   │   └── Link: [External Link: https://developer.globalpay.com]
│   └── Log in
│       ├── Title: "Log in"
│       └── Link: [External Link: https://myaccount.globalpayments.com/login]
├── ButtonText: "Contact us"
├── ButtonLink: [Link: /contact]
└── MobileMenuLabel: "Menu"
```

---

## Responsive Behavior

### Desktop (1024px+)
- Top utility bar visible (Careers, Developers, Log in)
- Full horizontal navigation with dropdown menus
- Search icon visible
- Contact button visible
- Mobile hamburger hidden

### Tablet (768px - 1023px)
- Top utility bar hidden
- Navigation hidden (in hamburger menu)
- Search icon hidden (in hamburger menu)
- Contact button visible
- Mobile hamburger visible

### Mobile (< 768px)
- Top utility bar hidden
- Navigation hidden (in hamburger menu)
- Search icon hidden
- Contact button hidden
- Mobile hamburger visible
- Logo scales down to 180px max width

---

## GraphQL Query Structure

The component expects data in the following format:

```graphql
{
  fields {
    data {
      datasource {
        logoImage {
          jsonValue {
            value {
              src
              alt
              width
              height
            }
          }
        }
        logoLink {
          jsonValue {
            value {
              href
              text
              target
            }
          }
        }
        navigationItems {
          targetItems {
            id
            title {
              jsonValue {
                value
              }
            }
            link {
              jsonValue {
                value {
                  href
                  text
                  target
                }
              }
            }
            isDropdown
            children {
              id
              title {
                jsonValue {
                  value
                }
              }
              link {
                jsonValue {
                  value {
                    href
                    text
                    target
                  }
                }
              }
            }
          }
        }
        utilityLinks {
          targetItems {
            id
            title {
              jsonValue {
                value
              }
            }
            link {
              jsonValue {
                value {
                  href
                  text
                  target
                }
              }
            }
          }
        }
        buttonText {
          jsonValue {
            value
          }
        }
        buttonLink {
          jsonValue {
            value {
              href
              text
              target
            }
          }
        }
        mobileMenuLabel {
          jsonValue {
            value
          }
        }
      }
    }
  }
}
```

---

## Component Registration

Don't forget to register the component in your component map:

```typescript
// .sitecore/component-map.ts
import { Default as HeaderGP } from 'src/components/Navigation/header-gp';

export const componentMap = {
  // ... other components
  HeaderGP: HeaderGP,
};
```

---

## Styling

The component uses BEM naming convention and includes:
- Sticky header behavior
- Smooth transitions and animations
- Hover states for all interactive elements
- Accessible focus states
- Mobile-friendly touch targets

Import the SCSS file in your main stylesheet:

```scss
@import 'navigation/header-gp';
```

---

## Accessibility Features

- Semantic HTML5 elements (`<header>`, `<nav>`)
- ARIA labels for navigation regions
- ARIA expanded states for toggles
- Keyboard navigation support
- Focus management for search input
- Skip links support (add if needed)

---

## Notes

1. **ClickOutside Hook**: The component uses a `ClickOutside` hook for closing menus. Ensure this hook exists in your project at `src/hooks/ClickOutside.ts`

2. **NextImage Component**: Uses `NextImage` from `src/lib/image-components` for optimized images

3. **Container Classes**: Adjust container widths in the SCSS if needed to match your design system

4. **Colors**: The component uses Global Payments brand colors:
   - Primary Blue: `#0066ff`
   - Black: `#000000`
   - Gray variants: `#495057`, `#f8f9fa`, `#e9ecef`

5. **Animations**: Includes smooth slide-down animations for mobile menu and search overlay

---

## Testing Checklist

- [ ] Logo displays and links correctly
- [ ] All navigation items render
- [ ] Dropdown menus work on hover (desktop)
- [ ] Mobile menu toggles properly
- [ ] Search overlay opens and closes
- [ ] Contact button displays and links correctly
- [ ] Utility links display (desktop only)
- [ ] Responsive behavior works at all breakpoints
- [ ] Accessibility features work (keyboard nav, screen readers)
- [ ] Component works in both editing and preview modes


