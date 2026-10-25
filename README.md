# Explorer Color Tags

A [Windhawk](https://windhawk.net/) mod that brings Finder-like color tags to
Windows File Explorer.

![Colored dots after file names and colored pills in the Tags column](docs/explorer-color-tags.png)

*Colored dots appear beside the name; matching color pills appear in the Tags
column.*

![The Tags submenu in the classic file context menu](docs/menu.png)

## Features

- Press `Alt+1` through `Alt+8` to toggle one of eight color tags on the selected
  files or folders.
- Press `Alt+0` to remove all tags from the selection.
- Tags work for every file type, including ZIP, EXE, image, video and
  extensionless files, plus folders.
- Up to three colored dots appear directly after the item name.
- Details view gets a **Tags** column with rounded, colored, uppercase pills.
- The Tags column can be enabled automatically or shown only in folders where
  you add it manually.
- The classic context menu exposes the same tags.
- Tag names and colors are configurable in Windhawk.

## Requirements

- Windows 11 x64.
- Windhawk 1.7.3 or newer.
- The classic File Explorer context menu for the right-click submenu.

## Install manually

1. Open Windhawk and create a new local mod.
2. Replace its source with
   [`explorer-color-tags.wh.cpp`](explorer-color-tags.wh.cpp).
3. Compile and enable the mod.
4. Disable and re-enable it, then open a new File Explorer window.

## Default shortcuts

| Shortcut | Tag | Color |
| --- | --- | --- |
| `Alt+1` | Important | `#E81123` |
| `Alt+2` | Work | `#0078D4` |
| `Alt+3` | Personal | `#107C10` |
| `Alt+4` | Later | `#FF8C00` |
| `Alt+5` | Archive | `#8764B8` |
| `Alt+6` | Review | `#C8A000` |
| `Alt+7` | Home | `#00B7C3` |
| `Alt+8` | Temporary | `#767676` |
| `Alt+0` | Remove all tags | |

Pressing the same shortcut again removes that tag. Tag names, colors and the
Tags column width can be changed in the mod settings. **Automatically add Tags
column** is disabled by default; enable it to add the column to every folder,
or show it per folder from the Explorer column-header menu.

## How it works

The mod keeps its own tag index instead of relying on the Windows
`System.Keywords` property. That property only works when a file type has a
compatible property handler, which excludes many common formats and folders.

Tags are indexed by file identity with a path fallback. A compact child-window
overlay draws the dots after item names and the colored pills in the native
**Tags** column. File contents are never modified.

The internal shortcut record remains available as a rebuildable index, but it
is not shown in the navigation pane.

## Known limitations

- The visual overlay depends on the current File Explorer DirectUI layout and
  may need updating after a major Windows change.
- The **Tags** column is custom-drawn. Its native sort and filter commands do
  not know the mod's tag values.
- Tagged files are not indexed with Windows Search.
- Tags are local to Windows and are not written into the files themselves.
- Do not put the internal tags folder in OneDrive, Dropbox or another actively
  synchronized location. A temporarily missing shortcut looks like a removed
  tag.
- The Windows 11 modern context menu is not extended; use the classic menu.

## Build check

The repository includes `compilar.sh`, which compiles with Windhawk's bundled
compiler and flags:

```sh
sh compilar.sh explorer-color-tags.wh.cpp
```

The check does not install or load the generated DLL.

## Attribution

This project is based on
[Explorer Tags](https://github.com/buedgik/explorer-tags) by `buedgik` and keeps
its MIT-licensed storage and context-menu foundations. The colored overlay,
Tags column, keyboard workflow and removal of the navigation-pane tag
navigation were added in this fork.

## License

MIT. See [LICENSE](LICENSE).
