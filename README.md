# postcss-logical-issue

Reproduction of postcss-logical issue

## Issue

When running `postcss` with `postcss-preset-env`, and using CSS logical properties that use a CSS custom property like:

```css
:root {
  --content-width: 300px;
}

.c {
  margin-inline-start: var(--content-width);
}
```

Produce as output a duplicate rule that prevents the usage of the custom property:

```css
:root {
  --content-width: 300px;
}

[dir="ltr"] .c {
  margin-left: 300px;
  margin-left: var(--content-width);
}

[dir="rtl"] .c {
  margin-right: 300px;
  margin-right: var(--content-width);
}

[dir="ltr"] .c {
  margin-left: 300px;
}

[dir="rtl"] .c {
  margin-right: 300px;
}
```
