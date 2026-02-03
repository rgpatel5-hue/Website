# Implementation Details

## Code Structure Overview

### Landing Page (`/index.html`)
The landing page is a single, self-contained HTML file with:
- Inline CSS (no external stylesheets)
- Inline JavaScript for interactivity
- No dependencies except Google Fonts

### File Size & Performance
- **HTML**: ~513 lines (~18KB uncompressed)
- **CSS**: Inline (~8KB)
- **JavaScript**: Inline (~2KB)
- **Total**: Minimal, fast-loading page
- **External Dependencies**: Only Google Fonts

---

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- Meta tags and styling -->
  </head>
  <body>
    <header>
      <!-- Logo and header buttons -->
    </header>
    
    <div class="main-container">
      <!-- Left content section -->
      <div class="left-content">
        <!-- Badge, headline, description, stats -->
      </div>
      
      <!-- Right glass card section -->
      <div class="right-content">
        <div class="glass-card">
          <!-- Title, subtitle -->
          <div class="glass-visual">
            <!-- Glass outline + water fill -->
          </div>
          <!-- Donation buttons grid -->
          <!-- Custom amount input -->
          <!-- Donate button -->
        </div>
      </div>
    </div>
    
    <script>
      <!-- JavaScript functionality -->
    </script>
  </body>
</html>
```

---

## CSS Architecture

### CSS Variables (Color System)
```css
:root {
  --cw-yellow: #FFC82C;
  --cw-yellow-light: #FFCF50;
  --cw-yellow-dark: #E5B327;
  --cw-blue-dark: #005587;
  --cw-blue: #0077B5;
  --cw-blue-light: #00A3E0;
  --cw-water-blue: #00A3E0;
  --cw-water-blue-light: #5BC4F1;
  --cw-white: #F5F5F5;
  --cw-black: #1A1A1A;
  --cw-gray: #4A4A4A;
}
```

### Layout System
- **Flexbox** for header and main container alignment
- **CSS Grid** for donation button layout (3 columns)
- **Media Queries** for responsive breakpoints

### Animation System
```css
@keyframes wave {
  0% { transform: translateX(0); }
  100% { transform: translateX(60px); }
}

/* Applied to water fill pseudo-element */
.water-fill::before {
  animation: wave 3s linear infinite;
}
```

### Responsive Design
```css
/* Mobile first approach */
@media (max-width: 1024px) {
  .main-container {
    flex-direction: column; /* Stack vertically */
  }
}

@media (max-width: 768px) {
  /* Additional adjustments for smaller screens */
}
```

---

## JavaScript Implementation

### State Management
```javascript
let selectedAmount = 10;    // Currently selected donation amount
let totalDonated = 0;       // Running total of all donations
```

### Core Functions

#### 1. selectAmount(amount)
```javascript
function selectAmount(amount) {
  selectedAmount = amount;
  // Update button states (add/remove 'active' class)
  // Clear custom input
  updateDisplay();
}
```
**Purpose**: Handles quick-select button clicks
**Updates**: Button states, display, glass fill

#### 2. Custom Input Handler
```javascript
document.getElementById('customAmount').addEventListener('input', function() {
  if (this.value) {
    selectedAmount = parseInt(this.value) || 0;
    // Remove active state from buttons
    updateDisplay();
  }
});
```
**Purpose**: Handles custom amount input
**Updates**: Selected amount when user types

#### 3. updateDisplay()
```javascript
function updateDisplay() {
  const total = totalDonated + selectedAmount;
  document.getElementById('amountDisplay').textContent = '$' + total;
  
  // Calculate fill percentage (max 100%)
  const percentage = Math.min((total / 40) * 100, 100);
  document.getElementById('waterFill').style.height = percentage + '%';
}
```
**Purpose**: Updates display and glass fill
**Updates**: Amount text, glass fill height

#### 4. processDonation()
```javascript
function processDonation() {
  if (selectedAmount <= 0) {
    alert('Please select a valid amount');
    return;
  }
  
  totalDonated += selectedAmount;
  updateDisplay();
  
  // Visual feedback (wave animation restart)
  // Reset form
  // Show confirmation
}
```
**Purpose**: Processes donation and updates state
**Actions**:
- Validates amount
- Adds to total
- Updates display
- Restarts animation
- Resets form

---

## CSS Classes Reference

### Structure Classes
```css
.glass-card         /* Main white card container */
.glass-visual       /* Glass container wrapper */
.glass-outline      /* Glass shape with border */
.water-fill         /* Animated water inside glass */
.donation-grid      /* 3-column button grid */
.donation-btn       /* Individual donation button */
.main-container     /* Main layout container */
.left-content       /* Left column content */
.right-content      /* Right column (glass card) */
```

### State Classes
```css
.active             /* Active button indicator */
.glass-card         /* Card in focus */
```

### Pseudo-elements
```css
.glass-outline::before    /* Glass rim */
.glass-outline::after     /* Glass shine effect (if added) */
.water-fill::before       /* Wave animation */
.badge::before            /* Checkmark symbol */
```

---

## Event Listeners

### Button Click Events
```html
<button class="donation-btn" onclick="selectAmount(5)">$5</button>
```
- Triggers: `selectAmount()` function
- Updates: Button state and display

### Custom Input
```html
<input type="number" id="customAmount" placeholder="...">
```
- Listener: `addEventListener('input', ...)`
- Updates: Selected amount in real-time

### Main Donation Button
```html
<button class="donate-btn-main" onclick="processDonation()">DONATE NOW</button>
```
- Triggers: `processDonation()` function
- Updates: Total, display, form state

---

## Glass Fill Mathematics

### Formula
```
Fill Percentage = (Total Donated / $40) × 100
Max: 100% (capped)
```

### Examples
```
$0 donated    → 0% filled
$5 donated    → 12.5% filled
$10 donated   → 25% filled
$20 donated   → 50% filled
$40 donated   → 100% filled (full)
$80 donated   → 100% filled (capped)
```

### Implementation
```javascript
const percentage = Math.min((total / 40) * 100, 100);
document.getElementById('waterFill').style.height = percentage + '%';
```

---

## Responsive Breakpoints

### Mobile (< 768px)
- **Layout**: Single column (stacked)
- **Padding**: Reduced (20px)
- **Font**: Smaller (mobile-optimized)
- **Grid**: Maintained (responsive columns)

### Tablet (768px - 1024px)
- **Layout**: Transitional
- **Padding**: Medium (30px)
- **Font**: Medium size
- **Grid**: Flexible

### Desktop (> 1024px)
- **Layout**: Two-column side-by-side
- **Padding**: Full (40px)
- **Font**: Optimal size
- **Grid**: Full 3 columns

---

## Color Usage Guide

### Primary Colors
| Element | Color | Hex |
|---------|-------|-----|
| Background | Blue gradient | #005587 → #0077B5 |
| Card | White | #F5F5F5 |
| Badge | Yellow | #FFC82C |
| Water | Light Blue | #00A3E0 |

### Secondary Colors
| Element | Color | Hex |
|---------|-------|-----|
| Buttons (inactive) | Gray border | #4A4A4A |
| Buttons (active) | Water Blue | #00A3E0 |
| Accent Yellow | Light | #FFCF50 |
| Dark Text | Black | #1A1A1A |

---

## Animation Timeline

### Wave Animation (3 seconds, infinite)
```
0%    → Wave at position 0
50%   → Wave translated 30px
100%  → Wave translated 60px (loops)
```

### Transition Effects (300ms ease)
```
Button hover    → 300ms color transition
Button click    → 150ms state change
Glass fill      → 500ms height transition
```

---

## Browser Compatibility

### Supported Features
- ✓ CSS Grid Layout
- ✓ Flexbox
- ✓ CSS Variables
- ✓ CSS Animations
- ✓ Linear Gradients
- ✓ ES6 JavaScript

### Browsers
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari 14+, Chrome Mobile)

---

## Optimization Techniques

### Performance
1. **Inline CSS**: Eliminates extra HTTP request
2. **Minimal JavaScript**: Only ~2KB of code
3. **No External Libraries**: No dependencies
4. **CSS Animations**: Hardware-accelerated
5. **Single Font Import**: Montserrat from Google Fonts

### Maintainability
1. **CSS Variables**: Easy color scheme changes
2. **Semantic HTML**: Clear structure
3. **Comments**: Documented sections
4. **Modular Functions**: Easy to extend

### Accessibility
1. **High Contrast**: WCAG AA compliant
2. **Large Touch Targets**: 44px minimum
3. **Clear Labels**: Readable button text
4. **Semantic HTML**: Screen reader friendly

---

## Future Enhancement Points

### Easy Additions
```javascript
// Add localStorage to persist donations
localStorage.setItem('totalDonated', totalDonated);

// Add sound effects
new Audio('ding.mp3').play();

// Add analytics tracking
gtag('event', 'donation', {amount: selectedAmount});
```

### Backend Integration
```javascript
// Connect to payment processor
fetch('/api/donate', {
  method: 'POST',
  body: JSON.stringify({amount: selectedAmount})
});
```

### Advanced Features
- Leaderboard tracking
- Social media sharing
- Email confirmations
- Receipt generation
- Tax deduction info

---

## Testing Checklist

### Visual Testing
- [ ] Header displays correctly
- [ ] Glass card centered and sized correctly
- [ ] Buttons visible and clickable
- [ ] Colors match design
- [ ] Text is readable
- [ ] Layout responsive on mobile
- [ ] Layout responsive on tablet
- [ ] Layout responsive on desktop

### Functional Testing
- [ ] Button clicks update selection
- [ ] Custom input accepts numbers
- [ ] Glass fills with animation
- [ ] Water wave animates
- [ ] Total updates correctly
- [ ] "Donate Now" processes
- [ ] Form resets after donation
- [ ] No console errors

### Accessibility Testing
- [ ] Tab navigation works
- [ ] Color contrast sufficient
- [ ] Touch targets large enough
- [ ] Screen reader friendly

---

## Deployment Checklist

Before deploying to production:
- [ ] Test all buttons
- [ ] Test responsive design
- [ ] Check for console errors
- [ ] Verify all links work
- [ ] Test on mobile devices
- [ ] Check color accuracy
- [ ] Verify font loading
- [ ] Test donation flow
- [ ] Check performance
- [ ] Validate HTML

---

Created: February 3, 2026  
Last Updated: February 3, 2026
