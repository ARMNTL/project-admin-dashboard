# Project Odin - Admin Dashboard

## Credits

-   The Odin emoji is from AI Emojis @sujan_shrestha1 [link here](https://emojis.sh/emoji/thor-hammer-EPY4fHmrLS)

## Steps I made

### Dashboard layout

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

### Sidebar

10. Let's start nesting elements to the sidebar section. I can see 3 sections: header, main, misc.

```html
<div class="sidebar-header"></div>
<div class="sidebar-main"></div>
<div class="sidebar-misc"></div>
```

11. Sidebar header section.

```html
<svg xmlns="http://www.w3.org/2000/svg" width="64" viewBox="0 0 24 24">
    <path
        d="M12,4H20V10H12V4M12,21V11H20V21H12M3,21V15H11V21H3M3,14V4H11V14H3M4,5V13H10V5H4M13,5V9H19V5H13M13,12V20H19V12H13M4,16V20H10V16H4Z"
    />
</svg>
<span>Dashboard</span>
```

12. Oh my font! Setting font.

```css
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&display=swap");

body {
    font-family: "Noto Sans", sans-serif, system-ui;
}
```

13. Setting the sidebar header font.

```css
.sidebar-container {
    grid-area: sidebar;
    background-color: #1992d4;
    /* 13 */
    color: white;
}
```

14. Changing the icon color to white.

```css
.sidebar-container svg path {
    fill: white;
}
```

15. I'd like to align the header. I'm thinking flexbox.

```css
.sidebar-header {
    font-size: 1.5rem;
    /* 15 */
    display: flexbox;
    flex-direction: column;
}

.sidebar-header {
    display: flex;
    align-items: center;
}
```

16. Sidebar main section.

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
    <path
        d="M16,8.41L11.5,3.91L4.41,11H6V12L6,19H9V13H14V19H17V11H18.59L17,9.41V6H16V8.41M2,12L11.5,2.5L15,6V5H18V9L21,12H18V20H13V14H10V20H5V12H2Z"
    />
</svg>
<span>Home</span>
```

17. Hmm... all the links are vertically aligned. I think that grid layout will work better than flexbox.

```css
.sidebar-header {
    font-size: 1.5rem;
    /* 15, 17 */
    display: grid;
    grid-template-columns: 1fr 2fr;
    align-items: center;
}
```

18. Nesting the rest of the sidebar sections. Similar to step 16.

19. It feels to crowded. Setting some padding.

```css
.sidebar-container {
    ...
    /* 19 */
    padding: 1rem;
}
```

20. Overflow :( adjusting sidebar size.

```css
.dashboard-grid-container {
    ...
    grid-template-columns: minmax(256px, 1fr) minmax(400px, 8fr);
    ...
}
```

21. Separating a bit the 3 sections.

```css
.sidebar-header,
.sidebar-main,
.sidebar-misc {
    display: grid;
    /* 21 */
    grid-template-columns: 1fr 2fr;
    align-items: center;
    margin-bottom: 3rem;
}
```

22. Overall padding in the sidebar layout.

```css
.sidebar-container div :is(a, span) {
    padding: 0.75rem;
}
```

23. Adjusting icons sizes.

```css
.sidebar-container svg {
    width: 22px;
}

.sidebar-header svg {
    width: 48px;
}
```

24. Aligning all icons in the sidebar section.

```css
:is(.sidebar-header, .sidebar-main, .sidebar-misc) svg {
    justify-self: center;
}
```

25. Styling sidebar links.

```css
.sidebar-container a {
    color: white;
    text-decoration: none;
}

.sidebar-container a:hover {
    color: lightblue;
}
```

### Header

26. Setting the grid for the header. It looks that there are 4 sections: search bar, profile, greeting and buttons.

```css
.header-container {
    ...
    /* 26 */
    display: grid;
    grid-template-rows: 1fr 1fr;
    grid-template-columns: minmax(400px, 1fr) minmax(300px, 1fr);
}
```

27. Search bar elements.

```html
<div class="search-bar">
    <svg xmlns="http://www.w3.org/2000/svg" width="22" viewBox="0 0 24 24">
        <path
            d="M9.5,4C13.09,4 16,6.91 16,10.5C16,12.12 15.41,13.6 14.43,14.73L20.08,20.38L19.37,21.09L13.72,15.44C12.59,16.41 11.11,17 9.5,17C5.91,17 3,14.09 3,10.5C3,6.91 5.91,4 9.5,4M9.5,5C6.46,5 4,7.46 4,10.5C4,13.54 6.46,16 9.5,16C12.54,16 15,13.54 15,10.5C15,7.46 12.54,5 9.5,5Z"
        />
    </svg>
    <input class="search-bar-input" type="text" />
</div>
```

28. Profile elements. Style the avatar to fit.

```html
<div class="header-profile">
    <button>
        <svg xmlns="http://www.w3.org/2000/svg" width="22" viewBox="0 0 24 24">
            <path
                d="M11.5,6C15.64,6 19,9.36 19,13.5C19,17.64 15.64,21 11.5,21C7.36,21 4,17.64 4,13.5C4,9.36 7.36,6 11.5,6M11.5,7C7.91,7 5,9.91 5,13.5C5,17.09 7.91,20 11.5,20C15.09,20 18,17.09 18,13.5C18,9.91 15.09,7 11.5,7M11,9H12V13.36L15.05,14.78L14.63,15.69L11,14V9M15.25,5.25L15.89,4.5L19.72,7.7L19.08,8.46L15.25,5.25M7.75,5.25L3.92,8.46L3.28,7.7L7.11,4.5L7.75,5.25Z"
            />
        </svg>
    </button>
    <img
        class="header-avatar"
        src="./r0ox7x62v4cnpiukgpmwe89w3jeo.png"
        alt="Odin emoji"
    />
    <span>Thor Odinson</span>
</div>
```

```css
.header-profile .header-avatar {
    width: 48px;
    height: 48px;
    background-color: lightgrey;
    border-radius: 50%;
}
```

29. Greeting elements.

```html
<div class="header-greeting">
    <img
        class="header-avatar"
        src="./r0ox7x62v4cnpiukgpmwe89w3jeo.png"
        alt="Odin emoji"
    />
    <p>Hi there,</p>
    <p>Thor Odinson (@TOP)</p>
</div>
```

```css
.header-greeting .header-avatar {
    width: 64px;
    height: 64px;
    background-color: lightgrey;
    border-radius: 50%;
}
```

30. Buttons elements.

```html
<div class="header-buttons">
    <button>New</button>
    <button>Upload</button>
    <button>Share</button>
</div>
```

31. Styling header search bar.

```css
.header-search-bar {
    /* border: 1px solid; */
    padding: 1rem;
    display: grid;
    grid-template-columns: 22px 1fr;
}

.header-search-bar input[type="search"] {
    font-size: 1rem;
    padding: 8px 10px;
    margin-left: 1rem;
    background-color: #e2e8f0;
    border: none;
    border-radius: 12px;
}

.header-search-bar input[type="search"]:focus {
    outline: 1px solid lightgrey;
}

.header-search-bar svg {
    align-self: center;
}
```

32. Styling header profile section.

```css
.header-profile {
    display: flex;
    justify-content: end;
    align-items: center;
}

.header-profile span {
    font-weight: bold;
    padding-left: 1rem;
}

.header-profile button {
    margin-right: 1rem;
    background: none;
    border: none;
}

.header-profile button:hover {
    background-image: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><title>bell-off</title><path d="M2.79,4.46L3.5,3.75L20.25,20.5L19.54,21.21L17.34,19H3L6,16V10.5C6,9.67 6.18,8.88 6.5,8.18L2.79,4.46M12,4.5C12,4.22 11.78,4 11.5,4C11.22,4 11,4.22 11,4.5V6.03C10,6.14 9.09,6.58 8.4,7.24L7.69,6.53C8.33,5.92 9.12,5.46 10,5.21V4.5C10,3.67 10.67,3 11.5,3C12.33,3 13,3.67 13,4.5V5.21C15.31,5.86 17,8 17,10.5V15.84L16,14.84V10.5C16,8.18 14.25,6.28 12,6.03V4.5M7,10.5V16.41L5.41,18H16.34L7.28,8.94C7.1,9.43 7,9.95 7,10.5M11.5,22C10.29,22 9.28,21.14 9.05,20H10.09C10.29,20.58 10.85,21 11.5,21C12.15,21 12.71,20.58 12.91,20H13.95C13.72,21.14 12.71,22 11.5,22Z" /></svg>');
    border-radius: 50%;
    cursor: pointer;
}
```

33. Styling header greeting section.

```css
.header-greeting {
    display: grid;
    grid-template-columns: 64px 1fr;
    align-items: center;
}

.header-greeting div {
    padding-left: 1rem;
}

.header-greeting div p:nth-child(2) {
    font-size: 1.2rem;
    font-weight: bold;
}
```

34. Styling header buttons.

```css
.header-buttons {
    display: flex;
    justify-content: end;
    align-items: center;
}

.header-buttons button {
    padding: 1rem;
    margin-right: 2rem;
    width: 7rem;
    border: none;
    border-radius: 20px;
    font-weight: bold;
    color: white;
    background-color: #1992d4;
}

.header-buttons button:hover {
    background-color: #40b0f0;
    cursor: pointer;
}
```

### Main Content

35. There are 3 sections: your projects, announcements and trending. Grid-wise, 2 x 2 looks good. Setting the grid first.

```html
<div class="main-content-container">
    <div class="projects-container"></div>
    <div class="announcements-container"></div>
    <div class="trending-container"></div>
</div>
```

```css
.main-content-container {
    ...
    display: grid;
    grid-template-rows: 1fr 1fr;
    grid-template-columns: 1fr minmax(256px, auto);
    grid-template-columns: 1fr minmax(256px, auto);
    padding: 2rem 1rem;
    gap: 1rem;
    grid-template-areas:
        "cards announcements"
        "cards trending";
}
```

36. The projects section looks the hardest. It has the title and the cards sections. Setting the grid.

```html
<div class="projects-container">
    <h2 class="projects-title">Your Projects</h2>
    <div class="projects-cards"></div>
</div>
```

```css
.projects-container {
    grid-area: cards;
    display: grid;
    grid-template-rows: minmax(2rem, auto) 1fr;
}
```

37. Styling cards title.

```css
.projects-title {
    font-size: 1.1rem;
}
```

38. Making the cards.

```html
<a class="card" href="#">
    <div class="content">
        <h4>Super Cool Project</h4>
        <p>
            Lorem ipsum odor amet, consectetuer adipiscing elit. Aaliquet aenean
            eros eleifend pharetra felis posuere vivamus.
        </p>
    </div>

    <div class="card-buttons">
        <button>
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="22"
                viewBox="0 0 24 24"
            >
                <path
                    d="M12.86,10.44L11,6.06L9.14,10.45L4.39,10.86L8,14L6.92,18.63L11,16.17L15.09,18.63L14,14L17.61,10.86L12.86,10.44M16.59,20.7L11,17.34L5.42,20.7L6.88,14.35L1.96,10.07L8.45,9.5L11,3.5L13.55,9.5L20.04,10.07L15.12,14.34L16.59,20.7Z"
                />
            </svg>
        </button>

        <button>
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="22"
                viewBox="0 0 24 24"
            >
                <path
                    d="M11.5,18C15.5,18 18.96,15.78 20.74,12.5C18.96,9.22 15.5,7 11.5,7C7.5,7 4.04,9.22 2.26,12.5C4.04,15.78 7.5,18 11.5,18M11.5,6C16.06,6 20,8.65 21.86,12.5C20,16.35 16.06,19 11.5,19C6.94,19 3,16.35 1.14,12.5C3,8.65 6.94,6 11.5,6M11.5,8C14,8 16,10 16,12.5C16,15 14,17 11.5,17C9,17 7,15 7,12.5C7,10 9,8 11.5,8M11.5,9C9.57,9 8,10.57 8,12.5C8,14.43 9.57,16 11.5,16C13.43,16 15,14.43 15,12.5C15,10.57 13.43,9 11.5,9Z"
                />
            </svg>
        </button>

        <button>
            <svg
                xmlns="http://www.w3.org/2000/svg"
                width="22"
                viewBox="0 0 24 24"
            >
                <path
                    d="M21.4,12.5L12,18.38L11,19V13.38L3,18.38L2,19V6L11,11.62V6L21.4,12.5M19.5,12.5L12,7.8V17.2L19.5,12.5M10.5,12.5L3,7.8V17.2L10.5,12.5Z"
                />
            </svg>
        </button></div
></a>
```

```css
.projects-cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(256px, 1fr));
    gap: 1rem;
}

.card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    color: black;
    text-decoration: none;
    border: 1px solid lightgrey;
    border-left: 10px solid #f0b429;
    border-radius: 8px;
    box-shadow: 0 0 8px grey;
    padding: 1rem;
}

.card p {
    font-size: 0.8rem;
    margin-top: 0.5rem;
}

.card-buttons {
    display: flex;
    justify-content: end;
}

.card button {
    background: none;
    border: none;
    margin-left: 1rem;
    text-align: center;
}

.card button:hover {
    opacity: 50%;
    cursor: pointer;
}
```

39. Nesting announcements elements.

```html
<div class="announcements-container">
    <h2 class="announcements-title">Announcements</h2>
    <div class="announcements">
        <div class="announcement">
            <a href="#">
                <h4>Site Maintenance</h4>
                <p>
                    Lorem ipsum dolor sit amet. Eum reiciendis accusamus ad
                    consequuntur odio ut iste officiis eos fuga magni. Non
                    voluptatibus atque est iste adipisci qui illum corrupti!
                </p>
            </a>
        </div>

        <div class="announcement">
            <a href="#">
                <h4>Site Maintenance</h4>
                <p>
                    Lorem ipsum dolor sit amet. Eum reiciendis accusamus ad
                    consequuntur odio ut iste officiis eos fuga magni. Non
                    voluptatibus atque est iste adipisci qui illum corrupti!
                </p>
            </a>
        </div>

        <div class="announcement">
            <a href="#">
                <h4>Site Maintenance</h4>
                <p>
                    Lorem ipsum dolor sit amet. Eum reiciendis accusamus ad
                    consequuntur odio ut iste officiis eos fuga magni. Non
                    voluptatibus atque est iste adipisci qui illum corrupti!
                </p>
            </a>
        </div>
    </div>
</div>
```

40. Styling announcements section.

```css
.announcements-container {
    grid-area: announcements;
    display: grid;
    grid-template-rows: minmax(2rem, auto) 1fr;
}

.announcements-title {
    font-size: 1.2rem;
    margin-bottom: 1rem;
}

.announcements {
    background-color: white;
    border: 1px solid lightgrey;
    border-radius: 8px;
    box-shadow: 0 0 8px grey;
    padding: 1rem;
}

.announcement a {
    color: black;
    text-decoration: none;
}

.announcement + .announcement {
    padding: 1rem 0;
    border-top: 1px solid lightgrey;
}

.announcements > .announcement:first-child {
    padding-bottom: 1rem;
}

.announcement h4 {
    font-size: 0.8rem;
}

.announcement p {
    font-size: 0.7rem;
}

.announcement p:hover {
    color: grey;
}
```

41. Nesting trending elements.

```html
<div class="trending-container">
    <h2 class="trending-title">Trending</h2>
    <div class="trendings">
        <div class="trending">
            <a href="#">
                <div class="trending-avatar">O</div>
                <div class="trending-group">
                    <div class="trending-domain">@TOP</div>
                    <div class="trending-project">Super Cool Project</div>
                </div>
            </a>
        </div>
    </div>
</div>
```

42. Styling trending.

```css
.trending-container {
    grid-area: trending;
    display: grid;
    grid-template-rows: minmax(2rem, auto) 1fr;
}

.trending-title {
    font-size: 1.2rem;
    margin-bottom: 1rem;
}

.trendings {
    background-color: white;
    border: 1px solid lightgrey;
    border-radius: 8px;
    box-shadow: 0 0 8px grey;
    padding: 1rem;
}

.trending {
    display: grid;
    grid-template-columns: 50px 1fr;
    gap: 1rem;
    padding: 1rem;
}

.trending a {
    text-decoration: none;
    color: black;
}

.trending a:visited {
    color: #1992d4;
}

.trending-avatar {
    text-align: center;
    align-self: center;
    justify-self: center;
    background-color: #1992d4;
    border-radius: 50%;
    font-size: 2rem;
    width: 48px;
    height: 48px;
}

.trending-domain {
    font-size: 0.8rem;
    font-weight: bold;
}

.trending-project {
    font-size: 0.8rem;
}
```
