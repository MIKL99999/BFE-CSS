# Truncate text with ellipsis in one line

Problem: https://bigfrontend.dev/css/truncate-text-with-ellipsis-in-one-line

Keep `.one-line` on a single line and show `…` where the text is cut.

`style.css` holds the main solution (variant 1). Every variant is in `solutions/`; open `index.html` and switch between them with the dropdown.

| # | File | Idea | Notes |
|---|------|------|-------|
| 1 | [01-overflow-hidden.css](solutions/01-overflow-hidden.css) | `white-space: nowrap; overflow: hidden; text-overflow: ellipsis` | The canonical trio. All three are required. |
| 2 | [02-overflow-clip.css](solutions/02-overflow-clip.css) | Same, with `overflow: clip` | Passes on BFE. Looks the same, behaves differently (see below). |
| 3 | [03-text-wrap-nowrap.css](solutions/03-text-wrap-nowrap.css) | `text-wrap: nowrap` instead of `white-space: nowrap` | Chrome 114+, Safari 17.4+. Not checked on BFE; the VS Code CSS linter does not know it yet. Only stops wrapping and leaves whitespace collapsing alone. |
| 4 | [04-line-clamp-fails.css](solutions/04-line-clamp-fails.css) | `-webkit-line-clamp: 1` | **Does not pass on BFE.** Text still wraps by words, so it is not a true single line, and a long word without spaces is cut with no ellipsis. Use it for multi-line clamping. |

## Why all three properties

- `white-space: nowrap` keeps the text on one line, so it overflows horizontally.
- `overflow: hidden` (or `clip`) cuts the overflow. `text-overflow` only works when `overflow` is not `visible`.
- `text-overflow: ellipsis` draws `…` at the cut instead of a hard clip.

`text-overflow` applies to block containers, so an inline element (`<span>`) needs `display: block` / `inline-block`. Inside a flex item, add `min-width: 0` to the item, otherwise it grows to fit the text and nothing overflows.

## `overflow: hidden` vs `overflow: clip`

- `hidden` cuts the content, but the element is still a **scroll container**. It can be scrolled by JS (`scrollLeft`, `scrollTo`), by keyboard when focused, by Shift + wheel, or by `scrollIntoView()` on a child. It also creates a new block formatting context.
- `clip` only cuts. The element cannot be scrolled at all, even from JS, and it does not create a new formatting context. `overflow-clip-margin` can widen the painted area a little past the box.

Try it in `index.html`: the `scrollLeft = 100` button moves the text with variant 1 and does nothing with variant 2.

## JavaScript

Only for cases CSS cannot do, such as an ellipsis in the middle (`file…name.txt`). Then cut the string by hand and put the full text in `title`.
