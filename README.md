# Project Odin - Admin Dashboard

## Steps I made

1. Create the main dashboard grid container.

```html
<div class="dashboard-container"></div>
```

2. Create sidebar container.

```html
<div class="sidebar-container"></div>
```

3. Create header container.

```html
<div class="header-container"></div>
```

4. Create main content container.

```html
<div class="main-content-container"></div>
```

5. Set main dashboard grid layout.

```css
.dashboard-grid-container {
    height: 100vh;
    display: grid;
    grid-template-rows: 200px 1fr;
    grid-template-columns: minmax(200px, 1fr) minmax(400px, 8fr);
    grid-template-areas:
        "sidebar header"
        "sidebar main-content";
}
```

6. Set sidebar grid and background color.

```css
.sidebar-container {
    grid-area: sidebar;
    background-color: #1992d4;
}
```

7. Set header grid and shadow.

```css
.header-container {
    grid-area: header;
    background-color: white;
    box-shadow: 0px 5px 5px lightgrey;
}
```

8. Set main content grid and bg color.

```css
.main-content-container {
    grid-area: main-content;
    background-color: #e2e8f0;
}
```

9. The header shadows got covered by the main content container.

```css
/* 7 */
.header-container {
    grid-area: header;
    background-color: white;
    box-shadow: 0px 5px 5px lightgrey;
    /* 9 */
    z-index: 1;
}
```
