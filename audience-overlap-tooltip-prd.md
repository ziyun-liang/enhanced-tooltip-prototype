# Enhanced Audience Overlap Tooltip - Product Requirements Document

## Overview
Interactive tooltip system for audience segment tables that displays detailed demographic information and cross-audience overlap data with animated visual connections.

## Feature Specifications

### 1. Interaction Behavior
**Requirement**: Sticky tooltip interaction with safe navigation
- **Trigger**: Mouse hover on any table row
- **Positioning**: Tooltip overlaps source row by 10px (creates safe horizontal navigation corridor)
- **Persistence**: Tooltip remains visible until user clicks outside
- **Navigation**: Users can move mouse horizontally within row space to reach tooltip without triggering adjacent rows
- **Close**: Click anywhere outside tooltip or table rows to dismiss
- **Multi-tooltip**: Opening new tooltip automatically closes previous one

### 2. Overlap Label (OVERLAPS Badge)
**Requirement**: Visual indicator for shared audience segments
- **Display**: Only shown for segments that exist in both audience tables
- **Style**: Rounded badge with segment-specific background color
- **Text**: "OVERLAPS" in uppercase, small font weight
- **Colors**: 
  - Tech Industry: `#ccebc5` (light green)
  - Wellness & Self Care: `#fddaec` (light pink)
  - Art Aficionados: `#fbb4ae` (light coral)
  - Fitness and Nutrition: `#decbe4` (light purple)

### 3. Dotted Line Animation
**Requirement**: Animated connection line between matching segments
- **Trigger**: Appears 400ms after tooltip is shown (for shared segments only)
- **Animation**: Line draws from left table to right table using true line growth (not stroke-dashoffset)
- **Visibility**: Tooltip positioned left (15% from edge) to ensure line animation remains visible in center gap
- **Style**: 
  - 1px stroke width
  - `stroke-dasharray: 4 3` (dotted pattern)
  - Color matches segment background color
  - Duration: 400ms with ease-in-out-cubic easing
- **End dots**: 4px circles appear after line completes drawing
- **Implementation**: Use `requestAnimationFrame` to animate `x2,y2` coordinates from start to end position

### 4. Divider Line
**Requirement**: Visual separator in tooltip
- **Position**: Between demo rate section and audience overlap section
- **Style**: 1px solid `#e1e1e1`
- **Margins**: 16px top, 12px bottom

### 5. Audience Overlap Icon + Title
**Requirement**: Section header with custom icon
- **Icon**: Custom SVG (16x16px)
  ```svg
  <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
    <circle cx="8" cy="8" r="8" fill="#346EB7"/>
    <path d="M4 6L11.7942 10.5" stroke="white" strokeWidth="0.5" strokeLinejoin="round" strokeDasharray="1.2 1.2"/>
         <circle cx="4" cy="6" r="0.5" fill="white" stroke="white"/>
    <circle cx="12" cy="10.5" r="0.5" fill="white" stroke="white"/>
  </svg>
  ```
- **Title**: "Audience Overlap"
- **Style**: 12px font, 600 weight, `#346eb7` color
- **Layout**: Icon and title horizontally aligned with 8px gap

### 6. Overlap Number (Percentage)
**Requirement**: Large percentage display
- **Data Source**: Predefined overlap percentages per segment
- **Style**: 
  - Font size: 18px
  - Font weight: 700 (bold)
  - Color: `#346eb7` (blue)
  - Bottom margin: 4px

### 7. Explanation Text
**Requirement**: Descriptive text explaining the overlap
- **Content**: Dynamic text based on segment name
- **Format**: "of [Segment Name] audience who listen to Ezra Klein also listen to Hard Fork"
- **Style**: 
  - Font size: 11px
  - Color: `#666666` (gray)
  - Line height: 1.4

## Data Structure

### Segment Overlap Data
```javascript
const sharedSegments = {
  "Tech Industry": { 
    percentage: 47, 
    description: "of Tech Industry audience who listen to Ezra Klein also listen to Hard Fork" 
  },
  "Wellness & Self Care": { 
    percentage: 23, 
    description: "of Wellness & Self Care audience who listen to Ezra Klein also listen to Hard Fork" 
  },
  "Art Aficionados": { 
    percentage: 31, 
    description: "of Art Aficionados audience who listen to Ezra Klein also listen to Hard Fork" 
  },
  "Fitness and Nutrition": { 
    percentage: 18, 
    description: "of Fitness and Nutrition audience who listen to Ezra Klein also listen to Hard Fork" 
  }
};
```

## Technical Implementation Notes

### Tooltip Positioning Logic
- Calculate viewport boundaries to ensure tooltip visibility
- Prefer above placement unless insufficient space
- 10px overlap with source row for safe navigation
- **Horizontal positioning**: 15% from left edge of row (optimized to preserve line animation visibility)
- **Tooltip dimensions**: min-width 220px, max-width 260px (optimized for gap visibility)

### Performance Considerations
- Use `requestAnimationFrame` for smooth line animations
- Debounce rapid hover events to prevent multiple tooltips
- Clean up event listeners on component unmount
- Optimize SVG rendering for connection lines

### Accessibility
- Ensure tooltip content is keyboard accessible
- Provide appropriate ARIA labels
- Maintain proper color contrast ratios
- Support screen reader navigation

## Browser Support
- Modern browsers with ES6+ support
- SVG animation support required
- CSS transform and transition support required

---

**Author**: Product Team  
**Date**: January 2025  
**Version**: 1.1 - Updated with optimized positioning and dimensions
