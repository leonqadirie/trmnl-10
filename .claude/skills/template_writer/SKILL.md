# TRMNL Template Writer Skill

**Skill Name:** `template-writer`
**Trigger:** `/template-writer` or when generating TRMNL e-ink display templates
**Purpose:** Generate production-ready HTML templates for TRMNL e-ink displays

---

## Quick Reference

| View Type | Dimensions | Use Case |
|-----------|------------|----------|
| `full` | 800x480px | Single content displays, dashboards |
| `half_horizontal` | 800x240px | Two stacked panels (top/bottom) |
| `half_vertical` | 400x480px | Two side-by-side panels (left/right) |
| `quadrant` | 400x240px | Four-panel grid layouts |

---

## Table of Contents

1. [View Types](#view-types)
2. [Base Template Structure](#base-template-structure)
3. [Layout Components](#layout-components)
4. [Typography Components](#typography-components)
5. [Content Components](#content-components)
6. [Visual Components](#visual-components)
7. [Utility Classes](#utility-classes)
8. [Data Attributes](#data-attributes)
9. [Responsive System](#responsive-system)
10. [Size Progression Tables](#size-progression-tables)
11. [Complete Examples](#complete-examples)
12. [Best Practices](#best-practices)

---

<view-types>
## View Types

### Full View (800x480px)

The full view occupies the entire screen. Use for single-focus content like dashboards, quotes, or detailed information displays.

**Content Capacity:**
- Up to 20 clamped lines of text
- 320px max content height (with title bar)
- Best for: single large value, text content, charts, detailed lists

**Base Structure:**
```html
<div class="view view--full">
  <div class="layout">
    <!-- Your content here -->
  </div>

  <div class="title_bar">
    <img class="image" src="/images/plugins/your-plugin--render.svg">
    <span class="title">Plugin Name</span>
    <span class="instance">Instance Label</span>
  </div>
</div>
```

### Half Horizontal View (800x240px)

Two views stacked vertically (top and bottom). Each panel is 800px wide and 240px tall.

**Content Capacity:**
- Up to 9 clamped lines of text
- 144px max content height (with title bar)
- Best for: summary stats, compact lists, paired comparisons

**Base Structure:**
```html
<div class="view view--half_horizontal">
  <div class="layout">
    <!-- Your content here -->
  </div>

  <div class="title_bar">
    <img class="image" src="/images/plugins/your-plugin--render.svg">
    <span class="title">Plugin Name</span>
    <span class="instance">Instance Label</span>
  </div>
</div>
```

### Half Vertical View (400x480px)

Two views side by side (left and right). Each panel is 400px wide and 480px tall.

**Content Capacity:**
- Up to 23 clamped lines of text
- 368px max content height (with title bar)
- Best for: tall lists, vertical metrics, side-by-side comparisons

**Base Structure:**
```html
<div class="view view--half_vertical">
  <div class="layout">
    <!-- Your content here -->
  </div>

  <div class="title_bar">
    <img class="image" src="/images/plugins/your-plugin--render.svg">
    <span class="title">Plugin Name</span>
    <span class="instance">Instance Label</span>
  </div>
</div>
```

### Quadrant View (400x240px)

Four views in a 2x2 grid. Each panel is 400px wide and 240px tall.

**Content Capacity:**
- Up to 9 clamped lines of text
- 144px max content height (with title bar)
- Best for: single metrics, mini dashboards, status indicators

**Base Structure:**
```html
<div class="view view--quadrant">
  <div class="layout">
    <!-- Your content here -->
  </div>

  <div class="title_bar">
    <img class="image" src="/images/plugins/your-plugin--render.svg">
    <span class="title">Plugin Name</span>
    <span class="instance">Instance Label</span>
  </div>
</div>
```
</view-types>

---

<base-template-structure>
## Base Template Structure

Every TRMNL template follows this hierarchy:

```
view (container with size modifier)
├── layout (content container with direction/alignment)
│   └── [content components]
└── title_bar (optional footer with icon/title/instance)
```

**Important Notes:**
- In the TRMNL markup editor, you do NOT need to wrap content with `view view--{{size}}` classes
- The `layout` and `title_bar` are sufficient for any layout
- Always place `title_bar` at the end (it renders at the bottom)

### Minimal Template (Markup Editor)

```html
<div class="layout layout--col gap">
  <!-- Your content here -->
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/trmnl--render.svg">
  <span class="title">Title</span>
  <span class="instance">Instance</span>
</div>
```

### Full Template (Development)

```html
<div class="view view--full">
  <div class="layout layout--col gap">
    <!-- Your content here -->
  </div>

  <div class="title_bar">
    <img class="image" src="/images/plugins/trmnl--render.svg">
    <span class="title">Title</span>
    <span class="instance">Instance</span>
  </div>
</div>
```
</base-template-structure>

---

<layout-components>
## Layout Components

### Layout

The primary container for content. Always start with a `layout` element inside your view.

**Direction Modifiers:**
- `layout--row` - Horizontal arrangement (left to right)
- `layout--col` - Vertical arrangement (top to bottom)

**Horizontal Alignment:**
- `layout--left` - Align items to the left
- `layout--center-x` - Center items horizontally
- `layout--right` - Align items to the right

**Vertical Alignment:**
- `layout--top` - Align items to the top
- `layout--center-y` - Center items vertically
- `layout--bottom` - Align items to the bottom

**Combined Alignment:**
- `layout--center` - Center both horizontally and vertically

**Stretch Modifiers:**
- `layout--stretch` - Stretch children in both directions
- `layout--stretch-x` - Stretch children horizontally
- `layout--stretch-y` - Stretch children vertically

**Examples:**

```html
<!-- Horizontal row, left-aligned -->
<div class="layout layout--row layout--left gap">
  <span class="label">Item 1</span>
  <span class="label">Item 2</span>
</div>

<!-- Vertical column, centered -->
<div class="layout layout--col layout--center gap">
  <span class="value value--large">42</span>
  <span class="label">Total Count</span>
</div>

<!-- Full stretch for equal-width children -->
<div class="layout layout--row layout--stretch gap">
  <div class="flex flex--center bg--gray-65 p--2.5 rounded">Col 1</div>
  <div class="flex flex--center bg--gray-65 p--2.5 rounded">Col 2</div>
</div>
```

### Columns

Multi-column layout system for distributing content across horizontal sections.

```html
<div class="columns">
  <div class="column">
    <!-- Column 1 content -->
  </div>
  <div class="column">
    <!-- Column 2 content -->
  </div>
  <div class="column">
    <!-- Column 3 content -->
  </div>
</div>
```

**With gap spacing:**
```html
<div class="columns gap">
  <div class="column gap">
    <div class="item">...</div>
    <div class="item">...</div>
  </div>
  <div class="column gap">
    <div class="item">...</div>
  </div>
</div>
```

### Grid

CSS Grid-based layout for more complex arrangements.

**Column Definition:**
- `grid--cols-1` through `grid--cols-12` - Set number of columns

**Column Spanning:**
- `col--span-1` through `col--span-12` - Span multiple columns

```html
<div class="grid grid--cols-3 gap">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>

<!-- With column spanning -->
<div class="grid grid--cols-4 gap">
  <div class="item col--span-2">Wide Item</div>
  <div class="item col--span-1">Item</div>
  <div class="item col--span-1">Item</div>
</div>
```

### Flex

Flexible box layout for dynamic content arrangement.

**Direction:**
- `flex--row` - Horizontal arrangement
- `flex--col` - Vertical arrangement

**Alignment:**
- `flex--left`, `flex--center-x`, `flex--right` - Horizontal
- `flex--top`, `flex--center-y`, `flex--bottom` - Vertical
- `flex--center` - Both axes

```html
<div class="flex flex--row flex--center gap">
  <span class="label">Tag 1</span>
  <span class="label">Tag 2</span>
</div>

<div class="flex flex--col flex--center gap--small">
  <span class="value value--large">99%</span>
  <span class="label">Completion</span>
</div>
```
</layout-components>

---

<typography-components>
## Typography Components

### Title

Main headings and section titles.

**Sizes:**
- `title` or `title--base` - Default size
- `title--small` - Smaller title

```html
<span class="title">Main Heading</span>
<span class="title title--small">Subheading</span>
```

### Value

Large numeric or text displays. Perfect for metrics, stats, and key figures.

**Sizes (smallest to largest):**
- `value--xxsmall`
- `value--xsmall`
- `value--small`
- `value` or `value--base` - Default
- `value--large`
- `value--xlarge`
- `value--xxlarge`
- `value--xxxlarge`

**Modifiers:**
- `value--tnums` - Tabular numerals (fixed-width digits for alignment)

```html
<span class="value value--xxxlarge value--tnums">$1,234.56</span>
<span class="value value--large">42</span>
<span class="value value--small value--tnums">+15.3%</span>
```

**Responsive Example:**
```html
<span class="value value--small md:value--large lg:value--xlarge value--tnums">
  1,234.56
</span>
```

### Label

Text labels for metadata, tags, and descriptive content.

**Sizes:**
- `label` or `label--base` - Default size
- `label--small` - Smaller label

**Variants:**
- Default (solid background implied)
- `label--outline` - Border only
- `label--underline` - Underline style
- `label--gray` - Grayed out appearance
- `label--inverted` - Inverted colors

```html
<span class="label">Default Label</span>
<span class="label label--outline">Outline</span>
<span class="label label--underline">Underline</span>
<span class="label label--gray">Gray</span>
<span class="label label--inverted">Inverted</span>

<!-- Small variants -->
<span class="label label--small">Small Label</span>
<span class="label label--small label--underline">Small Underline</span>
```

### Description

Secondary text content for supporting information.

```html
<span class="description">This is descriptive text that provides additional context.</span>
```

### Text Alignment

Apply to any text element:

```html
<span class="label text--left">Left aligned</span>
<span class="label text--center">Center aligned</span>
<span class="label text--right">Right aligned</span>
```
</typography-components>

---

<content-components>
## Content Components

### Title Bar

Footer component with plugin icon, title, and optional instance label.

```html
<div class="title_bar">
  <img class="image" src="/images/plugins/plugin-name--render.svg">
  <span class="title">Plugin Title</span>
  <span class="instance">Instance Name</span>
</div>
```

**Without instance:**
```html
<div class="title_bar">
  <img class="image" src="/images/plugins/plugin-name--render.svg">
  <span class="title">Plugin Title</span>
</div>
```

### Item

Structured content block with optional meta section and content area.

**Basic Item (no meta):**
```html
<div class="item">
  <div class="content">
    <span class="title title--small">Item Title</span>
    <span class="description">Item description text</span>
    <div class="flex gap--small">
      <span class="label label--small label--underline">Tag 1</span>
      <span class="label label--small label--underline">Tag 2</span>
    </div>
  </div>
</div>
```

**Item with Meta Bar:**
```html
<div class="item">
  <div class="meta"></div>
  <div class="content">
    <span class="title title--small">Item Title</span>
    <span class="description">Item description</span>
  </div>
</div>
```

**Item with Meta and Index:**
```html
<div class="item">
  <div class="meta">
    <span class="index">1</span>
  </div>
  <div class="content">
    <span class="title title--small">First Item</span>
    <span class="description">Description here</span>
  </div>
</div>
```

**Item with Emphasis (darker meta bar):**
- `item--emphasis-1` - Default emphasis
- `item--emphasis-2` - Medium emphasis
- `item--emphasis-3` - Strong emphasis

```html
<div class="item item--emphasis-3">
  <div class="meta"></div>
  <div class="content">
    <span class="title title--small">Important Item</span>
    <span class="description">High priority content</span>
  </div>
</div>
```

### Table

Standard HTML tables with TRMNL styling.

**Basic Table:**
```html
<table class="table" data-table-limit="true">
  <thead>
    <tr>
      <th><span class="title title--small text--gray-45">Header 1</span></th>
      <th><span class="title title--small text--gray-45">Header 2</span></th>
      <th><span class="title title--small text--gray-45">Header 3</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><span class="label">Cell 1</span></td>
      <td><span class="label label--small">Cell 2</span></td>
      <td><span class="label label--small" data-clamp="1">Long text...</span></td>
    </tr>
  </tbody>
</table>
```

**Indexed Table:**
```html
<table class="table table--indexed" data-table-limit="true">
  <thead>
    <tr>
      <th></th>
      <th><span class="title title--small text--gray-45">Name</span></th>
      <th><span class="title title--small text--gray-45">Value</span></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><span class="meta"><span class="index">1</span></span></td>
      <td><span class="label">Item Name</span></td>
      <td><span class="label label--small">$100</span></td>
    </tr>
  </tbody>
</table>
```

**Table Sizes:**
- `table` or `table--base` - Default
- `table--large` - Larger row heights
- `table--small` - Compact rows
- `table--xsmall` - Most compact

### Rich Text

Container for formatted text content with automatic sizing and clamping.

```html
<div class="richtext richtext--center gap--large">
  <div class="content content--center text--center" data-content-limiter="true">
    <p>Your rich text content here. This will automatically adjust
    size when it exceeds the available space.</p>
  </div>
</div>
```

**Alignment Options:**
- `richtext--left`, `richtext--center`, `richtext--right` - Container alignment
- `content--left`, `content--center`, `content--right` - Content block alignment
- `text--left`, `text--center`, `text--right` - Text alignment

**Content Sizes:**
- `content--large` - Larger text
- `content` or `content--base` - Default
- `content--small` - Smaller text

### Progress Bar

Visual progress indicator with fill track.

```html
<div class="progress-bar">
  <div class="content">
    <span class="label">Progress Label</span>
    <span class="label">75%</span>
  </div>
  <div class="track">
    <div class="fill" style="width: 75%"></div>
  </div>
</div>
```

**Sizes:**
- `progress-bar--small`
- `progress-bar` or `progress-bar--base`
- `progress-bar--large`

**Emphasis:**
- Default
- `progress-bar--emphasis-2`
- `progress-bar--emphasis-3`

### Progress Dots

Step indicator with discrete dots.

```html
<div class="progress-dots">
  <div class="content">
    <span class="label label--small">Step 3 of 5</span>
  </div>
  <div class="track">
    <div class="dot dot--filled"></div>
    <div class="dot dot--filled"></div>
    <div class="dot dot--current"></div>
    <div class="dot"></div>
    <div class="dot"></div>
  </div>
</div>
```

**Dot States:**
- `dot--filled` - Completed step
- `dot--current` - Current step
- `dot` (no modifier) - Upcoming step

### Divider

Visual separator between content sections.

```html
<div class="divider"></div>
```
</content-components>

---

<visual-components>
## Visual Components

### Image

Display images with various fitting options.

**Fit Modes:**
- `image--fill` - Stretch to fill, may distort
- `image--contain` - Fit within bounds, maintain aspect ratio
- `image--cover` - Fill and crop, maintain aspect ratio

**Dithering:**
- `image-dither` - Apply dithering for better e-ink appearance

```html
<img class="image image--contain" src="/path/to/image.png">
<img class="image image--cover image-dither" src="/path/to/photo.jpg">
```

**Aspect Ratios:**
```html
<div class="aspect--1/1">
  <img class="image image--cover" src="/path/to/image.jpg">
</div>

<div class="aspect--16/9">
  <img class="image image--cover" src="/path/to/image.jpg">
</div>
```

### Chart (Highcharts)

For charts, use Highcharts with animation disabled.

**Required Scripts:**
```html
<script src="https://usetrmnl.com/js/highcharts/12.3.0/highcharts.js"></script>
<script src="https://usetrmnl.com/js/chartkick/5.0.1/chartkick.min.js"></script>
```

**Important Chart Settings:**
- Always disable animation: `animation: false`
- Use black color palette: `colors: ["black"]`
- Set appropriate height based on view type

**Chart Container:**
```html
<div id="chart-unique-id" class="w--full"></div>
```

**Basic Line Chart:**
```javascript
Chartkick.LineChart("chart-unique-id", data, {
  adapter: "highcharts",
  colors: ["black"],
  curve: true,
  library: {
    chart: { height: 260 },
    plotOptions: {
      series: { animation: false, lineWidth: 4 }
    }
  }
});
```

### Borders

Horizontal and vertical border lines with grayscale values.

**Horizontal Borders:**
- `border--h-1` (black) through `border--h-7` (white)

**Vertical Borders:**
- `border--v-1` (black) through `border--v-7` (white)

```html
<div class="border--h-5 w--full"></div>
<div class="border--v-3 h--full"></div>
```
</visual-components>

---

<utility-classes>
## Utility Classes

### Gap (Spacing Between Items)

**Predefined Sizes:**
- `gap--none` - No gap
- `gap--xsmall` - Extra small
- `gap--small` - Small
- `gap` or `gap--base` - Default
- `gap--medium` - Medium
- `gap--large` - Large
- `gap--xlarge` - Extra large
- `gap--xxlarge` - Extra extra large

**Distribution:**
- `gap--auto` - Distribute space evenly (push to edges)
- `gap--space-between` - Space between items

**Arbitrary Values (0-50px, no responsive):**
- `gap--[10px]`, `gap--[25px]`, etc.

```html
<div class="layout layout--col gap--large">...</div>
<div class="flex flex--row gap--small">...</div>
<div class="grid grid--cols-3 gap--[20px]">...</div>
```

### Size (Width & Height)

**Predefined Values (in increments of 4px):**
- `w--0`, `w--1`, `w--2` ... `w--96`
- `h--0`, `h--1`, `h--2` ... `h--96`

**Common Values:**
- `w--4` = 16px
- `w--12` = 48px
- `w--24` = 96px
- `w--48` = 192px
- `w--64` = 256px

**Special Values:**
- `w--full` / `h--full` - 100%
- `w--auto` / `h--auto` - Auto
- `w--min-{size}` / `w--max-{size}` - Min/max width
- `h--min-{size}` / `h--max-{size}` - Min/max height

**Arbitrary Values (0-800px):**
- `w--[250px]`, `h--[180px]`, etc.

```html
<div class="w--full h--48">...</div>
<div class="w--[300px] h--[200px]">...</div>
<div class="w--max-72">...</div>
```

### Padding

**All Sides:**
- `p--0`, `p--1`, `p--2`, `p--2.5`, `p--3` ... `p--12`

**Directional:**
- `pt--{size}` - Top
- `pr--{size}` - Right
- `pb--{size}` - Bottom
- `pl--{size}` - Left
- `px--{size}` - Horizontal (left & right)
- `py--{size}` - Vertical (top & bottom)

```html
<div class="p--4">All sides padding</div>
<div class="px--2.5 py--4">Horizontal and vertical</div>
<div class="pt--2 pb--4">Top and bottom</div>
```

### Margin

**Same pattern as padding:**
- `m--{size}`, `mt--`, `mr--`, `mb--`, `ml--`, `mx--`, `my--`

```html
<div class="mb--4">Bottom margin</div>
<div class="mx--auto">Auto horizontal (centering)</div>
```

### Background Colors

16 grayscale shades from black to white:

- `bg--black`
- `bg--gray-10` through `bg--gray-75` (in increments of 5)
- `bg--white`

**With bit-depth adaptation:**
```html
<div class="bg--gray-65 2bit:bg--gray-75 4bit:bg--gray-70">
  Adapts to display capabilities
</div>
```

### Text Colors

Same grayscale system:
- `text--black`
- `text--gray-10` through `text--gray-75`
- `text--white`

```html
<span class="title text--gray-45">Grayed Title</span>
```

### Rounded Corners

**Predefined Sizes:**
- `rounded--none` - 0px
- `rounded--xsmall` - 5px
- `rounded--small` - 7px
- `rounded` - 10px (default)
- `rounded--medium` - 15px
- `rounded--large` - 20px
- `rounded--xlarge` - 25px
- `rounded--xxlarge` - 30px
- `rounded--full` - 9999px (pill shape)

```html
<div class="bg--gray-65 p--4 rounded--medium">Rounded box</div>
<div class="bg--black p--2 rounded--full">Pill</div>
```
</utility-classes>

---

<data-attributes>
## Data Attributes

### Text Clamping

Limit text to a specific number of lines with ellipsis.

```html
<span class="label" data-clamp="1">Single line with ellipsis...</span>
<span class="label" data-clamp="2">Two lines maximum...</span>
<span class="description" data-clamp="3">Three lines of text...</span>
```

### Content Limiter

Automatically resize content to fit available space.

```html
<div class="content" data-content-limiter="true">
  <p>This content will automatically adjust size when it exceeds
  the available height.</p>
</div>
```

**With custom max height:**
```html
<div class="content" data-content-limiter="true" data-content-max-height="140">
  <p>Custom height threshold of 140px.</p>
</div>
```

### Table Limit

Enable automatic row limiting for tables.

```html
<table class="table" data-table-limit="true">
  <!-- Rows beyond available space show "and X more" -->
</table>
```

### Pixel Perfect

Ensure crisp text rendering on 1-bit displays.

```html
<div class="content" data-pixel-perfect="true">
  <p>Crisp, pixel-aligned text.</p>
</div>
```

### List Overflow

Control list overflow behavior:

```html
<div class="columns" data-overflow-max-cols="3">
  <!-- Maximum 3 columns, overflow handled -->
</div>
```
</data-attributes>

---

<responsive-system>
## Responsive System

TRMNL supports three types of responsive modifiers:

### Size-Based Breakpoints

- `sm:` - Small screens
- `md:` - Medium screens
- `lg:` - Large screens
- `xl:` - Extra large screens

```html
<span class="value value--small md:value--large lg:value--xlarge">
  Responsive sizing
</span>

<div class="grid grid--cols-1 md:grid--cols-2 lg:grid--cols-3 gap">
  <!-- Responsive grid -->
</div>
```

### Orientation-Based

- `portrait:` - Portrait orientation
- `landscape:` - Landscape orientation

```html
<span class="label portrait:label--small landscape:label--base">
  Orientation-aware label
</span>

<div class="layout layout--col portrait:layout--row">
  <!-- Column in landscape, row in portrait -->
</div>
```

### Bit-Depth Based

Optimize for different display color depths:

- `1bit:` - 1-bit displays (black/white only)
- `2bit:` - 2-bit displays (4 grayscale levels)
- `4bit:` - 4-bit displays (16 grayscale levels)

```html
<div class="bg--gray-65 2bit:bg--gray-75 4bit:bg--gray-70">
  Optimized background per bit-depth
</div>

<span class="label 1bit:label--inverted 2bit:label--outline 4bit:label--underline">
  Adaptive label style
</span>
```

### Combined Modifiers

Combine multiple responsive systems:

```html
<span class="label md:portrait:2bit:label--inverted lg:4bit:label--outline">
  Complex responsive targeting
</span>
```

**Order of specificity:** `size:orientation:bit-depth:class`
</responsive-system>

---

<size-progression-tables>
## Size Progression Tables

### View Dimensions

| View Type | Width | Height | Content Height (with title bar) |
|-----------|-------|--------|--------------------------------|
| Full | 800px | 480px | ~320px |
| Half Horizontal | 800px | 240px | ~144px |
| Half Vertical | 400px | 480px | ~368px |
| Quadrant | 400px | 240px | ~144px |

### Recommended Value Sizes by View

| View Type | Primary Value | Secondary Value | Label |
|-----------|--------------|-----------------|-------|
| Full | `value--xxxlarge` | `value--large` | `label` |
| Half Horizontal | `value--xlarge` | `value--small` | `label--small` |
| Half Vertical | `value--xxlarge` | `value--base` | `label` |
| Quadrant | `value--large` | `value--xsmall` | `label--small` |

### Text Clamping by View

| View Type | Recommended Max Lines | data-clamp Value |
|-----------|----------------------|------------------|
| Full | 20 lines | `data-clamp="20"` |
| Half Horizontal | 9 lines | `data-clamp="9"` |
| Half Vertical | 23 lines | `data-clamp="23"` |
| Quadrant | 9 lines | `data-clamp="9"` |

### Chart Heights by View

| View Type | Recommended Chart Height |
|-----------|-------------------------|
| Full | 260px |
| Half Horizontal | 120-150px |
| Half Vertical | 200px |
| Quadrant | 60-80px |

### Gap Sizes

| Class | Pixel Value |
|-------|-------------|
| `gap--none` | 0px |
| `gap--xsmall` | 4px |
| `gap--small` | 8px |
| `gap` / `gap--base` | 12px |
| `gap--medium` | 16px |
| `gap--large` | 24px |
| `gap--xlarge` | 32px |
| `gap--xxlarge` | 48px |
</size-progression-tables>

---

<complete-examples>
## Complete Examples

### Example 1: Single Value Display (Full View)

Perfect for displaying one key metric prominently.

```html
<div class="layout layout--col layout--center gap">
  <span class="value value--xxxlarge value--tnums">$42,857</span>
  <span class="title">Total Revenue</span>
  <span class="label label--small label--underline">+12.5% from last month</span>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/analytics--render.svg">
  <span class="title">Analytics</span>
  <span class="instance">Monthly</span>
</div>
```

### Example 2: Stats Grid (Full View)

Multiple metrics in a grid layout.

```html
<div class="layout">
  <div class="grid grid--cols-3 gap--large">
    <div class="item">
      <div class="meta"></div>
      <div class="content">
        <span class="value value--large value--tnums">25,388</span>
        <span class="label">Pageviews</span>
      </div>
    </div>
    <div class="item">
      <div class="meta"></div>
      <div class="content">
        <span class="value value--large value--tnums">4,771</span>
        <span class="label">Visitors</span>
      </div>
    </div>
    <div class="item">
      <div class="meta"></div>
      <div class="content">
        <span class="value value--large value--tnums">2.23</span>
        <span class="label">Avg. Time (min)</span>
      </div>
    </div>
  </div>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/simple-analytics--render.svg">
  <span class="title">Simple Analytics</span>
  <span class="instance">usetrmnl.com</span>
</div>
```

### Example 3: List with Items (Full View)

Event list with meta bars and content.

```html
<div class="layout layout--top">
  <div class="columns">
    <div class="column">
      <div class="item">
        <div class="meta">
          <span class="index">1</span>
        </div>
        <div class="content">
          <span class="title title--small">Team Meeting</span>
          <span class="description">Weekly team sync-up</span>
          <div class="flex gap--small">
            <span class="label label--small label--underline">9:00 AM</span>
            <span class="label label--small label--underline">Confirmed</span>
          </div>
        </div>
      </div>
      <div class="item">
        <div class="meta">
          <span class="index">2</span>
        </div>
        <div class="content">
          <span class="title title--small">Client Presentation</span>
          <span class="description">Q4 review with XYZ Corp</span>
          <div class="flex gap--small">
            <span class="label label--small label--underline">2:00 PM</span>
            <span class="label label--small label--underline">Tentative</span>
          </div>
        </div>
      </div>
    </div>
    <div class="column">
      <div class="item">
        <div class="meta">
          <span class="index">3</span>
        </div>
        <div class="content">
          <span class="title title--small">Code Review</span>
          <span class="description">PR reviews for Project Beta</span>
          <div class="flex gap--small">
            <span class="label label--small label--underline">3:30 PM</span>
          </div>
        </div>
      </div>
      <div class="item">
        <div class="meta">
          <span class="index">4</span>
        </div>
        <div class="content">
          <span class="title title--small">Project Deadline</span>
          <span class="description">Submit final deliverables</span>
          <div class="flex gap--small">
            <span class="label label--small label--underline">11:59 PM</span>
            <span class="label label--small label--underline">Important</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/google-calendar--render.svg">
  <span class="title">Google Calendar</span>
  <span class="instance">Today</span>
</div>
```

### Example 4: Table Display (Full View)

Data table with overflow handling.

```html
<div class="layout">
  <table class="table table--indexed" data-table-limit="true">
    <thead>
      <tr>
        <th></th>
        <th><span class="title title--small text--gray-45">Stock</span></th>
        <th><span class="title title--small text--gray-45">Price</span></th>
        <th><span class="title title--small text--gray-45">Change</span></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><span class="meta"><span class="index">1</span></span></td>
        <td><span class="label">AAPL</span></td>
        <td><span class="label label--small">$178.72</span></td>
        <td><span class="label label--small">+2.34%</span></td>
      </tr>
      <tr>
        <td><span class="meta"><span class="index">2</span></span></td>
        <td><span class="label">GOOGL</span></td>
        <td><span class="label label--small">$141.80</span></td>
        <td><span class="label label--small">-0.52%</span></td>
      </tr>
      <tr>
        <td><span class="meta"><span class="index">3</span></span></td>
        <td><span class="label">MSFT</span></td>
        <td><span class="label label--small">$378.91</span></td>
        <td><span class="label label--small">+1.12%</span></td>
      </tr>
    </tbody>
  </table>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/stock-price--render.svg">
  <span class="title">Stock Prices</span>
  <span class="instance">Portfolio</span>
</div>
```

### Example 5: Rich Text Quote (Full View)

Centered text content with automatic sizing.

```html
<div class="layout">
  <div class="richtext richtext--center gap--large">
    <div class="content content--center text--center" data-content-limiter="true">
      <p>"The only way to do great work is to love what you do. If you haven't
      found it yet, keep looking. Don't settle."</p>
      <p>— Steve Jobs</p>
    </div>
  </div>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/motivational-quote--render.svg">
  <span class="title">Daily Quote</span>
  <span class="instance">Inspiration</span>
</div>
```

### Example 6: Compact Stats (Quadrant View)

Single metric for small quadrant display.

```html
<div class="layout layout--col layout--center gap--small">
  <span class="value value--large value--tnums">72°F</span>
  <span class="title title--small">Sunny</span>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/weather--render.svg">
  <span class="title">Weather</span>
  <span class="instance">San Francisco</span>
</div>
```

### Example 7: Progress Tracking (Half Horizontal)

Progress bar with supporting metrics.

```html
<div class="layout layout--col gap--space-between">
  <div class="flex flex--row gap--large">
    <div class="item">
      <div class="meta"></div>
      <div class="content">
        <span class="value value--small value--tnums">15</span>
        <span class="label label--small">Completed</span>
      </div>
    </div>
    <div class="item">
      <div class="meta"></div>
      <div class="content">
        <span class="value value--small value--tnums">5</span>
        <span class="label label--small">Remaining</span>
      </div>
    </div>
  </div>

  <div class="progress-bar w--full">
    <div class="content">
      <span class="label">Sprint Progress</span>
      <span class="label">75%</span>
    </div>
    <div class="track">
      <div class="fill" style="width: 75%"></div>
    </div>
  </div>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/todoist--render.svg">
  <span class="title">Todoist</span>
  <span class="instance">Current Sprint</span>
</div>
```

### Example 8: Side-by-Side Metrics (Half Vertical)

Two columns of related data.

```html
<div class="layout layout--col gap--space-between">
  <div class="item">
    <div class="meta"></div>
    <div class="content">
      <span class="value value--xlarge value--tnums">$12,450</span>
      <span class="label">Today's Sales</span>
    </div>
  </div>

  <div class="divider"></div>

  <div class="item">
    <div class="meta"></div>
    <div class="content">
      <span class="value value--large value--tnums">156</span>
      <span class="label">Orders</span>
    </div>
  </div>

  <div class="divider"></div>

  <div class="item">
    <div class="meta"></div>
    <div class="content">
      <span class="value value--large value--tnums">$79.81</span>
      <span class="label">Avg. Order Value</span>
    </div>
  </div>
</div>

<div class="title_bar">
  <img class="image" src="/images/plugins/shopify--render.svg">
  <span class="title">Shopify</span>
  <span class="instance">Today</span>
</div>
```
</complete-examples>

---

<best-practices>
## Best Practices

### E-ink Optimization

1. **Use high contrast**: Prefer black text on white backgrounds or white text on black backgrounds
2. **Avoid thin lines**: Use `border--h-3` or darker for visible borders
3. **Disable animations**: Always set `animation: false` in charts
4. **Test bit-depth variants**: Your design should work on 1-bit, 2-bit, and 4-bit displays
5. **Use dithered backgrounds**: Apply `bg--gray-65 2bit:bg--gray-75 4bit:bg--gray-70` for consistent appearance

### Content Sizing

1. **Scale values appropriately**: Use smaller value sizes for smaller views
2. **Clamp long text**: Always use `data-clamp` on text that might overflow
3. **Use content limiter**: Add `data-content-limiter="true"` for dynamic content
4. **Test with real data**: Ensure your template works with varying content lengths

### Layout Best Practices

1. **Start with layout**: Always wrap content in a `layout` element
2. **Use semantic gaps**: Choose gap sizes that reflect content hierarchy
3. **Align consistently**: Pick an alignment strategy and stick with it
4. **Test all view sizes**: Ensure your design works across all four view types

### Common Patterns

**Stats Display:**
```html
<div class="item">
  <div class="meta"></div>
  <div class="content">
    <span class="value value--tnums">123</span>
    <span class="label">Metric Name</span>
  </div>
</div>
```

**Tag Group:**
```html
<div class="flex gap--small">
  <span class="label label--small label--underline">Tag 1</span>
  <span class="label label--small label--underline">Tag 2</span>
</div>
```

**Two-Column Layout:**
```html
<div class="columns gap">
  <div class="column gap">...</div>
  <div class="column gap">...</div>
</div>
```

### Things to Avoid

1. **Don't use animations**: E-ink displays refresh slowly
2. **Don't rely on color**: Use grayscale patterns for differentiation
3. **Don't use very light grays**: They may not render on 1-bit displays
4. **Don't nest layouts excessively**: Keep structure shallow for performance
5. **Don't forget the title bar**: It provides essential context for users
</best-practices>

---

## Additional Resources

- Framework Documentation: `https://trmnl.com/framework/docs`
- Layout Examples: `https://trmnl.com/framework/examples`

---

*This skill file was generated for TRMNL template development. For the most up-to-date documentation, refer to the framework documentation in the codebase.*
