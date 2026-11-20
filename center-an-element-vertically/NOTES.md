# Center an element vertically

Problem: https://bigfrontend.dev/css/center-an-element-vertically

Center `.inner` (100×100) inside `.outer` (100%×100%) on both axes, changing only `.outer` and `.inner`.

`style.css` holds the main solution (variant 2). Every variant is in `solutions/`; open `index.html` and switch between them with the dropdown.

| # | File | Idea | Notes |
|---|------|------|-------|
| 1 | [01-flex.css](solutions/01-flex.css) | `display: flex; align-items: center; justify-content: center` | The classic. Works for any size of `.inner`. |
| 2 | [02-grid-place-items.css](solutions/02-grid-place-items.css) | `display: grid; place-items: center` | Shortest. Centers the item inside its grid cell. |
| 3 | [03-grid-place-content.css](solutions/03-grid-place-content.css) | `display: grid; place-content: center` | Centers the whole grid track block instead of the item in its cell. Same result for one child. |
| 4 | [04-flex-margin-auto.css](solutions/04-flex-margin-auto.css) | `display: flex` (or `grid`) + `margin: auto` on `.inner` | Auto margins on a flex/grid item absorb free space on all sides. |
| 5 | [05-absolute-transform.css](solutions/05-absolute-transform.css) | `top/left: 50%` + `transform: translate(-50%, -50%)` | No need to know the size. Useful for overlays and modals. |
| 6 | [06-absolute-inset-margin-auto.css](solutions/06-absolute-inset-margin-auto.css) | `position: absolute; inset: 0; margin: auto` | Needs explicit `width` and `height` on `.inner`. |
| 7 | [07-absolute-calc.css](solutions/07-absolute-calc.css) | `top/left: calc(50% - 50px)` | Needs the size known up front; breaks if it changes. |

## Not used here

`display: table-cell; vertical-align: middle` on `.outer` does not work in this problem. Without a parent with `display: table`, the browser wraps the cell in an anonymous table that shrinks to its content, so `.outer`'s `width/height: 100%` have no effect. It would need an extra wrapper, and only `.outer` and `.inner` may be changed.

## Note on `html, body`

Each file sets `html, body { height: 100%; margin: 0 }` only so `.outer` has a height to center in when previewing locally. On BFE the container already has a size, so submit only the `.outer` / `.inner` rules.
