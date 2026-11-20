# BFE CSS — My Solutions

My solutions to the CSS problems on [BigFrontEnd.dev](https://bigfrontend.dev/css).

## Structure

Each problem lives in its own folder, named after the slug in the problem's URL:

```
bfe-css/
├── _template/                     # template for a new problem
│   ├── index.html
│   └── style.css
├── center-an-element-vertically/  # https://bigfrontend.dev/css/center-an-element-vertically
│   ├── index.html
│   ├── style.css
│   └── NOTES.md                   # (optional) notes, alternative approaches
└── ...
```

## Adding a new problem

1. Take the slug from the problem URL: `https://bigfrontend.dev/css/<slug>`.
2. Copy the template:
   ```bash
   cp -r _template <slug>
   ```
3. Add the problem link and your solution to `index.html` and `style.css`.
4. Open `index.html` in a browser and check the result.
5. Commit:
   ```bash
   git add <slug>
   git commit -m "solve: <slug>"
   git push
   ```

## Progress

| # | Problem | Status |
|---|---------|--------|
| 1 | [center-an-element-vertically](https://bigfrontend.dev/css/center-an-element-vertically) | ⬜ |
