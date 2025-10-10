# tailugin

Tailugin is a collection of Tailwind CSS v4–ready utilities, offering expressive @utility rules for enter/leave animations (originally by [jamiebuilds/tailwindcss-animate](https://github.com/jamiebuilds/tailwindcss-animate)
), refined easing presets, and semantic UI state variants—so you can compose polished interactions using idiomatic Tailwind class names.

> **Compatibility**: Tailugin targets the Tailwind CSS v4 architecture (`@utility`, `@custom-variant`, `@theme`). Earlier versions of Tailwind do not understand these directives.

## Installation

Install Tailugin alongside Tailwind CSS v4:

```bash
bun add tailugin tailwindcss@next
# or
npm install tailugin tailwindcss@next
```

> Tailwind CSS v4 is still in prerelease as of this writing. Replace `@next` with the latest compatible tag once Tailwind publishes v4 formally.

## Usage

Import Tailugin from your Tailwind entry CSS (for example `app.css`). Tailwind v4 processes the `@import` statements at build time.

```css
@import "tailwindcss";
@import "tailugin";
```

You can also ships granular entry points if you only need a subset of utilities:

```css
@import "tailugin/animate.css";
@import "tailugin/conditions.css";
@import "tailugin/easings.css";
```

### Class name syntax

All utilities follow the Tailwind CSS v4 pattern where the suffix after the utility name becomes the `--value()` argument. For numeric shorthands, integers are multiplied by sensible units (percentages, degrees, or spacing scale). Where Tailwind lacks defaults (for example, there is no canonical list of custom easing tokens yet), Tailugin provides theme tokens you can reference.

## Animation utilities

| Utility          | Description                                                                                                                                                                                                                          | Accepted values                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| `animate-in`     | Sets up shared enter animation keyframes. Use with other utilities (e.g., `fade-in-0`) to define the actual transform/opacity. Duration defaults to `300ms`; override with Tailwind's `duration-*` utilities or set `--tw-duration`. | n/a                                                               |
| `animate-out`    | Sets up shared leave animation keyframes. Combine with exit utilities such as `slide-out-y-4`. Duration defaults to `300ms`.                                                                                                         | n/a                                                               |
| `fill-mode-*`    | Controls `animation-fill-mode`. Accepts `none`, `forwards`, `backwards`, `both`.                                                                                                                                                     | literal keywords                                                  |
| `direction-*`    | Controls `animation-direction`. Accepts `normal`, `reverse`, `alternate`, `alternate-reverse`.                                                                                                                                       | literal keywords                                                  |
| `repeat-*`       | Sets `animation-iteration-count`. Provide an integer (`repeat-3`) or `[integer]` arbitrary value, including `infinite`.                                                                                                              | integer, `[integer]`, `infinite`                                  |
| `play-state-*`   | Controls `animation-play-state`. Accepts `running` or `paused`.                                                                                                                                                                      | literal keywords                                                  |
| `fade-in-*`      | Sets `--tw-enter-opacity`. Numeric suffixes map to percentages; arbitrary values allowed.                                                                                                                                            | integers → %, `[percentage]`                                      |
| `fade-out-*`     | Sets `--tw-leave-opacity`. Numeric suffixes map to percentages; arbitrary values allowed.                                                                                                                                            | integers → %, `[percentage]`                                      |
| `slide-in-y-*`   | Sets `--tw-enter-translate-y` from Tailwind spacing scale or arbitrary `[percentage]/[length]`.                                                                                                                                      | integers → spacing, arbitrary length/percentage                   |
| `-slide-in-y-*`  | Negative version of `slide-in-y-*`.                                                                                                                                                                                                  | integers → negative spacing, arbitrary negative length/percentage |
| `slide-out-y-*`  | Sets `--tw-leave-translate-y`.                                                                                                                                                                                                       | integers → spacing, arbitrary length/percentage                   |
| `-slide-out-y-*` | Negative version of `slide-out-y-*`.                                                                                                                                                                                                 | integers → negative spacing, arbitrary negative length/percentage |
| `slide-in-x-*`   | Sets `--tw-enter-translate-x`.                                                                                                                                                                                                       | integers → spacing, arbitrary length/percentage                   |
| `-slide-in-x-*`  | Negative version of `slide-in-x-*`.                                                                                                                                                                                                  | integers → negative spacing, arbitrary negative length/percentage |
| `slide-out-x-*`  | Sets `--tw-leave-translate-x`.                                                                                                                                                                                                       | integers → spacing, arbitrary length/percentage                   |
| `-slide-out-x-*` | Negative version of `slide-out-x-*`.                                                                                                                                                                                                 | integers → negative spacing, arbitrary negative length/percentage |
| `spin-in-*`      | Sets `--tw-enter-rotate`. Numeric suffix maps to degrees; arbitrary angles allowed.                                                                                                                                                  | integers → deg, `[angle]`                                         |
| `-spin-in-*`     | Negative rotation for enter animations.                                                                                                                                                                                              | integers → -deg, `[angle]`                                        |
| `spin-out-*`     | Sets `--tw-leave-rotate`.                                                                                                                                                                                                            | integers → deg, `[angle]`                                         |
| `-spin-out-*`    | Negative rotation for leave animations.                                                                                                                                                                                              | integers → -deg, `[angle]`                                        |
| `zoom-in-*`      | Sets `--tw-enter-scale`. Numeric suffix maps to percentages; arbitrary percentages allowed.                                                                                                                                          | integers → %, `[percentage]`                                      |
| `zoom-out-*`     | Sets `--tw-leave-scale`. Numeric suffix maps to percentages; arbitrary percentages allowed.                                                                                                                                          | integers → %, `[percentage]`                                      |

All animation primitives rely on the shared `@keyframes animate-enter` and `@keyframes animate-leave` definitions. Combine enter (`animate-in`) and leave (`animate-out`) utilities with the transformation utilities to orchestrate complex transitions.

## Easing theme tokens

Tailugin exposes a curated easing palette via `@theme`. Reference these custom properties through Tailwind's native `ease-*` utilities or by authoring custom utilities that read the variables.

| Token                 | Curve                                     |
| --------------------- | ----------------------------------------- |
| `--ease-in-quad`      | `cubic-bezier(0.55, 0.085, 0.68, 0.53)`   |
| `--ease-in-cubic`     | `cubic-bezier(0.55, 0.055, 0.675, 0.19)`  |
| `--ease-in-quart`     | `cubic-bezier(0.895, 0.03, 0.685, 0.22)`  |
| `--ease-in-quint`     | `cubic-bezier(0.755, 0.05, 0.855, 0.06)`  |
| `--ease-in-expo`      | `cubic-bezier(0.95, 0.05, 0.795, 0.035)`  |
| `--ease-in-circ`      | `cubic-bezier(0.6, 0.04, 0.98, 0.335)`    |
| `--ease-out-quad`     | `cubic-bezier(0.25, 0.46, 0.45, 0.94)`    |
| `--ease-out-cubic`    | `cubic-bezier(0.215, 0.61, 0.355, 1)`     |
| `--ease-out-quart`    | `cubic-bezier(0.165, 0.84, 0.44, 1)`      |
| `--ease-out-quint`    | `cubic-bezier(0.23, 1, 0.32, 1)`          |
| `--ease-out-expo`     | `cubic-bezier(0.19, 1, 0.22, 1)`          |
| `--ease-out-circ`     | `cubic-bezier(0.075, 0.82, 0.165, 1)`     |
| `--ease-in-out-quad`  | `cubic-bezier(0.455, 0.03, 0.515, 0.955)` |
| `--ease-in-out-cubic` | `cubic-bezier(0.645, 0.045, 0.355, 1)`    |
| `--ease-in-out-quart` | `cubic-bezier(0.77, 0, 0.175, 1)`         |
| `--ease-in-out-quint` | `cubic-bezier(0.86, 0, 0.07, 1)`          |
| `--ease-in-out-expo`  | `cubic-bezier(1, 0, 0, 1)`                |
| `--ease-in-out-circ`  | `cubic-bezier(0.785, 0.135, 0.15, 0.86)`  |

To use them, map Tailwind class names to the variables in your CSS, for example:

```css
@utility ease-in-quad {
  animation-timing-function: var(--ease-in-quad);
}
```

Tailwind v4's default theme has not finalized named easings yet, so Tailugin does not register class aliases out of the box. Define the utilities above in your project if you need direct class names.

## Custom variants

Tailugin defines semantic variants that respond to ARIA, `data-*`, and structural state. Apply them using Tailwind's `variant:utility` syntax, such as `disabled:opacity-50` or `dark:bg-gray-950`.

### Interaction variants

| Variant             | Matches                                                                            |
| ------------------- | ---------------------------------------------------------------------------------- |
| `placeholder-shown` | `:placeholder-shown`, `[data-placeholder-shown]`                                   |
| `active`            | `:active`, `[data-active]`, `[data-active="true"]`                                 |
| `disabled`          | `:disabled`, `[data-disabled]`, `[data-disabled="true"]`, `[aria-disabled="true"]` |
| `focus`             | `:focus`, `[data-focus]`, `[data-focus="true"]`                                    |
| `focus-visible`     | `:focus-visible`, `[data-focus-visible]`, `[data-focus-visible="true"]`            |
| `dragging`          | `[data-dragging]`, `[aria-grabbed="true"]`                                         |
| `loading`           | `[data-loading]`, `[data-loading="true"]`, `[aria-busy="true"]`                    |
| `fullscreen`        | `:fullscreen`, `[data-fullscreen]`, `[data-fullscreen="true"]`                     |

### State variants

| Variant         | Matches                                                                                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `open`          | `[open]`, `[data-open]`, `[data-open="true"]`, `[data-state="open"]`, `[aria-expanded="true"]`                         |
| `closed`        | `[closed]`, `[data-closed]`, `[data-closed="true"]`, `[data-state="closed"]`, `[aria-expanded="false"]`                |
| `checked`       | `[data-state="checked"]`, `[aria-checked="true"]`, `[data-checked]`, `[data-checked="true"]`, `[data-selected="true"]` |
| `unchecked`     | `[data-state="unchecked"]`, `[aria-checked="false"]`, `[data-checked="false"]`                                         |
| `indeterminate` | `[data-state="indeterminate"]`, `[aria-checked="mixed"]`, `[data-indeterminate]`, `[data-indeterminate="true"]`        |
| `on`            | `[data-state="on"]`, `[role="switch"][aria-checked="true"]`                                                            |
| `off`           | `[data-state="off"]`, `[role="switch"][aria-checked="false"]`                                                          |
| `expanded`      | `[aria-expanded="true"]`, `[data-expanded]`, `[data-expanded="true"]`, `[data-state="expanded"]`, `[data-open]`        |
| `collapsed`     | `[aria-expanded="false"]`, `[data-collapsed]`, `[data-collapsed="true"]`, `[data-state="collapsed"]`, `[data-closed]`  |
| `highlighted`   | `[data-highlighted]`, `[data-highlighted="true"]`, `[aria-selected="true"]`                                            |
| `current`       | `[aria-current]`, `[aria-current="true"]`, `[data-current]`, `[data-current="true"]`                                   |
| `current-page`  | `[aria-current="page"]`                                                                                                |
| `current-step`  | `[aria-current="step"]`                                                                                                |
| `under-value`   | `[data-state="under-value"]`, `[data-under-value]`                                                                     |

### Layout variants

| Variant      | Matches                                                              |
| ------------ | -------------------------------------------------------------------- |
| `horizontal` | `[data-orientation="horizontal"]`, `[aria-orientation="horizontal"]` |
| `vertical`   | `[data-orientation="vertical"]`, `[aria-orientation="vertical"]`     |
| `topmost`    | `[data-topmost]`                                                     |

### Calendar variants

| Variant       | Matches                                         |
| ------------- | ----------------------------------------------- |
| `now`         | `[data-now]`                                    |
| `today`       | `[data-today]`, `[aria-current="date"]`         |
| `unavailable` | `[data-unavailable]`                            |
| `range-start` | `[data-range-start]`                            |
| `range-end`   | `[data-range-end]`                              |
| `complete`    | `[data-complete]`, `[data-completed="true"]`    |
| `incomplete`  | `[data-incomplete]`, `[data-completed="false"]` |

### Theme variants

| Variant | Matches                                          |
| ------- | ------------------------------------------------ |
| `dark`  | `.dark` scope (excluding nested `.light` scopes) |

## Combining utilities and variants

Because Tailugin relies on Tailwind's native directives, you can compose utilities and variants exactly as you would built-in classes. For example:

```html
<button
  class="animate-in zoom-in-95 fade-in-0 duration-200 ease-out-quart disabled:opacity-50"
>
  Continue
</button>
```

This button zooms and fades in with a custom ease curve, while the `disabled` variant ensures the button visually responds to accessibility states.

## Troubleshooting

- **Missing class warnings**: Tailwind v4 is responsible for generating the final CSS from `@utility` rules. Ensure your Tailwind CLI or framework integration is on v4; earlier versions silently ignore the directives.
- **Custom easing utility names**: Tailugin only registers the CSS variables for easings. Define your own `@utility` wrappers or rely on Tailwind's upcoming defaults once available.

## License

Tailugin is released under the MIT License. See [LICENSE](LICENSE) for details.
