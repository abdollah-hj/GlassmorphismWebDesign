# API Reference

## Table of Contents

1. [Core Classes](#core-classes)
2. [Utility Functions](#utility-functions)
3. [Configuration Objects](#configuration-objects)
4. [Events](#events)
5. [CSS Custom Properties](#css-custom-properties)
6. [TypeScript Definitions](#typescript-definitions)

## Core Classes

### GlassEffects

The main class for managing glassmorphism effects throughout your application.

#### Constructor

```javascript
new GlassEffects(options?: GlassEffectsOptions)
```

**Parameters:**

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| options | `GlassEffectsOptions` | No | `{}` | Configuration options |

**Options Object:**

```typescript
interface GlassEffectsOptions {
  autoInit?: boolean;           // Auto-initialize on creation
  animationDuration?: number;   // Default animation duration (ms)
  blurIntensity?: number;      // Default blur intensity
  fallbackMode?: boolean;      // Enable fallback for unsupported browsers
  debugMode?: boolean;         // Enable debug logging
}
```

#### Methods

##### `init()`

Initialize all glassmorphism effects in the document.

```javascript
init(): Promise<void>
```

**Returns:** Promise that resolves when initialization is complete.

**Example:**
```javascript
const glass = new GlassEffects();
await glass.init();
```

##### `applyGlassEffect(element, options)`

Apply glassmorphism effect to a specific element.

```javascript
applyGlassEffect(
  element: Element | string,
  options?: GlassOptions
): GlassInstance
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| element | `Element \| string` | Yes | Target element or CSS selector |
| options | `GlassOptions` | No | Effect configuration |

**Options Object:**

```typescript
interface GlassOptions {
  intensity?: 'light' | 'medium' | 'heavy' | number;
  color?: 'white' | 'black' | 'blue' | 'purple' | 'pink' | string;
  blur?: number;              // Blur amount in pixels (0-50)
  opacity?: number;           // Background opacity (0-1)
  border?: 'none' | 'light' | 'medium' | 'heavy';
  shadow?: 'none' | 'light' | 'medium' | 'heavy';
  borderRadius?: number;      // Border radius in pixels
  animation?: boolean;        // Enable transition animations
}
```

**Returns:** `GlassInstance` object for further manipulation.

**Example:**
```javascript
const glassInstance = glass.applyGlassEffect('#my-card', {
  intensity: 'heavy',
  color: 'blue',
  blur: 15,
  opacity: 0.2
});
```

##### `removeGlassEffect(element)`

Remove glassmorphism effect from an element.

```javascript
removeGlassEffect(element: Element | string): boolean
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| element | `Element \| string` | Yes | Target element or CSS selector |

**Returns:** `true` if effect was removed, `false` if no effect was found.

**Example:**
```javascript
const removed = glass.removeGlassEffect('#my-card');
console.log('Effect removed:', removed);
```

##### `updateGlassEffect(element, options)`

Update existing glassmorphism effect on an element.

```javascript
updateGlassEffect(
  element: Element | string,
  options: Partial<GlassOptions>
): boolean
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| element | `Element \| string` | Yes | Target element or CSS selector |
| options | `Partial<GlassOptions>` | Yes | Options to update |

**Returns:** `true` if effect was updated, `false` if no effect exists.

**Example:**
```javascript
glass.updateGlassEffect('#my-card', {
  intensity: 'light',
  color: 'purple'
});
```

##### `getAllInstances()`

Get all active glass effect instances.

```javascript
getAllInstances(): GlassInstance[]
```

**Returns:** Array of all active `GlassInstance` objects.

##### `destroy()`

Clean up all effects and event listeners.

```javascript
destroy(): void
```

### GlassModal

Class for managing modal dialogs with glassmorphism styling.

#### Static Methods

##### `show(modalId, options)`

Show a modal dialog.

```javascript
static show(
  modalId: string,
  options?: ModalShowOptions
): Promise<GlassModal>
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| modalId | `string` | Yes | Modal element ID |
| options | `ModalShowOptions` | No | Display options |

**Options Object:**

```typescript
interface ModalShowOptions {
  animation?: 'fade' | 'slide' | 'scale' | 'none';
  duration?: number;          // Animation duration (ms)
  backdrop?: boolean;         // Show backdrop
  keyboard?: boolean;         // Close on ESC key
  focus?: boolean;           // Focus modal on show
}
```

**Returns:** Promise resolving to `GlassModal` instance.

**Example:**
```javascript
const modal = await GlassModal.show('my-modal', {
  animation: 'scale',
  duration: 400
});
```

##### `hide(modalId, options)`

Hide a modal dialog.

```javascript
static hide(
  modalId: string,
  options?: ModalHideOptions
): Promise<boolean>
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| modalId | `string` | Yes | Modal element ID |
| options | `ModalHideOptions` | No | Hide options |

**Options Object:**

```typescript
interface ModalHideOptions {
  animation?: 'fade' | 'slide' | 'scale' | 'none';
  duration?: number;
  force?: boolean;           // Force close without validation
}
```

**Returns:** Promise resolving to `true` if hidden, `false` if prevented.

##### `create(content, options)`

Create and show a modal programmatically.

```javascript
static create(
  content: ModalContent,
  options?: ModalCreateOptions
): Promise<GlassModal>
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| content | `ModalContent` | Yes | Modal content configuration |
| options | `ModalCreateOptions` | No | Creation options |

**Content Object:**

```typescript
interface ModalContent {
  title?: string;
  body: string | Element;
  footer?: string | Element;
  buttons?: ModalButton[];
}

interface ModalButton {
  text: string;
  variant?: 'primary' | 'secondary' | 'accent' | 'outline';
  action: string | Function;
  disabled?: boolean;
}
```

**Example:**
```javascript
const modal = await GlassModal.create({
  title: 'Confirm Action',
  body: '<p>Are you sure you want to continue?</p>',
  buttons: [
    { text: 'Cancel', action: 'close', variant: 'secondary' },
    { text: 'Confirm', action: () => handleConfirm(), variant: 'primary' }
  ]
});
```

#### Instance Methods

##### `show(options)`

Show this modal instance.

```javascript
show(options?: ModalShowOptions): Promise<void>
```

##### `hide(options)`

Hide this modal instance.

```javascript
hide(options?: ModalHideOptions): Promise<void>
```

##### `toggle(options)`

Toggle modal visibility.

```javascript
toggle(options?: ModalShowOptions): Promise<void>
```

##### `isVisible()`

Check if modal is currently visible.

```javascript
isVisible(): boolean
```

##### `setContent(content)`

Update modal content.

```javascript
setContent(content: ModalContent): void
```

##### `dispose()`

Completely remove modal from DOM and clean up.

```javascript
dispose(): void
```

### GlassNavigation

Class for managing responsive navigation with glassmorphism styling.

#### Constructor

```javascript
new GlassNavigation(element, options?)
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| element | `Element \| string` | Yes | Navigation element or selector |
| options | `NavigationOptions` | No | Configuration options |

**Options Object:**

```typescript
interface NavigationOptions {
  breakpoint?: number;        // Mobile breakpoint (px)
  animation?: 'slide' | 'fade' | 'scale';
  autoHide?: boolean;        // Hide on scroll
  scrollSpy?: boolean;       // Highlight active section
  offset?: number;           // Scroll spy offset
  duration?: number;         // Animation duration
}
```

#### Methods

##### `show()`

Show navigation menu (mobile).

```javascript
show(): Promise<void>
```

##### `hide()`

Hide navigation menu (mobile).

```javascript
hide(): Promise<void>
```

##### `toggle()`

Toggle navigation menu visibility.

```javascript
toggle(): Promise<void>
```

##### `setActive(element)`

Set active navigation item.

```javascript
setActive(element: Element | string): void
```

**Example:**
```javascript
nav.setActive('#home-link');
```

##### `updateScrollSpy()`

Manually update scroll spy highlighting.

```javascript
updateScrollSpy(): void
```

##### `destroy()`

Clean up navigation instance.

```javascript
destroy(): void
```

### GlassTheme

Static class for managing themes.

#### Static Methods

##### `setTheme(themeName)`

Set the active theme.

```javascript
static setTheme(themeName: string): boolean
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| themeName | `string` | Yes | Theme name to activate |

**Returns:** `true` if theme was set, `false` if theme not found.

##### `getTheme()`

Get current active theme name.

```javascript
static getTheme(): string
```

**Returns:** Current theme name.

##### `registerTheme(name, config)`

Register a custom theme.

```javascript
static registerTheme(
  name: string,
  config: ThemeConfig
): void
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| name | `string` | Yes | Theme name |
| config | `ThemeConfig` | Yes | Theme configuration |

**Theme Configuration:**

```typescript
interface ThemeConfig {
  primary: string;           // Primary glass color
  secondary: string;         // Secondary glass color
  accent: string;           // Accent glass color
  blur: number;             // Default blur amount
  border: string;           // Border color
  shadow: string;           // Shadow configuration
  variables?: Record<string, string>; // CSS custom properties
}
```

**Example:**
```javascript
GlassTheme.registerTheme('ocean', {
  primary: 'rgba(59, 130, 246, 0.1)',
  secondary: 'rgba(16, 185, 129, 0.1)',
  accent: 'rgba(245, 158, 11, 0.1)',
  blur: 12,
  border: 'rgba(59, 130, 246, 0.3)',
  shadow: '0 8px 32px rgba(59, 130, 246, 0.2)',
  variables: {
    '--ocean-wave': '#3B82F6',
    '--ocean-deep': '#1E40AF'
  }
});
```

##### `getAvailableThemes()`

Get list of all available themes.

```javascript
static getAvailableThemes(): string[]
```

**Returns:** Array of theme names.

##### `removeTheme(name)`

Remove a custom theme.

```javascript
static removeTheme(name: string): boolean
```

**Returns:** `true` if theme was removed, `false` if not found.

## Utility Functions

### `isGlassmorphismSupported()`

Check if the browser supports glassmorphism effects.

```javascript
function isGlassmorphismSupported(): boolean
```

**Returns:** `true` if `backdrop-filter` is supported.

**Example:**
```javascript
if (isGlassmorphismSupported()) {
  // Use full glassmorphism
} else {
  // Use fallback styling
}
```

### `generateGlassCSS(options)`

Generate CSS properties for glassmorphism effect.

```javascript
function generateGlassCSS(options: GlassOptions): CSSProperties
```

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| options | `GlassOptions` | Yes | Glass effect options |

**Returns:** Object with CSS properties.

**Example:**
```javascript
const styles = generateGlassCSS({
  intensity: 'medium',
  color: 'blue',
  blur: 10
});

Object.assign(element.style, styles);
```

### `debounce(func, delay)`

Utility function for debouncing function calls.

```javascript
function debounce<T extends (...args: any[]) => any>(
  func: T,
  delay: number
): (...args: Parameters<T>) => void
```

**Example:**
```javascript
const debouncedResize = debounce(() => {
  // Handle resize
}, 100);

window.addEventListener('resize', debouncedResize);
```

### `throttle(func, limit)`

Utility function for throttling function calls.

```javascript
function throttle<T extends (...args: any[]) => any>(
  func: T,
  limit: number
): (...args: Parameters<T>) => void
```

## Configuration Objects

### Global Configuration

```javascript
GlassConfig.set(config: GlobalConfig): void
GlassConfig.get(): GlobalConfig
```

**Global Configuration:**

```typescript
interface GlobalConfig {
  defaultBlur: number;
  defaultOpacity: number;
  animationDuration: number;
  borderRadius: number;
  theme: string;
  fallbackMode: boolean;
  debugMode: boolean;
  prefix: string;              // CSS class prefix
}
```

**Example:**
```javascript
GlassConfig.set({
  defaultBlur: 15,
  defaultOpacity: 0.15,
  animationDuration: 400,
  theme: 'dark',
  debugMode: true
});
```

## Events

### Glass Effect Events

All glassmorphism components emit custom events:

#### `glass:applied`

Fired when a glass effect is applied to an element.

```javascript
element.addEventListener('glass:applied', (event) => {
  console.log('Applied:', event.detail);
});
```

**Event Detail:**
```typescript
interface GlassAppliedDetail {
  element: Element;
  options: GlassOptions;
  instance: GlassInstance;
}
```

#### `glass:removed`

Fired when a glass effect is removed from an element.

```javascript
element.addEventListener('glass:removed', (event) => {
  console.log('Removed:', event.detail);
});
```

#### `glass:updated`

Fired when a glass effect is updated.

```javascript
element.addEventListener('glass:updated', (event) => {
  console.log('Updated:', event.detail);
});
```

### Modal Events

#### `modal:show`

Fired when a modal is shown.

```javascript
document.addEventListener('modal:show', (event) => {
  console.log('Modal shown:', event.detail.modalId);
});
```

#### `modal:hide`

Fired when a modal is hidden.

```javascript
document.addEventListener('modal:hide', (event) => {
  console.log('Modal hidden:', event.detail.modalId);
});
```

#### `modal:beforeShow`

Fired before a modal is shown. Can be cancelled.

```javascript
document.addEventListener('modal:beforeShow', (event) => {
  // Cancel modal showing
  if (shouldPreventModal()) {
    event.preventDefault();
  }
});
```

### Navigation Events

#### `nav:toggle`

Fired when navigation is toggled.

```javascript
document.addEventListener('nav:toggle', (event) => {
  console.log('Navigation toggled:', event.detail.isOpen);
});
```

## CSS Custom Properties

### Core Variables

```css
:root {
  /* Blur effects */
  --glass-blur-light: 5px;
  --glass-blur-medium: 10px;
  --glass-blur-heavy: 20px;
  
  /* Opacity levels */
  --glass-opacity-light: 0.05;
  --glass-opacity-medium: 0.1;
  --glass-opacity-heavy: 0.2;
  
  /* Colors */
  --glass-white: rgba(255, 255, 255, var(--glass-opacity-medium));
  --glass-black: rgba(0, 0, 0, var(--glass-opacity-medium));
  --glass-blue: rgba(59, 130, 246, var(--glass-opacity-medium));
  --glass-purple: rgba(147, 51, 234, var(--glass-opacity-medium));
  --glass-pink: rgba(236, 72, 153, var(--glass-opacity-medium));
  
  /* Borders */
  --glass-border-light: 1px solid rgba(255, 255, 255, 0.1);
  --glass-border-medium: 1px solid rgba(255, 255, 255, 0.2);
  --glass-border-heavy: 2px solid rgba(255, 255, 255, 0.3);
  
  /* Shadows */
  --glass-shadow-light: 0 4px 16px rgba(0, 0, 0, 0.05);
  --glass-shadow-medium: 0 8px 32px rgba(0, 0, 0, 0.1);
  --glass-shadow-heavy: 0 16px 64px rgba(0, 0, 0, 0.2);
  
  /* Border radius */
  --glass-radius-small: 8px;
  --glass-radius-medium: 12px;
  --glass-radius-large: 16px;
  
  /* Transitions */
  --glass-transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  --glass-transition-fast: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);
  --glass-transition-slow: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Component-Specific Variables

#### Card Variables
```css
:root {
  --glass-card-padding: 1.5rem;
  --glass-card-gap: 1rem;
  --glass-card-min-height: 100px;
  --glass-card-hover-transform: translateY(-2px);
}
```

#### Button Variables
```css
:root {
  --glass-button-padding: 0.75rem 1.5rem;
  --glass-button-font-weight: 500;
  --glass-button-hover-scale: 1.02;
}
```

#### Modal Variables
```css
:root {
  --glass-modal-backdrop: rgba(0, 0, 0, 0.5);
  --glass-modal-max-width: 500px;
  --glass-modal-z-index: 1050;
}
```

## TypeScript Definitions

For TypeScript projects, the library includes comprehensive type definitions:

```typescript
// Main library types
declare module 'glassmorphism-web' {
  export class GlassEffects {
    constructor(options?: GlassEffectsOptions);
    init(): Promise<void>;
    applyGlassEffect(element: Element | string, options?: GlassOptions): GlassInstance;
    removeGlassEffect(element: Element | string): boolean;
    updateGlassEffect(element: Element | string, options: Partial<GlassOptions>): boolean;
    getAllInstances(): GlassInstance[];
    destroy(): void;
  }

  export class GlassModal {
    static show(modalId: string, options?: ModalShowOptions): Promise<GlassModal>;
    static hide(modalId: string, options?: ModalHideOptions): Promise<boolean>;
    static create(content: ModalContent, options?: ModalCreateOptions): Promise<GlassModal>;
    
    show(options?: ModalShowOptions): Promise<void>;
    hide(options?: ModalHideOptions): Promise<void>;
    toggle(options?: ModalShowOptions): Promise<void>;
    isVisible(): boolean;
    setContent(content: ModalContent): void;
    dispose(): void;
  }

  export class GlassNavigation {
    constructor(element: Element | string, options?: NavigationOptions);
    show(): Promise<void>;
    hide(): Promise<void>;
    toggle(): Promise<void>;
    setActive(element: Element | string): void;
    updateScrollSpy(): void;
    destroy(): void;
  }

  export class GlassTheme {
    static setTheme(themeName: string): boolean;
    static getTheme(): string;
    static registerTheme(name: string, config: ThemeConfig): void;
    static getAvailableThemes(): string[];
    static removeTheme(name: string): boolean;
  }

  // Utility functions
  export function isGlassmorphismSupported(): boolean;
  export function generateGlassCSS(options: GlassOptions): CSSProperties;
  export function debounce<T extends (...args: any[]) => any>(func: T, delay: number): (...args: Parameters<T>) => void;
  export function throttle<T extends (...args: any[]) => any>(func: T, limit: number): (...args: Parameters<T>) => void;

  // Configuration
  export const GlassConfig: {
    set(config: GlobalConfig): void;
    get(): GlobalConfig;
  };
}
```

---

This API reference provides complete documentation for all public APIs, methods, and configuration options in the Glassmorphism Web Design library.