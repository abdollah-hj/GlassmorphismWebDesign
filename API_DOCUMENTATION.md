# Glassmorphism Web Design - API Documentation

## Table of Contents

1. [Overview](#overview)
2. [Core Components](#core-components)
3. [CSS Utilities](#css-utilities)
4. [JavaScript APIs](#javascript-apis)
5. [Configuration](#configuration)
6. [Examples](#examples)
7. [Browser Support](#browser-support)

## Overview

The Glassmorphism Web Design library provides modern, glass-like UI components with backdrop blur effects, transparency, and subtle borders. This documentation covers all public APIs, components, and utilities available in the library.

## Core Components

### GlassCard Component

Creates a glassmorphic card with customizable properties.

#### Syntax
```html
<div class="glass-card" data-glass-intensity="medium" data-glass-color="white">
  <!-- Content -->
</div>
```

#### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data-glass-intensity` | `string` | `"medium"` | Glass effect intensity: `"light"`, `"medium"`, `"heavy"` |
| `data-glass-color` | `string` | `"white"` | Base color: `"white"`, `"black"`, `"blue"`, `"purple"`, `"pink"` |
| `data-glass-blur` | `number` | `10` | Backdrop blur amount in pixels |
| `data-glass-opacity` | `number` | `0.1` | Background opacity (0-1) |

#### Example
```html
<div class="glass-card" data-glass-intensity="heavy" data-glass-color="blue">
  <h3>Glass Card Title</h3>
  <p>This is a glassmorphic card with heavy blur and blue tint.</p>
</div>
```

### GlassButton Component

Interactive button with glassmorphic styling and hover effects.

#### Syntax
```html
<button class="glass-button" data-variant="primary" data-size="medium">
  Button Text
</button>
```

#### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data-variant` | `string` | `"primary"` | Button style: `"primary"`, `"secondary"`, `"accent"` |
| `data-size` | `string` | `"medium"` | Button size: `"small"`, `"medium"`, `"large"` |
| `data-glass-hover` | `boolean` | `true` | Enable hover glass effect |

#### Example
```html
<button class="glass-button" data-variant="accent" data-size="large">
  Get Started
</button>
```

### GlassModal Component

Modal dialog with glassmorphic backdrop and content area.

#### Syntax
```html
<div class="glass-modal" id="modal-id">
  <div class="glass-modal-content">
    <!-- Modal content -->
  </div>
</div>
```

#### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data-backdrop-blur` | `number` | `15` | Background blur intensity |
| `data-close-on-click` | `boolean` | `true` | Close modal on backdrop click |
| `data-animation` | `string` | `"fade"` | Animation type: `"fade"`, `"slide"`, `"scale"` |

#### Methods

```javascript
// Show modal
GlassModal.show('modal-id');

// Hide modal
GlassModal.hide('modal-id');

// Toggle modal
GlassModal.toggle('modal-id');
```

#### Example
```html
<div class="glass-modal" id="example-modal" data-animation="scale">
  <div class="glass-modal-content">
    <h2>Modal Title</h2>
    <p>Modal content goes here.</p>
    <button onclick="GlassModal.hide('example-modal')">Close</button>
  </div>
</div>
```

### GlassNavigation Component

Navigation bar with glassmorphic styling.

#### Syntax
```html
<nav class="glass-nav" data-position="fixed" data-glass-intensity="medium">
  <ul class="glass-nav-items">
    <li><a href="#home">Home</a></li>
    <li><a href="#about">About</a></li>
  </ul>
</nav>
```

#### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `data-position` | `string` | `"static"` | Position: `"static"`, `"fixed"`, `"sticky"` |
| `data-glass-intensity` | `string` | `"medium"` | Glass effect intensity |
| `data-auto-hide` | `boolean` | `false` | Auto-hide on scroll |

## CSS Utilities

### Glass Effect Utilities

#### `.glass-effect`
Base glass effect utility class.

```css
.glass-effect {
  backdrop-filter: blur(10px);
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
}
```

#### Intensity Modifiers

- `.glass-light` - Light glass effect
- `.glass-medium` - Medium glass effect  
- `.glass-heavy` - Heavy glass effect

#### Color Modifiers

- `.glass-white` - White-tinted glass
- `.glass-black` - Black-tinted glass
- `.glass-blue` - Blue-tinted glass
- `.glass-purple` - Purple-tinted glass
- `.glass-pink` - Pink-tinted glass

### Layout Utilities

#### `.glass-container`
Container with glassmorphic styling and responsive behavior.

```css
.glass-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  backdrop-filter: blur(15px);
  background: rgba(255, 255, 255, 0.05);
}
```

#### `.glass-grid`
CSS Grid layout with glass styling.

```css
.glass-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}
```

## JavaScript APIs

### GlassEffects Class

Main class for managing glass effects and animations.

#### Constructor

```javascript
const glassEffects = new GlassEffects(options);
```

#### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `autoInit` | `boolean` | `true` | Auto-initialize on DOM ready |
| `animationDuration` | `number` | `300` | Animation duration in ms |
| `blurIntensity` | `number` | `10` | Default blur intensity |

#### Methods

##### `init()`
Initialize all glass effects.

```javascript
glassEffects.init();
```

##### `applyGlassEffect(element, options)`
Apply glass effect to specific element.

```javascript
glassEffects.applyGlassEffect(element, {
  intensity: 'heavy',
  color: 'blue',
  blur: 15
});
```

##### `removeGlassEffect(element)`
Remove glass effect from element.

```javascript
glassEffects.removeGlassEffect(element);
```

##### `updateGlassEffect(element, newOptions)`
Update existing glass effect.

```javascript
glassEffects.updateGlassEffect(element, {
  intensity: 'light',
  color: 'purple'
});
```

#### Events

Glass effects emit custom events:

```javascript
// Glass effect applied
element.addEventListener('glass:applied', (event) => {
  console.log('Glass effect applied', event.detail);
});

// Glass effect removed
element.addEventListener('glass:removed', (event) => {
  console.log('Glass effect removed', event.detail);
});

// Glass effect updated
element.addEventListener('glass:updated', (event) => {
  console.log('Glass effect updated', event.detail);
});
```

### GlassModal Class

Modal management with glassmorphic styling.

#### Static Methods

##### `show(modalId, options)`
Show modal with optional configuration.

```javascript
GlassModal.show('my-modal', {
  animation: 'slide',
  duration: 400,
  backdrop: true
});
```

##### `hide(modalId, options)`
Hide modal.

```javascript
GlassModal.hide('my-modal', {
  animation: 'fade',
  duration: 300
});
```

##### `create(content, options)`
Create and show modal programmatically.

```javascript
const modal = GlassModal.create({
  title: 'Dynamic Modal',
  content: '<p>This modal was created dynamically.</p>',
  buttons: [
    { text: 'Cancel', action: 'close' },
    { text: 'Confirm', action: () => console.log('Confirmed') }
  ]
}, {
  size: 'large',
  animation: 'scale'
});
```

### GlassTheme Class

Theme management for glassmorphic components.

#### Methods

##### `setTheme(themeName)`
Set active theme.

```javascript
GlassTheme.setTheme('dark');
```

##### `getTheme()`
Get current theme.

```javascript
const currentTheme = GlassTheme.getTheme();
```

##### `registerTheme(name, config)`
Register custom theme.

```javascript
GlassTheme.registerTheme('custom', {
  primary: 'rgba(100, 200, 255, 0.1)',
  secondary: 'rgba(255, 100, 200, 0.1)',
  blur: 12,
  border: 'rgba(255, 255, 255, 0.3)'
});
```

## Configuration

### Global Configuration

Configure library defaults:

```javascript
GlassConfig.set({
  defaultBlur: 10,
  defaultOpacity: 0.1,
  animationDuration: 300,
  borderRadius: 12,
  theme: 'light'
});
```

### CSS Custom Properties

Customize styling using CSS custom properties:

```css
:root {
  --glass-blur: 10px;
  --glass-opacity: 0.1;
  --glass-border: rgba(255, 255, 255, 0.2);
  --glass-radius: 12px;
  --glass-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}
```

## Examples

### Basic Glass Card

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="glassmorphism.css">
</head>
<body>
  <div class="glass-card" data-glass-color="blue">
    <h2>Welcome</h2>
    <p>This is a beautiful glass card.</p>
  </div>
  
  <script src="glassmorphism.js"></script>
</body>
</html>
```

### Interactive Dashboard

```html
<div class="glass-container">
  <nav class="glass-nav" data-position="fixed">
    <ul class="glass-nav-items">
      <li><a href="#dashboard">Dashboard</a></li>
      <li><a href="#analytics">Analytics</a></li>
      <li><a href="#settings">Settings</a></li>
    </ul>
  </nav>
  
  <div class="glass-grid">
    <div class="glass-card" data-glass-intensity="light">
      <h3>Revenue</h3>
      <p class="metric">$12,345</p>
    </div>
    
    <div class="glass-card" data-glass-intensity="medium">
      <h3>Users</h3>
      <p class="metric">1,234</p>
    </div>
    
    <div class="glass-card" data-glass-intensity="heavy">
      <h3>Growth</h3>
      <p class="metric">+15%</p>
    </div>
  </div>
</div>
```

### Form with Glass Effects

```html
<form class="glass-card" data-glass-color="white">
  <h2>Contact Us</h2>
  
  <div class="form-group">
    <input type="text" placeholder="Name" class="glass-input">
  </div>
  
  <div class="form-group">
    <input type="email" placeholder="Email" class="glass-input">
  </div>
  
  <div class="form-group">
    <textarea placeholder="Message" class="glass-textarea"></textarea>
  </div>
  
  <button type="submit" class="glass-button" data-variant="primary">
    Send Message
  </button>
</form>
```

### Modal Implementation

```html
<button onclick="GlassModal.show('contact-modal')" class="glass-button">
  Open Modal
</button>

<div class="glass-modal" id="contact-modal" data-animation="scale">
  <div class="glass-modal-content">
    <h2>Contact Information</h2>
    <p>Get in touch with us using the form below.</p>
    
    <form>
      <input type="text" placeholder="Your Name" class="glass-input">
      <input type="email" placeholder="Your Email" class="glass-input">
      <button type="submit" class="glass-button">Submit</button>
    </form>
    
    <button onclick="GlassModal.hide('contact-modal')" class="glass-button" data-variant="secondary">
      Close
    </button>
  </div>
</div>
```

## Browser Support

### Supported Browsers

- **Chrome**: 76+ (full support)
- **Firefox**: 70+ (full support)
- **Safari**: 13+ (full support)
- **Edge**: 79+ (full support)

### Features

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `backdrop-filter` | ✅ 76+ | ✅ 70+ | ✅ 13+ | ✅ 79+ |
| CSS Grid | ✅ 57+ | ✅ 52+ | ✅ 10.1+ | ✅ 16+ |
| Custom Properties | ✅ 49+ | ✅ 31+ | ✅ 9.1+ | ✅ 15+ |

### Fallbacks

For browsers without `backdrop-filter` support:

```css
.glass-effect {
  background: rgba(255, 255, 255, 0.9);
}

@supports (backdrop-filter: blur(10px)) {
  .glass-effect {
    backdrop-filter: blur(10px);
    background: rgba(255, 255, 255, 0.1);
  }
}
```

---

This documentation provides comprehensive coverage of all public APIs, components, and utilities in the Glassmorphism Web Design library. For additional examples and advanced usage, please refer to the example files in the repository.