# UI/UX Design Specifications

## Design System Overview

### Color Palette

**Primary Colors:**
- Primary Blue: `#0066CC`
- Primary Green: `#00AA44`
- Neutral Gray: `#333333`

**Secondary Colors:**
- Light Blue: `#E6F0FF`
- Light Green: `#E6F9F0`
- Light Gray: `#F5F5F5`
- Border Gray: `#CCCCCC`

**Status Colors:**
- Success: `#00AA44` (Green)
- Warning: `#FFAA00` (Orange)
- Error: `#CC0000` (Red)
- Info: `#0066CC` (Blue)

### Typography

**Font Family:** 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif

**Font Sizes:**
- H1: 32px (bold)
- H2: 24px (bold)
- H3: 20px (bold)
- Body: 14px (regular)
- Small: 12px (regular)
- Caption: 11px (light)

### Spacing

**Margin/Padding Scale:**
- XS: 4px
- S: 8px
- M: 16px
- L: 24px
- XL: 32px
- XXL: 48px

---

## Page Layouts

### 1. Patient Dashboard

```
┌─────────────────────────────────────────────────────────┐
│ Header: Logo | Search | Notifications | Profile Menu    │
├─────────────────────────────────────────────────────────┤
│ Sidebar           │                                      │
│ ├─ Dashboard      │  Main Content Area                   │
│ ├─ Appointments   │  ┌─────────────────────────────────┐ │
│ ├─ Medical Hist   │  │ Welcome John Doe                │ │
│ ├─ Bills          │  │                                 │ │
│ ├─ Profile        │  ┌─────────────┐ ┌──────────────┐ │ │
│ └─ Logout         │  │ Next Appt   │ │ Pending Bill │ │ │
│                   │  │ 15 June     │ │ $150         │ │ │
│                   │  │ Dr. Jane    │ │              │ │ │
│                   │  └─────────────┘ └──────────────┘ │ │
│                   │                                     │ │
│                   │  ┌──────────────────────────────┐ │ │
│                   │  │ Recent Appointments          │ │ │
│                   │  │ [List of past appointments]  │ │ │
│                   │  └──────────────────────────────┘ │ │
│                   └─────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
```

### 2. Appointment Booking

```
┌─────────────────────────────────────────────────────────┐
│ Header                                                   │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  Book an Appointment                                     │
│                                                          │
│  Step 1: Select Specialization                          │
│  ┌──────────────────────────────────┐                   │
│  │ [Cardiology  ▼]                  │                   │
│  └──────────────────────────────────┘                   │
│                                                          │
│  Step 2: Select Doctor                                  │
│  ┌──────────────────────────────────┐                   │
│  │ Dr. Jane Smith (Cardiology)  [>] │                   │
│  │ Dr. John Doe (Cardiology)    [>] │                   │
│  └──────────────────────────────────┘                   │
│                                                          │
│  Step 3: Select Date & Time                             │
│  ┌──────────────┐  ┌──────────────┐                     │
│  │ Date: [___]  │  │ Time: [___]   │                    │
│  └──────────────┘  └──────────────┘                     │
│                                                          │
│  ┌─────────────────┐  ┌──────────────┐                  │
│  │ [ Back ]        │  │ [ Confirm ]  │                  │
│  └─────────────────┘  └──────────────┘                  │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### 3. Doctor Portal

```
┌─────────────────────────────────────────────────────────┐
│ Header                                                   │
├─────────────────────────────────────────────────────────┤
│ Sidebar           │ Main Content                         │
│ ├─ Dashboard      │ ┌──────────────────────────────────┐│
│ ├─ Appointments   │ │ Today's Appointments             ││
│ ├─ Schedule       │ │ 9:00 AM - John Doe  [Details]   ││
│ ├─ Patients       │ │ 10:30 AM - Jane Doe [Details]   ││
│ ├─ Profile        │ │                                  ││
│ └─ Logout         │ │ Patients Pending                 ││
│                   │ │ [List of patients]               ││
│                   │ └──────────────────────────────────┘│
│                   │                                      │
│                   │ ┌──────────────────────────────────┐│
│                   │ │ Schedule Management              ││
│                   │ │ [Calendar View]                  ││
│                   │ └──────────────────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

### 4. Admin Dashboard

```
┌─────────────────────────────────────────────────────────┐
│ Header: Admin Dashboard                                 │
├─────────────────────────────────────────────────────────┤
│ ┌────────────────┐ ┌────────────────┐ ┌────────────────┐│
│ │ Total Patients │ │ Total Doctors  │ │ Total Revenue  ││
│ │ 1,234          │ │ 45             │ │ $25,480        ││
│ └────────────────┘ └────────────────┘ └────────────────┘│
│                                                          │
│ ┌────────────────────────────────────────────────────┐  │
│ │ Appointment Status                                  │  │
│ │ Scheduled: 89  │ Completed: 156  │ Cancelled: 12  │  │
│ └────────────────────────────────────────────────────┘  │
│                                                          │
│ ┌────────────────────────────────────────────────────┐  │
│ │ Revenue Trend (Last 30 Days) [Chart]              │  │
│ └────────────────────────────────────────────────────┘  │
│                                                          │
│ ┌────────────────────────────────────────────────────┐  │
│ │ Recent Activities                                   │  │
│ │ • New patient registered - 2 hours ago             │  │
│ │ • Appointment booked - 1 hour ago                  │  │
│ │ • Payment received - 30 minutes ago                │  │
│ └────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

---

## Component Specifications

### Button Styles

**Primary Button**
- Background: `#0066CC`
- Color: White
- Padding: 10px 20px
- Border-radius: 4px
- Font-weight: Bold

**Secondary Button**
- Background: White
- Color: `#0066CC`
- Border: 2px solid `#0066CC`
- Padding: 10px 20px
- Border-radius: 4px

**Danger Button**
- Background: `#CC0000`
- Color: White
- Padding: 10px 20px
- Border-radius: 4px

### Input Fields

**Text Input**
- Border: 1px solid `#CCCCCC`
- Padding: 10px
- Border-radius: 4px
- Font-size: 14px
- Focus: Blue border `#0066CC`

**Label**
- Font-weight: Bold
- Font-size: 14px
- Color: `#333333`
- Margin-bottom: 5px

### Cards

- Background: White
- Border: 1px solid `#CCCCCC`
- Border-radius: 8px
- Padding: 16px
- Box-shadow: 0 2px 4px rgba(0,0,0,0.1)

---

## Responsive Design

### Breakpoints

- **Mobile:** 320px - 480px
- **Tablet:** 481px - 768px
- **Desktop:** 769px and above

### Mobile Adaptations

- Sidebar collapses to hamburger menu
- Single column layout
- Larger touch targets (44px minimum)
- Full-width buttons and inputs
- Simplified navigation

---

## Accessibility

### WCAG 2.1 Compliance

- **Level AA** minimum compliance
- Color contrast ratio: 4.5:1 for normal text
- Focus indicators visible
- Keyboard navigation support
- ARIA labels for screen readers
- Semantic HTML structure

### Keyboard Navigation

- Tab order logical
- Focus states clearly visible
- Enter/Space to activate buttons
- Arrow keys for navigation where applicable
- Escape to close modals

---

## Animation Guidelines

**Transitions:**
- Duration: 200-300ms
- Easing: ease-in-out

**Hover Effects:**
- Buttons: Darken background by 10%
- Links: Underline on hover
- Cards: Subtle box-shadow increase

---

**Last Updated:** June 1, 2026  
**Designer:** Mubarak Andarabi - Documentation & Design Lead
