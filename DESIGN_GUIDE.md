# Website Visual Guide

## Landing Page Layout

```
┌─────────────────────────────────────────────────────────┐
│  charity: water logo                      [Donate Now]  │
└─────────────────────────────────────────────────────────┘

┌──────────────────────────┐   ┌──────────────────────────┐
│                          │   │    Fill the Glass        │
│  100% Goes to Clean      │   │  Every tap brings...     │
│  Water                   │   │                          │
│                          │   │    ┌──────────────────┐  │
│  Your drop makes a       │   │    │ Glass Visual     │  │
│  difference.             │   │    │ with Water Fill  │  │
│                          │   │    └──────────────────┘  │
│  Tap to donate and watch │   │                          │
│  your drop help fill...  │   │  Tap the glass to add... │
│                          │   │                          │
│  703M+ | $40            │   │  $0                       │
│  People lack | Gives    │   │  of $40...                │
│  clean water | one      │   │                          │
│                          │   │  [$5] [$10] [$20]       │
│                          │   │  [$40] [$100] [$250]    │
│                          │   │                          │
│                          │   │  [Custom Amount]         │
│                          │   │                          │
│                          │   │  [DONATE NOW]            │
└──────────────────────────┘   └──────────────────────────┘
```

## Color Palette

### Primary Colors
- **Dark Blue (Background Top)**: #005587
- **Medium Blue (Background)**: #0077B5
- **Light Blue (Water/Links)**: #00A3E0
- **Yellow (Accent)**: #FFC82C
- **White (Cards/Text)**: #F5F5F5

### Secondary Colors
- **Dark Text**: #1A1A1A
- **Gray Text**: #4A4A4A
- **Yellow Light**: #FFCF50
- **Yellow Dark**: #E5B327

## Typography

### Font: Montserrat
- **H1 (Main Title)**: 3.5rem, Weight 800, Letter-spacing 0
- **H2 (Section Title)**: 1.8rem, Weight 700
- **Body Text**: 1.1rem, Weight 400, Line-height 1.6
- **Badge Text**: 0.85rem, Weight 600
- **Button Text**: 0.95rem, Weight 700, Letter-spacing 1px

## Interactive Elements

### Buttons
```
Default State:
┌──────────────────┐
│   [Button Text]  │
└──────────────────┘
Background: Varies by button type
Border: 2px
Padding: 12px (small), 14px (main)

Hover State:
┌──────────────────┐
│   [Button Text]  │
└──────────────────┘
Lightens/changes color with transition

Active State:
┌──────────────────┐
│   [Button Text]  │
└──────────────────┘
Different background, indicates selection
```

### Glass Visual
```
        Water Wave Effect
             ~~~~
        ┌─────────────┐
        │             │
        │   Water     │  <- Filled based on donation
        │   (Blue)    │  <- Height: 0% to 100%
        │             │
        │             │
        │             │
        └─────────────┘
   ▼                 ▼ (Rounded bottom)
```

## Responsive Breakpoints

### Mobile (< 768px)
```
┌─────────────────────┐
│    Header           │
├─────────────────────┤
│   Left Content      │
│   (Full Width)      │
├─────────────────────┤
│   Glass Card        │
│   (Full Width)      │
└─────────────────────┘
```

### Tablet (768px - 1024px)
```
┌─────────────────────────────────┐
│         Header                  │
├─────────────────────────────────┤
│   Left    │      Right          │
│  Content  │  (Glass Card)       │
│           │                     │
└─────────────────────────────────┘
```

### Desktop (> 1024px)
```
┌──────────────────────────────────────────┐
│    Header with Logo and Donate Button    │
├──────────────────────────────────────────┤
│                                          │
│   Left Content        │    Glass Card   │
│   - Badge            │    - Glass       │
│   - Headline         │    - Buttons     │
│   - Description      │    - Input       │
│   - Stats            │    - CTA         │
│                                          │
└──────────────────────────────────────────┘
```

## User Interaction Flow

```
1. User visits homepage
        ↓
2. Sees landing page with glass card
        ↓
3. Selects donation amount
   (from quick-select or custom input)
        ↓
4. Clicks "DONATE NOW"
        ↓
5. Glass fills with animation
   Water level increases
   Total amount updates
        ↓
6. Can make another donation
   or play the game
```

## Glass Fill Stages

```
Empty (0%)
┌─────────┐
│         │
│         │
│         │
│         │
│         │
└─────────┘

$10 (25%)
┌─────────┐
│         │
│         │
│         │
│ ▓▓▓▓▓   │
└─────────┘

$20 (50%)
┌─────────┐
│         │
│         │
│ ▓▓▓▓▓   │
│ ▓▓▓▓▓   │
└─────────┘

$40 (100%)
┌─────────┐
│ ▓▓▓▓▓   │
│ ▓▓▓▓▓   │
│ ▓▓▓▓▓   │
│ ▓▓▓▓▓   │
└─────────┘
FULL! ✓
```

## Animation Effects

### Wave Animation
```
Time 0s:   ~~~~
           ~~~~
Time 0.5s:  ~~~~
            ~~~~
Time 1s:   ~~~~
           ~~~~
(Continuous 3-second loop)
```

### Button Transitions
```
State Change: 300ms ease
Color Change: Smooth gradient
Hover Effect: Brightness increase
```

## Accessibility Features

✓ High color contrast (WCAG AA compliant)
✓ Large touch targets (44px minimum)
✓ Clear button labels
✓ Semantic HTML structure
✓ Focus indicators for keyboard navigation
✓ Mobile-friendly layout
✓ Readable font sizes

## Performance Metrics

- Inline CSS (no external file)
- Minimal JavaScript (~2KB)
- Single Google Font import
- Zero build process required
- Fast initial load time
- Smooth animations (60fps)

---

Created: February 3, 2026
