# CommonSwift Motion

@Metadata {
  @PageImage(purpose: icon, source: "brands-common-swift-motion-icon", alt: "CommonSwift Motion icon")
  @PageImage(purpose: card, source: "brands-common-swift-motion-card", alt: "CommonSwift Motion card")
  @PageKind(article)
  @PageColor(orange)
}
@Image(source: "brands-common-swift-motion-hero", alt: "CommonSwift Motion hero")


## Intent

Motion should reinforce context changes without distracting from reading.

## Rules

- Use subtle transitions (200-250ms) for panels and drawers.
- Avoid looping animations in documentation pages.
- Honor reduce-motion preferences by disabling non-essential motion.

## Do

- Animate state changes (hover, focus, active) with small, consistent timing.
- Use loading indicators only when necessary.

## Avoid

- Large parallax or decorative motion in docs.
- Competing animations in adjacent panels.
