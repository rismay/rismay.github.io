# CommonSwift Brand Identity

@Metadata {
  @PageImage(purpose: icon, source: "brands-common-swift-brand-identity-icon", alt: "CommonSwift Brand Identity icon")
  @PageImage(purpose: card, source: "brands-common-swift-brand-identity-card", alt: "CommonSwift Brand Identity card")
  @PageKind(article)
  @PageColor(orange)
}
@Image(source: "brands-common-swift-brand-identity-hero", alt: "CommonSwift Brand Identity hero")


## Design Brief

[Read the full design brief](<doc:common-swift-design-brief>)

## Visual Identity

### Color Palette

- **Primary:** #F05138 (Swift Orange)
- **Secondary:** #333333 (Charcoal)
- **Accent:** #007AFF (Apple Blue)

### Color Usage

- Primary is reserved for calls-to-action and key highlights.
- Secondary anchors typography and long-form text.
- Accent is for links, hover states, and interactive affordances.
- Neutral base uses white/near-white backgrounds with high contrast text.

### Logo

This is the primary logo for CommonSwift. It represents the modular and interconnected nature of the ecosystem.

![Primary Logo](logo-primary.svg)

### Pictographs

These pictographs represent the core libraries of the CommonSwift ecosystem.

| Library | Pictograph |
|---|---|
| `CommonShell` | ![CommonShell Pictograph](pictograph-common-shell.svg) |
| `CommonCLI` | ![CommonCLI Pictograph](pictograph-common-cli.svg) |
| `CommonProcess` | ![CommonProcess Pictograph](pictograph-common-process.svg) |

### Typography

- Headings: modern sans with strong legibility.
- Body: humanist sans to balance approachability and precision.
- Code: monospaced, ligatures disabled for clarity.

#### Font families (proposed)

- Headings: SF Pro Display (fallback: SF Pro Text, system)
- Body: SF Pro Text (fallback: system)
- Code: SF Mono (fallback: Menlo, monospace)

### Layout and Grid

- Base spacing scale: 4/8/12/16/24/32/48.
- Grid favors generous margins and predictable rhythm.
- Dense views should never drop below 8pt row height.

### Iconography

- Outline icons for navigation and categories.
- Filled icons only for active or selected states.
- Pictographs keep consistent stroke weight and corner radius.

### Motion

- Subtle transitions for emphasis (200-250ms).
- No looping animations in documentation contexts.
- Respect reduce-motion preferences by disabling non-essential motion.

### Accessibility

- Contrast ratio >= 4.5 for body text and UI controls.
- Keyboard-first navigation in interactive demos.
- Focus states are visible and consistent with accent color.

### Sample UI palette

| Token | Hex | Usage |
|---|---|---|
| `ui.background` | #FFFFFF | App background |
| `ui.surface` | #F6F7F9 | Panels, cards |
| `ui.border` | #E4E7EC | Dividers, outlines |
| `ui.text.primary` | #1D1D1F | Primary text |
| `ui.text.secondary` | #4B4B4B | Secondary text |
| `ui.link` | #007AFF | Links, hover |
| `ui.cta` | #F05138 | Primary actions |
| `ui.success` | #2E9D4B | Success states |
| `ui.warning` | #B46A00 | Warnings |
| `ui.error` | #D12C2C | Errors |

### Voice and Tone

- Confident, calm, and precise.
- Avoid hype; emphasize clarity and dependability.

## Topics

- <doc:common-swift-color>
- <doc:common-swift-typography>
- <doc:common-swift-logo>
- <doc:common-swift-iconography>
- <doc:common-swift-layout-grid>
- <doc:common-swift-motion>
- <doc:common-swift-accessibility>
- <doc:common-swift-voice-tone>
- <doc:common-swift-examples>
