---
name: Local-First Prototype Series
version: alpha
description: >
  Visual identity for the local-first prototype series: Governance Window Tracker,
  checkout-seam, fhir-seam, and Local-First Social (SocialPings). A single shared
  design system governing all four prototypes. React + TypeScript + Tailwind stack.
  Tokens here are normative. Session agents must not override them with defaults.

colors:
  primary: "#0F172A"
  primary-surface: "#1E293B"
  secondary: "#475569"
  secondary-surface: "#64748B"
  neutral: "#F8FAFC"
  neutral-muted: "#F1F5F9"
  border: "#E2E8F0"
  accent: "#3B82F6"
  accent-surface: "#EFF6FF"

  # Seam state palette — used for connection/sync status UI across all prototypes
  seam-none: "#6B7280"
  seam-connecting: "#F59E0B"
  seam-established: "#10B981"
  seam-error: "#EF4444"
  seam-error-surface: "#FEF2F2"
  seam-warning-surface: "#FFFBEB"
  seam-success-surface: "#ECFDF5"

  # FHIR response taxonomy (fhir-seam only)
  fhir-accepted: "#10B981"
  fhir-validation: "#F59E0B"
  fhir-transient: "#6B7280"
  fhir-permanent: "#EF4444"

typography:
  display:
    fontFamily: Inter
    fontSize: 1.5rem
    fontWeight: 600
    lineHeight: 1.25
    letterSpacing: -0.02em
  heading:
    fontFamily: Inter
    fontSize: 1.125rem
    fontWeight: 600
    lineHeight: 1.4
  body-md:
    fontFamily: Inter
    fontSize: 0.9375rem
    fontWeight: 400
    lineHeight: 1.6
  body-sm:
    fontFamily: Inter
    fontSize: 0.875rem
    fontWeight: 400
    lineHeight: 1.5
  label:
    fontFamily: Inter
    fontSize: 0.75rem
    fontWeight: 500
    lineHeight: 1.4
    letterSpacing: 0.01em
  mono:
    fontFamily: "JetBrains Mono, Menlo, monospace"
    fontSize: 0.8125rem
    fontWeight: 400
    lineHeight: 1.6

rounded:
  sm: 4px
  md: 6px
  lg: 10px
  pill: 9999px

spacing:
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  2xl: 48px

components:
  # Primary action button
  button-primary:
    backgroundColor: "{colors.accent}"
    textColor: "#FFFFFF"
    typography: "{typography.label}"
    rounded: "{rounded.md}"
    padding: "10px 16px"
  button-primary-hover:
    backgroundColor: "#2563EB"

  # Secondary / ghost button
  button-secondary:
    backgroundColor: "{colors.neutral}"
    textColor: "{colors.primary}"
    typography: "{typography.label}"
    rounded: "{rounded.md}"
    padding: "10px 16px"

  # Seam status badge — core component, appears in all four prototypes
  seam-badge-none:
    backgroundColor: "{colors.neutral-muted}"
    textColor: "{colors.seam-none}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: "2px 10px"
  seam-badge-connecting:
    backgroundColor: "{colors.seam-warning-surface}"
    textColor: "{colors.seam-connecting}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: "2px 10px"
  seam-badge-established:
    backgroundColor: "{colors.seam-success-surface}"
    textColor: "{colors.seam-established}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: "2px 10px"
  seam-badge-error:
    backgroundColor: "{colors.seam-error-surface}"
    textColor: "{colors.seam-error}"
    typography: "{typography.label}"
    rounded: "{rounded.pill}"
    padding: "2px 10px"

  # Card — local state container
  card:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.primary}"
    rounded: "{rounded.lg}"
    padding: "{spacing.lg}"
  card-muted:
    backgroundColor: "{colors.neutral-muted}"
    textColor: "{colors.secondary}"
    rounded: "{rounded.lg}"
    padding: "{spacing.lg}"

  # Input
  input:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.primary}"
    rounded: "{rounded.md}"
    padding: "10px 12px"
  input-focus:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.primary}"

  # FHIR response states (fhir-seam)
  fhir-banner-accepted:
    backgroundColor: "{colors.seam-success-surface}"
    textColor: "{colors.fhir-accepted}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"
  fhir-banner-validation:
    backgroundColor: "{colors.seam-warning-surface}"
    textColor: "{colors.fhir-validation}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"
  fhir-banner-transient:
    backgroundColor: "{colors.neutral-muted}"
    textColor: "{colors.fhir-transient}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"
  fhir-banner-permanent:
    backgroundColor: "{colors.seam-error-surface}"
    textColor: "{colors.fhir-permanent}"
    rounded: "{rounded.md}"
    padding: "{spacing.md}"

  # Composer (SocialPings) — hint text reflects seam state
  composer-hint-established:
    backgroundColor: "{colors.seam-success-surface}"
    textColor: "{colors.seam-established}"
    typography: "{typography.label}"
    rounded: "{rounded.sm}"
    padding: "4px 8px"
  composer-hint-offline:
    backgroundColor: "{colors.neutral-muted}"
    textColor: "{colors.seam-none}"
    typography: "{typography.label}"
    rounded: "{rounded.sm}"
    padding: "4px 8px"

  # Bottom nav (SocialPings mobile shell)
  bottom-nav:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.secondary}"
  bottom-nav-active:
    backgroundColor: "#FFFFFF"
    textColor: "{colors.accent}"
---

## Overview

Minimal utilitarian. The prototypes in this series are not consumer products — they
are architectural arguments made concrete. The visual language follows from that
purpose: high legibility, low decoration, no chrome. Every UI element should be
explicable by what it is communicating about state, not by aesthetic preference.

The single most important design decision in this system is the **seam state
palette**. The seam — the minimum server-dependent surface in an otherwise
local-first system — is the architectural claim this series makes. The UI must
make that claim visible. A user should be able to read the seam state at a glance:
no connection, connecting, established, error. These four states map to four colors
(`seam-none`, `seam-connecting`, `seam-established`, `seam-error`) that are
semantically consistent across all four prototypes. Agents must not substitute
Tailwind defaults for these states.

Stack context: React + TypeScript + Tailwind CSS. All `rounded`, `spacing`, and
typography values have direct Tailwind equivalents. Use the token values here as
the source of truth; derive Tailwind classes from them. Do not invent new colors
or spacing values mid-session.

## Colors

The palette is divided into three functional groups.

**Base palette** — primary, primary-surface, secondary, secondary-surface, neutral,
neutral-muted, border. These govern application chrome, text hierarchy, and
backgrounds. `primary` (#0F172A) is Slate 900 — deep enough to read as near-black
without being pure black. `neutral` (#F8FAFC) is Slate 50 — warm off-white that
reads as a surface, not a void.

**Seam state palette** — seam-none through seam-error-surface. These colors are
semantically load-bearing. They are not decorative. The seam-badge component is the
primary consumer, but any UI element that reflects connection state — composer hint
text, sync status indicators, relay health displays — must use these tokens and not
ad-hoc Tailwind color classes. Consistency across prototypes is the requirement.

**FHIR response palette** — fhir-accepted, fhir-validation, fhir-transient,
fhir-permanent. Applies only in fhir-seam. The four states correspond to HTTP 200,
422, 503, and 500 responses but are named semantically, not technically. The UI
should display the semantic label, not the status code. A patient should not see
"503."

**Accent** (#3B82F6, Blue 500) is the single interactive color. It governs
primary buttons, active nav states, and focused inputs. It appears sparingly.

## Typography

Inter throughout. This is a deliberate constraint: one typeface, one scale, weight
and size as the only variables. The `mono` token (JetBrains Mono fallback to Menlo)
is reserved for code display, relay addresses, and Y.js document IDs — anything
that should read as a technical identifier rather than prose.

The `label` token governs all badge text, status indicators, and small-form UI
elements. It is 12px with slight positive letter-spacing — legible at small sizes
without appearing cramped.

## Layout

Mobile-first. SocialPings is a mobile shell application (bottom nav, full-height
layout, `h-screen overflow-hidden` on the wrapper). checkout-seam and fhir-seam
are desktop-primary but should function at tablet width. The Governance Window
Tracker is read-only and desktop-primary.

The bottom nav pattern in SocialPings is load-bearing: `shrink-0` on the nav
element prevents it from collapsing under content pressure. This is a known failure
mode — do not omit.

Max content width: 680px on desktop, full width minus 32px padding on mobile.

## Shapes

Rounded corners use the token scale (`sm`/`md`/`lg`/`pill`) consistently. Pill
radius is reserved for seam state badges and trust tier chips — the visual
distinction signals "status indicator" vs. "interactive element." Do not apply
`pill` to buttons.

## Components

### Seam Badge

The seam badge is the single most cross-cutting component in this system. It
appears in every prototype that has an active seam (checkout-seam, fhir-seam,
SocialPings). Its four states (none, connecting, established, error) must match the
seam state palette tokens exactly. The composer hint text in SocialPings is a
variant of the seam badge concept applied inline rather than as a pill — use
`composer-hint-established` and `composer-hint-offline` tokens, not free-form
color classes.

### FHIR Response Banners

The four fhir-banner variants correspond to the four response states documented in
the fhir-seam architecture. Text displayed in each banner:
- `fhir-banner-accepted`: "Your intake has been received." (no status code)
- `fhir-banner-validation`: "Something in your form needs correction. [Review]"
- `fhir-banner-transient`: "The system is temporarily unavailable. Your form is
  saved locally — try again in a few minutes."
- `fhir-banner-permanent`: "We weren't able to submit your form right now. Please
  contact the clinic directly."

These copy strings are part of the design spec, not just color tokens. An agent
generating banner UI must use this language, not HTTP error messages.

### Card vs. Card-Muted

`card` is for active local state — the cutting table, the cart, the patient form,
the active thread. `card-muted` is for historical or secondary state — order
history entries, archived pings, trust graph entries at lower tiers. The visual
distinction signals to the user what is live vs. what is record.

## Do's and Don'ts

**Do** use seam state tokens for any UI element that reflects connection or sync
state. **Do not** use Tailwind color utilities (`text-green-500`, `bg-yellow-100`,
etc.) for these elements — they will drift across sessions.

**Do** use the `mono` typography token for relay addresses, Y.js document IDs, and
peer handles rendered in technical contexts. **Do not** apply `mono` to conversational
UI — ping text, status messages, display names.

**Do** apply `attachArrayObserver()` before any Y.Array nested in a Y.Map is
observed. This is not a UI concern but it surfaces as one: stale references produce
empty UI that looks like a styling bug and is not.

**Do not** introduce new colors mid-session. If a new color is needed, it is a
design decision that belongs here, not in a one-off Tailwind class.

**Do not** apply `pill` radius to buttons. Pill radius is reserved for status
indicators.
