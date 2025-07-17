# Component Reference Guide

## Introduction

This guide provides detailed technical specifications for all glassmorphism components, including accessibility guidelines, performance considerations, and implementation best practices.

## Core Components

### GlassCard

#### Technical Specifications

**CSS Classes:**
- `.glass-card` - Base card component
- `.glass-card--small` - Small size variant
- `.glass-card--large` - Large size variant
- `.glass-card--interactive` - Interactive hover state

**Data Attributes:**
```html
data-glass-intensity="light|medium|heavy"
data-glass-color="white|black|blue|purple|pink|green|orange"
data-glass-blur="1-50"
data-glass-opacity="0.0-1.0"
data-glass-border="none|light|medium|heavy"
data-glass-shadow="none|light|medium|heavy"
```

**CSS Custom Properties:**
```css
--glass-card-padding: 1.5rem;
--glass-card-radius: 12px;
--glass-card-min-height: 100px;
--glass-card-max-width: 400px;
--glass-card-transition: all 0.3s ease;
```

#### Accessibility Guidelines

- **ARIA Labels**: Use `aria-label` or `aria-labelledby` for cards containing important information
- **Focus Management**: Ensure interactive cards are keyboard accessible with `tabindex="0"`
- **Color Contrast**: Maintain minimum 4.5:1 contrast ratio for text content
- **Screen Readers**: Use semantic HTML elements (`<article>`, `<section>`) within cards

```html
<article class="glass-card" aria-labelledby="card-title" tabindex="0" role="article">
  <h3 id="card-title">Accessible Card Title</h3>
  <p>Card content with proper contrast.</p>
</article>
```

#### Performance Considerations

- **Backdrop Filter**: Can impact performance on lower-end devices
- **Animation**: Use `transform` and `opacity` for smooth animations
- **Repaints**: Minimize changes to blur values during runtime

### GlassButton

#### Technical Specifications

**CSS Classes:**
- `.glass-button` - Base button component
- `.glass-button--primary` - Primary action button
- `.glass-button--secondary` - Secondary action button
- `.glass-button--accent` - Accent/call-to-action button
- `.glass-button--outline` - Outline variant
- `.glass-button--text` - Text-only variant

**States:**
- `:hover` - Hover state with enhanced glass effect
- `:focus` - Focus state with visible outline
- `:active` - Active/pressed state
- `:disabled` - Disabled state with reduced opacity

**Data Attributes:**
```html
data-variant="primary|secondary|accent|outline|text"
data-size="small|medium|large|xl"
data-glass-hover="true|false"
data-loading="true|false"
data-icon-position="left|right|only"
```

#### Implementation Examples

**Basic Button:**
```html
<button class="glass-button" data-variant="primary">
  Click Me
</button>
```

**Button with Icon:**
```html
<button class="glass-button" data-variant="secondary" data-icon-position="left">
  <svg class="button-icon" aria-hidden="true">...</svg>
  Save Document
</button>
```

**Loading State:**
```html
<button class="glass-button" data-variant="primary" data-loading="true" disabled>
  <span class="loading-spinner" aria-hidden="true"></span>
  Processing...
</button>
```

#### Accessibility Guidelines

- **Semantic HTML**: Always use `<button>` for interactive elements
- **ARIA States**: Use `aria-pressed`, `aria-expanded` for toggle buttons
- **Loading States**: Use `aria-busy="true"` and `aria-describedby` for loading feedback
- **Focus Indicators**: Ensure visible focus indicators for keyboard navigation

### GlassModal

#### Technical Specifications

**Structure:**
```html
<div class="glass-modal" id="modal-id" role="dialog" aria-labelledby="modal-title" aria-modal="true">
  <div class="glass-modal-backdrop" data-dismiss="modal"></div>
  <div class="glass-modal-container">
    <div class="glass-modal-content">
      <header class="glass-modal-header">
        <h2 id="modal-title">Modal Title</h2>
        <button class="glass-modal-close" data-dismiss="modal" aria-label="Close">×</button>
      </header>
      <div class="glass-modal-body">
        <!-- Modal content -->
      </div>
      <footer class="glass-modal-footer">
        <!-- Action buttons -->
      </footer>
    </div>
  </div>
</div>
```

**JavaScript API:**
```javascript
// Instance methods
const modal = new GlassModal('#modal-id', options);
modal.show();
modal.hide();
modal.toggle();
modal.dispose();

// Static methods
GlassModal.show('#modal-id');
GlassModal.hide('#modal-id');
GlassModal.getInstance('#modal-id');
```

#### Configuration Options

```javascript
const options = {
  backdrop: true,           // Show backdrop
  keyboard: true,           // Close on ESC key
  focus: true,             // Focus modal on show
  animation: 'fade',       // Animation type
  size: 'medium',          // Modal size
  centered: false,         // Vertically center
  scrollable: false,       // Scrollable body
  static: false           // Static backdrop
};
```

#### Accessibility Guidelines

- **Focus Management**: Trap focus within modal when open
- **ARIA Attributes**: Use proper `role`, `aria-modal`, `aria-labelledby`
- **Keyboard Navigation**: Support ESC to close, Tab to navigate
- **Screen Reader**: Announce modal opening/closing

### GlassNavigation

#### Technical Specifications

**Structure:**
```html
<nav class="glass-nav" role="navigation" aria-label="Main navigation">
  <div class="glass-nav-brand">
    <a href="/" class="glass-nav-brand-link">Brand</a>
  </div>
  <button class="glass-nav-toggle" aria-expanded="false" aria-controls="nav-menu">
    <span class="sr-only">Toggle navigation</span>
    <span class="glass-nav-toggle-icon"></span>
  </button>
  <div class="glass-nav-collapse" id="nav-menu">
    <ul class="glass-nav-items">
      <li class="glass-nav-item">
        <a href="#home" class="glass-nav-link" aria-current="page">Home</a>
      </li>
      <li class="glass-nav-item">
        <a href="#about" class="glass-nav-link">About</a>
      </li>
    </ul>
  </div>
</nav>
```

**Responsive Behavior:**
- Desktop: Horizontal layout with full visibility
- Tablet: Collapsible with hamburger menu
- Mobile: Stacked vertical layout

#### JavaScript Integration

```javascript
// Initialize responsive navigation
const nav = new GlassNavigation('.glass-nav', {
  breakpoint: 768,
  animation: 'slide',
  autoHide: true,
  scrollSpy: true
});

// Methods
nav.toggle();
nav.show();
nav.hide();
nav.setActive(linkElement);
```

## Advanced Components

### GlassForm

#### Technical Specifications

**Form Controls:**
- `.glass-input` - Text input with glass styling
- `.glass-textarea` - Textarea with glass styling
- `.glass-select` - Select dropdown with glass styling
- `.glass-checkbox` - Checkbox with glass styling
- `.glass-radio` - Radio button with glass styling

**Validation States:**
- `.is-valid` - Valid input state
- `.is-invalid` - Invalid input state
- `.is-pending` - Validation pending state

#### Implementation

```html
<form class="glass-form" novalidate>
  <div class="glass-form-group">
    <label for="email" class="glass-form-label">Email Address</label>
    <input type="email" id="email" class="glass-input" required 
           aria-describedby="email-help email-feedback">
    <div id="email-help" class="glass-form-text">We'll never share your email.</div>
    <div id="email-feedback" class="glass-form-feedback"></div>
  </div>
  
  <div class="glass-form-group">
    <label for="message" class="glass-form-label">Message</label>
    <textarea id="message" class="glass-textarea" rows="4" required
              aria-describedby="message-feedback"></textarea>
    <div id="message-feedback" class="glass-form-feedback"></div>
  </div>
  
  <button type="submit" class="glass-button" data-variant="primary">
    Submit Form
  </button>
</form>
```

### GlassTooltip

#### Technical Specifications

**Positioning:**
- `data-placement="top|bottom|left|right"`
- `data-offset="0"` - Offset from target element
- `data-boundary="viewport|window"` - Boundary element

**Triggers:**
- `data-trigger="hover|focus|click|manual"`
- `data-delay="0"` - Show/hide delay in milliseconds

#### Implementation

```html
<button class="glass-button" 
        data-glass-tooltip="This is a helpful tooltip"
        data-placement="top"
        data-trigger="hover focus">
  Hover for tooltip
</button>
```

```javascript
// Manual control
const tooltip = new GlassTooltip(element, {
  title: 'Dynamic tooltip content',
  placement: 'bottom',
  trigger: 'manual'
});

tooltip.show();
tooltip.hide();
```

### GlassDropdown

#### Technical Specifications

**Structure:**
```html
<div class="glass-dropdown">
  <button class="glass-button glass-dropdown-toggle" 
          data-toggle="dropdown" 
          aria-expanded="false"
          aria-haspopup="true">
    Dropdown Button
  </button>
  <div class="glass-dropdown-menu" role="menu">
    <a class="glass-dropdown-item" href="#" role="menuitem">Action</a>
    <a class="glass-dropdown-item" href="#" role="menuitem">Another action</a>
    <div class="glass-dropdown-divider" role="separator"></div>
    <a class="glass-dropdown-item" href="#" role="menuitem">Separated link</a>
  </div>
</div>
```

**JavaScript API:**
```javascript
const dropdown = new GlassDropdown(toggleElement, {
  placement: 'bottom-start',
  boundary: 'viewport',
  offset: [0, 2],
  autoClose: true
});
```

## Utility Components

### GlassLoading

#### Spinner Variants

```html
<!-- Basic spinner -->
<div class="glass-spinner" role="status" aria-label="Loading">
  <span class="sr-only">Loading...</span>
</div>

<!-- Pulsing dots -->
<div class="glass-loading-dots" role="status" aria-label="Loading">
  <span class="dot"></span>
  <span class="dot"></span>
  <span class="dot"></span>
</div>

<!-- Progress bar -->
<div class="glass-progress" role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">
  <div class="glass-progress-bar" style="width: 75%"></div>
</div>
```

### GlassAlert

#### Alert Types

```html
<!-- Info alert -->
<div class="glass-alert glass-alert--info" role="alert">
  <h4 class="glass-alert-heading">Information</h4>
  <p>This is an informational message.</p>
</div>

<!-- Success alert -->
<div class="glass-alert glass-alert--success" role="alert">
  <p>Operation completed successfully!</p>
</div>

<!-- Warning alert -->
<div class="glass-alert glass-alert--warning" role="alert">
  <p>Please review your input before proceeding.</p>
</div>

<!-- Error alert -->
<div class="glass-alert glass-alert--error" role="alert">
  <h4 class="glass-alert-heading">Error</h4>
  <p>An error occurred while processing your request.</p>
  <button class="glass-button glass-button--outline">Retry</button>
</div>
```

## Best Practices

### Performance Optimization

1. **Minimize Backdrop Filters**: Use sparingly and prefer CSS transforms for animations
2. **Hardware Acceleration**: Use `will-change` property for animated elements
3. **Debounce Scroll**: Debounce scroll events for better performance
4. **Lazy Loading**: Initialize components only when needed

```css
.glass-card {
  will-change: transform, opacity;
  transform: translateZ(0); /* Force hardware acceleration */
}
```

### Accessibility Best Practices

1. **Semantic HTML**: Use appropriate semantic elements
2. **Keyboard Navigation**: Ensure all interactive elements are keyboard accessible
3. **Screen Reader Support**: Provide proper ARIA labels and descriptions
4. **Color Contrast**: Maintain sufficient contrast ratios
5. **Focus Management**: Implement proper focus management for modals and dropdowns

### Browser Compatibility

#### Fallback Strategies

```css
/* Fallback for older browsers */
.glass-effect {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(255, 255, 255, 0.3);
}

/* Modern browsers with backdrop-filter support */
@supports (backdrop-filter: blur(10px)) {
  .glass-effect {
    backdrop-filter: blur(10px);
    background: rgba(255, 255, 255, 0.1);
  }
}

/* Feature detection with JavaScript */
if ('CSS' in window && CSS.supports('backdrop-filter', 'blur(10px)')) {
  document.documentElement.classList.add('backdrop-filter-support');
}
```

### Testing Guidelines

#### Component Testing

```javascript
// Example test for GlassModal
describe('GlassModal', () => {
  test('should show and hide modal', () => {
    const modal = new GlassModal('#test-modal');
    modal.show();
    expect(document.body.classList).toContain('modal-open');
    
    modal.hide();
    expect(document.body.classList).not.toContain('modal-open');
  });
  
  test('should trap focus when open', () => {
    const modal = new GlassModal('#test-modal');
    modal.show();
    
    // Test focus trapping
    const firstFocusable = modal.element.querySelector('[tabindex="0"]');
    expect(document.activeElement).toBe(firstFocusable);
  });
});
```

#### Accessibility Testing

```javascript
// Automated accessibility testing
import { axe, toHaveNoViolations } from 'jest-axe';

test('should not have accessibility violations', async () => {
  const { container } = render(<GlassCard>Content</GlassCard>);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});
```

---

This component reference provides detailed specifications for implementing glassmorphism components with proper accessibility, performance, and browser compatibility considerations.