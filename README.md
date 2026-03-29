# Windows XP Hugo Theme

A Hugo theme that recreates the **Windows XP Luna Blue** desktop experience in the browser — complete with draggable windows, a start menu, taskbar, and Explorer-style file browsing.

On mobile, it transforms into a **Windows Mobile 2003** Pocket PC interface.

## Features

- **Full desktop simulation** — taskbar, start menu, system tray with clock
- **Window manager** — drag, resize, minimize, maximize, close
- **Explorer layouts** — detail list view (blog) and icon grid view (projects)
- **Windows Picture and Fax Viewer** — click any image to open the photo viewer with zoom, rotate, and navigation
- **Scattered desktop files** — blog posts appear as Notepad files on the desktop
- **Mobile-first alternative** — Windows Mobile 2003 Today screen on small devices
- **Zero JavaScript frameworks** — vanilla JS, lightweight and fast
- **Configurable via Hugo menus** — desktop icons, start menu, sidebar all driven by `menu.main`

## Quick Start

### As a git submodule

```bash
cd your-hugo-site
git submodule add https://github.com/probonas/hugo-theme-windowsxp.git themes/hugo-theme-windowsxp
```

### As a Hugo module

Add to your `hugo.toml`:

```toml
[module]
[[module.imports]]
path = "github.com/probonas/hugo-theme-windowsxp"
```

Then run:

```bash
hugo mod get -u
```

## Configuration

### Minimal `hugo.toml`

```toml
baseURL = 'https://example.com/'
title = 'My Website'
theme = 'hugo-theme-windowsxp'

[params]
name = 'Your Name'
bio = 'A short tagline'
avatar = 'https://example.com/avatar.jpg'

mainSections = ['blog']

[menu]

[[menu.main]]
identifier = 'about'
name = 'About'
url = '/about/'
weight = 10
[menu.main.params]
icon = 'UserAccounts'
windowTitle = 'About Me'

[[menu.main]]
identifier = 'blog'
name = 'Blog'
url = '/blog/'
weight = 20
[menu.main.params]
icon = 'MyDocuments'
windowTitle = 'My Documents'

[[menu.main]]
identifier = 'projects'
name = 'Projects'
url = '/projects/'
weight = 30
[menu.main.params]
icon = 'MyComputer'
windowTitle = 'My Computer'
xpLayout = 'icons'
```

### Site Parameters

| Parameter | Description | Default |
|---|---|---|
| `params.name` | Display name (start menu, about page) | Site title |
| `params.bio` | Short bio line | — |
| `params.description` | Meta description | — |
| `params.avatar` | Avatar image URL | — |
| `params.github` | GitHub username | — |
| `params.linkedin` | LinkedIn username | — |
| `params.resumeURL` | Resume PDF path (adds desktop icon) | — |
| `params.mainSections` | Sections for blog-like content | `["blog", "posts"]` |
| `params.favicon` | Favicon path | `favicon.ico` |

### XP-Specific Parameters

| Parameter | Description | Default |
|---|---|---|
| `params.xp.wallpaper` | Custom wallpaper image path | `/bliss.jpg` |
| `params.xp.homeWindow` | URL loaded in the homepage window | `/about/` |
| `params.xp.homeWindowTitle` | Title of the homepage window | `About Me — System Properties` |
| `params.xp.homeWindowIcon` | Icon for the homepage window | `SystemProperties` |

### Menu Parameters

Each `menu.main` entry supports these params:

| Parameter | Description | Default |
|---|---|---|
| `icon` | XP icon name (filename without `.png`) | `FolderClosed` |
| `windowTitle` | Title shown in the XP window title bar | Menu name |
| `xpLayout` | List page layout: `list` or `icons` | `list` |
| `desktopIcon` | Show as desktop icon (`true`/`false`) | `true` |
| `desktopLabel` | Custom label for the desktop icon | Menu name |

### Available Icons

The following icons are included in `static/icons/xp/`:

`Back`, `Briefcase`, `CommandPrompt`, `ControlPanel`, `Desktop`, `Explorer`, `FolderClosed`, `FolderOpened`, `FolderView`, `Forward`, `GenericDocument`, `GenericTextDocument`, `Go`, `HelpandSupport`, `InternetExplorer6`, `InternetShortcut`, `LocalDisk`, `Logout`, `MyComputer`, `MyDocuments`, `NetworkConnections`, `Notepad`, `Programs`, `RecentDocuments`, `Run`, `Search`, `Shortcutoverlay`, `Shutdown`, `SystemProperties`, `TourXP`, `Up`, `UserAccounts`, `Volume`, `WindowsFlag`, `WindowsPictureandFaxViewer`

## Content Structure

```
content/
├── _index.md
├── about/
│   └── index.md          # layout: "about" for the System Properties look
├── blog/
│   ├── _index.md
│   ├── my-post.md
│   └── another-post.md
└── projects/
    ├── _index.md
    ├── project-a.md
    └── project-b.md
```

### About Page

Create `content/about/index.md` with `layout: "about"` in front matter to get the System Properties-style about page (no toolbar chrome, profile header with avatar).

### External Links

For project pages or posts that link to an external URL, add `externalUrl` to the front matter:

```yaml
---
title: "My OSS Project"
externalUrl: "https://github.com/user/repo"
---
```

### Adding Custom Sections

Add a new section by:

1. Creating `content/your-section/_index.md`
2. Adding a menu entry in `hugo.toml`:

```toml
[[menu.main]]
identifier = 'your-section'
name = 'Papers'
url = '/your-section/'
weight = 40
[menu.main.params]
icon = 'FolderClosed'
windowTitle = 'My Papers'
```

The section automatically gets a desktop icon, start menu entry, sidebar links, and an Explorer window.

## Customization

### Custom Wallpaper

Place your image in `static/` and set:

```toml
[params.xp]
wallpaper = '/your-wallpaper.jpg'
```

### Override CSS

Create `assets/css/xp.css` in your site root to override the theme's styles. Hugo's asset pipeline will use your file instead.

## Development

To run the example site:

```bash
cd exampleSite
hugo server --themesDir ../..
```

## License

MIT
