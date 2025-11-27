# Employee Task Tracker - Design Guidelines

## Design Approach

**Selected Approach:** Fillo Finance-Inspired Light Theme

**Visual Direction:** Clean, warm, professional dashboard with a light cream/beige background, white cards, and subtle shadows. Emphasis on generous whitespace, consistent rounded corners (rounded-xl to rounded-2xl), and a warm, inviting color palette.

**Core Philosophy:** Create a sophisticated, approachable interface through warm neutrals and soft geometric shapes. Maintain visual hierarchy through subtle color variations and spacing rather than heavy contrast.

---

## Color System

### Light Theme (Default)
- **Background:** Warm cream/beige (`36 33% 96%`)
- **Cards:** Pure white (`0 0% 100%`)
- **Foreground:** Deep charcoal (`24 10% 15%`)
- **Muted:** Light warm gray (`24 8% 50%`)
- **Primary:** Deep charcoal for buttons and interactive elements
- **Accent:** Mint/teal (`155 60% 45%`) for highlights and success states
- **Borders:** Subtle warm gray (`36 20% 88%`)

### Dark Theme
- **Background:** Deep warm gray (`24 10% 10%`)
- **Cards:** Elevated warm gray (`24 10% 14%`)
- **Foreground:** Warm off-white (`36 33% 96%`)
- **Primary:** Mint accent (`155 60% 50%`)
- **Accent:** Same mint for consistency

### Status Colors
- **Success/Accent:** Mint green (`155 60% 45%`)
- **Warning:** Warm orange (`40 90% 55%`)
- **Destructive:** Red (`0 72% 51%`)

---

## Typography System

**Font Family:** Inter via system fonts stack

**Type Scale:**
- Page titles: text-2xl to text-3xl, font-bold, tracking-tight
- Section headings: text-xl to text-2xl, font-semibold
- Card titles: text-base to text-lg, font-semibold
- Body text: text-sm to text-base, font-normal, leading-relaxed
- Secondary text: text-sm, font-medium
- Labels/metadata: text-xs, font-medium, uppercase, tracking-wide
- Sidebar navigation: text-sm, font-medium

---

## Layout System

**Sidebar Navigation:**
- Width: 16rem (256px)
- Background: White (card color)
- Border: Subtle right border
- User profile: Top of sidebar with avatar and name
- Navigation items: rounded-xl, h-11, px-4
- Active state: Muted background with semibold text
- Icons: size-5, consistent spacing

**Main Content Area:**
- Background: Warm cream background
- Container: max-w-7xl, p-8
- Page header: Integrated into main content area
- Section spacing: space-y-6 to space-y-8

**Header:**
- Height: h-16
- Background: Matches main background
- Search bar: Left side with icon
- User profile: Right side with avatar and name dropdown
- Notification button: Accent color background (bg-accent/10, text-accent)

**Spacing Scale (Tailwind):**
Primary values: **3, 4, 6, 8, 10, 12**
- Card internal: p-6
- Section gaps: space-y-6 to space-y-8
- Grid gaps: gap-6
- Component micro-spacing: space-x-3, space-y-2
- Page margins: p-8

---

## Component Library

### Insight Cards (Dashboard)
- Card: bg-card, rounded-2xl, shadow-sm, p-6
- Title: text-base, font-semibold
- Description: text-sm, text-muted-foreground
- Amount: text-2xl, font-bold
- Action link: text-sm with arrow icon
- Border divider between content and action

### Analytics Card
- Container: rounded-2xl, shadow-sm
- Search bar: rounded-xl with icon
- Chart toggle buttons: rounded-xl, grouped
- Chart: Gradient fill with soft colors (mint/orange)

### Data Tables
- Container: rounded-2xl, shadow-sm, overflow-hidden
- Headers: bg-muted/30, text-xs, uppercase, tracking-wide
- Rows: px-6, py-4, hover:bg-muted/20
- Progress bars: rounded-full, h-2

### Task Cards
- Card: rounded-2xl, shadow-sm
- Header: Status badge and quick actions
- Content: Description, assignee, due date
- Footer: Quick status selector

### Filter Panels
- Container: rounded-2xl, shadow-sm, p-4
- Dropdowns: rounded-xl
- Clear button: rounded-lg

### Buttons
- Primary: bg-foreground text-background, rounded-xl
- Outline: border-border, rounded-xl
- Ghost: No background, rounded-xl
- Icon buttons: rounded-xl, consistent sizing

### Forms & Dialogs
- Modal: rounded-2xl, shadow-lg
- Input fields: rounded-xl, border-border
- Labels: text-sm, font-medium

---

## Interactive States

**Hover:** Subtle background elevation using hover-elevate utility
**Active:** Slightly more pronounced with active-elevate-2
**Focus:** Ring with offset, rounded corners match component
**Loading:** Skeleton screens with rounded-2xl placeholders, pulse animation
**Disabled:** Reduced opacity (opacity-50), cursor-not-allowed

---

## Responsive Behavior

**Mobile (<768px):**
- Sidebar: Slide-over drawer
- Stats/task grids: Single column
- Tables: Transform to stacked card views
- Padding: p-6 instead of p-8

**Tablet (768-1024px):**
- Collapsible sidebar (icon-only mode)
- Stats grid: 2 columns
- Task cards: 2 columns

**Desktop (>1024px):**
- Full sidebar
- 3-column grids
- Maximum spaciousness

---

## Tabs Component
- Container: bg-card, rounded-xl, border, p-1
- Tab triggers: rounded-lg, px-4, py-2
- Active state: bg-foreground, text-background
