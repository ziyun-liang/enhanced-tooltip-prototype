# Product Requirements Document (PRD)
# Enhanced Audience Overlap Tooltip 

## Document Information
- **Version:** 1.0
- **Date:** 09/02/2025
- **Status:** Ready for Development
- **Team:** KScope Product Team

## 1. Executive Summary

### 1.1 Project Goal
Enable KScope users to discover valuable audience overlap insights when comparing two Audios or Newsletters.

### 1.2 Success Metrics
TBD

## Feature Specifications

### 1. Interaction Behavior
**Requirement:** Sticky tooltip interaction with safe navigation

- **Trigger:** Mouse hover on any table row
- **Positioning:** Tooltip overlaps source row by 10px (creates safe horizontal navigation corridor)
- **Navigation:** Users can move mouse horizontally within row space to reach tooltip without triggering adjacent rows
- **Close:** Click anywhere outside tooltip or table rows to dismiss
- **Multi-tooltip:** Opening new tooltip automatically closes previous one

### 2. Overlap Label (OVERLAPS Badge)
**Requirement:** Visual indicator for shared audience segments

- **Display:** Only shown for segments that exist in both audience tables
- **Style:** Rounded badge with segment-specific background color
- **Text:** "OVERLAPS" in uppercase, small font weight
- **Colors:** Match overlapped segment colors

### 3. Dotted Line Animation
**Requirement:** Animated connection line between matching segments

- **Trigger:** Appears 400ms after tooltip is shown (for shared segments only)
- **Animation:** Line draws from left table to right table using true line growth (not stroke-dashoffset)
- **Visibility:** Tooltip positioned left (15% from edge) to ensure line animation remains visible in center gap
- **Style:**
  - 1px stroke width
  - stroke-dasharray: 4 3 (dotted pattern)
  - Color matches segment background color
  - Duration: 400ms with ease-in-out-cubic easing
- **End dots:** 4px circles appear after line completes drawing

### 4. Divider Line
**Requirement:** Visual separator in tooltip

- **Position:** Between demo rate section and audience overlap section
- **Style:** 1px solid #e1e1e1
- **Margins:** 16px top, 12px bottom

### 5. Audience Overlap Icon + Title
**Requirement:** Section header with custom icon

- **Icon:** Custom SVG (16x16px)
  ```svg
  <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
    <circle cx="8" cy="8" r="8" fill="#346EB7"/>
    <path d="M4 6L11.7942 10.5" stroke="white" strokeWidth="0.5" strokeLinejoin="round" strokeDasharray="1.2 1.2"/>
         <circle cx="4" cy="6" r="0.5" fill="white" stroke="white"/>
    <circle cx="12" cy="10.5" r="0.5" fill="white" stroke="white"/>
  </svg>
  ```
- **Title:** "Audience Overlap"
- **Style:** 12px font, 600 weight, #346eb7 color
- **Layout:** Icon and title horizontally aligned with 8px gap

### 6. Overlap Number (Percentage)
**Requirement:** Large percentage display

- **Data Source:** Predefined overlap percentages per segment
- **Style:**
  - Font size: 18px
  - Font weight: 700 (bold)
  - Color: #346eb7 (blue)
  - Bottom margin: 4px

### 7. Explanation Text
**Requirement:** Descriptive text explaining the overlap

- **Content:** Dynamic text based on segment name
- **Format:** "of [Segment Name] audience who listen to Ezra Klein also listen to Hard Fork"
- **Style:**
  - Font size: 11px
  - Color: #666666 (gray)
  - Line height: 1.4

## Technical Implementation Notes

### Tooltip Positioning Logic
- Calculate viewport boundaries to ensure tooltip visibility
- Prefer above placement unless insufficient space
- 10px overlap with source row for safe navigation
- Horizontal positioning: 15% from left edge of row (optimized to preserve line animation visibility)
- Tooltip dimensions: min-width 220px, max-width 260px (optimized for gap visibility)