# Passenger themes

Themes and code colour schemes for [Passenger](https://github.com/Zaneris/passenger), the IDE for C# and modern .NET.
Every Passenger lists this repository from the start: open Settings | Appearance, open the Theme or Colour scheme list,
and choose. A theme you choose is kept on your machine, so it works offline afterwards; Refresh under Theme sources takes
a newer copy.

A theme sets the colours and shapes of Passenger's window and code, Dark and Light; a code colour scheme sets only the
code's colours, under any theme. Both are JSON data, never code: Passenger reads each against its own format and uses
nothing it cannot check.

## The themes

- **Harbour**: Warm and quiet: the app icon's teal on linen by day and a warm charcoal by night, its amber for what wants a glance. Rounder than Passenger's own, the open editor tab a card in the editor's colour joined to it, round badges and chips, and popups with no crown, its parameters in italics and six colours for its brackets. The tide comes in along the editor's foot and the Welcome screen, a low sun glinting on it.
- **Sorbet**: Soft pastels on a dusky plum by night and a pale lavender paper by day, a mauve accent and peach for the caret; round as a scoop, peach, mauve and mint light in its corners, its comments and parameters in italics.
- **Nocturne**: A violet night of hot pink keywords, lemon strings and mint calls, its colours those of Dracula Theme by the Dracula Theme team (dracula-theme.theme-dracula on Open VSX, MIT), under pill shapes, a crescent moon and stars across the Welcome screen, the frame and the tool windows, and the Explorer on the right.
- **Saffron**: Ink-dark slate with saffron and tangerine, sky-blue types and lime strings; by day the same on chalk. A sunburst rises behind the Welcome screen and the window's frame, and the title bar glows from ink into ember.
- **Bonbon**: A cool grey night lit with candy pink, butter, mint and sky, its day a blush-white page; round and soft, with sprinkles tossed across the tool windows and the Welcome screen and the terminal open below.
- **Ledger**: Plain neutral greys with a clear blue accent, coral keywords and navy or ice strings: quiet, for long days. Dense and square-cornered on a ledger's graph paper, its tool windows laid out for the day's accounts.
- **Slate**: A soft blue-grey with lilac keywords, sage strings, cornflower calls and wheat types, its colours those of One Dark Pro by Binaryify (zhuangtongfa.material-theme on Open VSX, MIT), under card shapes, a survey map's contours behind the code, and the terminal and problems open below.
- **Orbit**: Deep space with signal teal, aqua and periwinkle and a warm sand for strings; by day a pale observatory. Orbits circle a sun off the corner of every editor, the title bar runs teal into periwinkle, and the editor's tabs stand down its side.
- **Nightjar**: A navy night sky of violet keywords, apricot strings and seafoam members, its colours those of Night Owl by Sarah Drasner (sdras.night-owl on Open VSX, MIT), under card shapes, a nightjar crossing the moon on the Welcome screen and behind the tool windows, and the editor's tabs down its side.
- **Moss**: A green-grey woodland, sage and leaf with honey strings and clay types, easy on the eye night and day; ferns grow from the editor's foot, and it opens calm, the Explorer alone.
- **Phosphor**: A near-black terminal glass with electric lime, cyan and violet; by day crisp ink on white. Sharp-cornered, a screen's scanlines behind the code and a lime glow round its popups by night, the terminal open below.

## The code colour schemes

- **Reef**: Sky-blue keywords, leaf-green comments, sand strings, coral numbers and mint methods on a dark theme, deeper inks of the same on a light one; the editor's ground and gutter stay the theme's, so the window's areas stay told apart by shade.

## Your own source

Any folder, GitHub repository or https address holding a `passenger-themes.json` like this one's is a source. Add it in
Settings | Appearance | Theme sources: a folder by its full path, a repository as `owner/name` (its raw files are read at
its default branch), or the https address the index sits under. Passenger reads a source only when you look at its
themes, choose one or press Refresh. A single file of your own goes in with Add from File beside the Theme or Colour scheme
list.

## A source

A source's root holds `passenger-themes.json`, which lists its files by paths inside it (folders joined by `/`, no `..`,
no absolute path or address, each ending `.json`). A theme's images go beside its file.

```json
{
  "format": 1,
  "themes": ["Harbour.json", "Sakura/theme.json"],
  "codeColours": ["Dusk.json"]
}
```

## A theme

```json
{
  "format": 1,
  "name": "Harbour",
  "description": "Warm and quiet: teal on linen by day, a warm charcoal by night.",
  "tokens": { "ControlRadius": 8, "TabMargin": [1, 6, 1, 0] },
  "dark": { "Frame": "#151311", "Accent": "#2CB5A3" },
  "light": { "Frame": "#EEE8DC", "Accent": "#0F766E" }
}
```

`name` is required, at most 64 characters; `description` is optional, at most 1,000. `tokens` holds values for both
variants, `dark` and `light` for one each; a token goes in `tokens` or in `dark` and `light`, never both. Any of the
three may be left out, as may `background`, `fonts`, `languages`, `layout` and `vscode` below.

A token is named as its key in [Tokens.axaml](https://github.com/Zaneris/passenger/blob/main/src/Passenger.App/Theme/Tokens.axaml) without `Passenger.`:
`Frame`, `Editor.Background`, `Syntax.Keyword`, `SyntaxStyle.Comment`, `ControlRadius`, and the margins
`EditorTextPadding` (between the editor's gutter and its text), `ToolHeaderHeight`, `ToolTitleMargin` and
`DialogFooterPadding`. Tokens.axaml gives every token
and its default value; a token takes the kind of value its default is:

| The default | The value |
|---|---|
| a colour (`SolidColorBrush`) | `"#RRGGBB"`, `"#AARRGGBB"`, or `{"colour": "#RRGGBB", "opacity": 0.2}` (opacity 0 to 1) |
| a gradient (`LinearGradientBrush`) | a colour, or `{"start": [0, 0], "end": [1, 0], "stops": [{"offset": 0, "colour": "#1B3270"}, {"offset": 1, "colour": "#0E4552"}]}`: points as fractions of the area, 2 to 16 stops with offsets rising from 0 to 1 |
| shadows (`BoxShadows`) | `"X Y BLUR SPREAD #AARRGGBB"` (BLUR and SPREAD may be left out, `inset` may lead), up to 8 joined by commas, or `"none"` |
| a radius (`CornerRadius`) | a number for every corner, or `[top left, top right, bottom right, bottom left]`, 0 to 1000 |
| a thickness (`Thickness`) | a number for every side, or `[left, top, right, bottom]`, -1000 to 1000 |
| a number (`x:Double`) | a number, 0 to 1000 |
| a syntax style (`x:String`) | `"Normal"`, `"Bold"`, `"Italic"` or `"Bold Italic"` |

Beside those, a theme may give three tokens Passenger's own theme leaves out, `Syntax.Brace4`, `Syntax.Brace5` and
`Syntax.Brace6`: rainbow braces take turns in as many colours as a theme gives, three to six, a bracket's depth cycling
through exactly those (`Syntax.Brace5` counts only after `Syntax.Brace4`, `Syntax.Brace6` only after both), so a theme of
five draws the sixth depth in `Syntax.Brace1`'s colour. It may also give `SyntaxStyle.Parameter`, how a parameter is set.
`Syntax.Parameter`, `Syntax.Local`, `Syntax.Namespace` and `Syntax.Operator` are drawn in the code's plain words in
Passenger's own theme; a file that leaves them out draws them in its own `Editor.Text`, unless it is laid over a VS Code
theme, whose own they are.
A file that leaves out `ButtonHover`, `ButtonPressed` or `AccentPressed`, a button's grounds under the pointer and
pressed, has them worked out in each variant from its own colours, as Passenger's themes work them out: a plain button's
are its `Hover` and `Selected` laid over its `Button`, and the default button's pressed goes as far past its `AccentHover`
as that is from its `Accent`.

### Its background picture

```json
"background": {
  "image": "dusk.webp",
  "opacity": 0.25,
  "tint": { "colour": "#101830", "strength": 0.2 },
  "places": ["editor", "toolWindows", "frame", "welcome"],
  "fit": "cover",
  "align": "bottom right",
  "light": { "image": "day.jpg", "opacity": 0.2 }
}
```

`image` is a picture beside the theme's file (its folders joined by `/`, no `..`): a PNG, JPEG or WebP of at most 8 MB,
at most 8192 pixels along a side and 16 million pixels in all. Passenger reads its size from its
header before anything decodes it, then decodes it with its own decoders. The rest may be left out:

- `opacity`, how much of the picture shows, 0 to 0.3 (0.15 if left out). The picture is drawn over the area, its text and
  its ground alike, so every glyph keeps at least 70% of its contrast with its ground whatever the picture holds.
- `tint`, a colour washed over the picture at a `strength` from 0 (none) to 1 (the colour alone; 0.5 if left out).
- `places`, where it is drawn: one or more of `editor` (each editor, fitted to it), `toolWindows` (each tool window's
  page), `frame` (the toolbar, the stripes, the editor tabs' strip and the status bar, fitted to the whole window so they
  show one picture) and `welcome` (the Welcome screen). `["editor"]` if left out.
- `fit`: `cover` (fills the area, its overflow cut off; the default), `contain` (whole inside the area), `tile` (at its own
  size, repeated) or `centre` (at its own size, once).
- `align`: `centre` (the default), or `top`, `bottom`, `left`, `right`, or one of each, `bottom right`.
- `dark` and `light` give what differs under one variant, the rest as above, or `"none"` for no picture there.

The picture is kept beside the theme when the theme is chosen, so it draws offline too.

### Its fonts

```json
"fonts": { "code": { "family": "Fira Code", "size": 14 }, "window": { "family": "Inter" } }
```

The code's and the window's family, each by its name, and the code's `size` in points (6 to 48). A family or size you
choose in Settings wins wherever you chose one; Reset Font Size goes back to the theme's size. A family not installed
here leaves Passenger's own.

### The code's colours by language

```json
"languages": {
  "csharp": { "dark": { "Syntax.Keyword": "#FF7AB8" }, "light": { "Syntax.Keyword": "#B0306A" } },
  "json": { "tokens": { "SyntaxStyle.Comment": "Italic" } }
}
```

A language is named by its id as Passenger knows it (`csharp`, `xaml`, `msbuild`, `xml`, `json`, `aspnetcorerazor`, `gdscript`, `typescript`,
`css`, `markdown`, …), and gives the code's tokens (`Editor.*`, `Syntax.*`, `SyntaxStyle.*`, `Diff.*`) in `tokens`,
`dark` and `light` as a theme gives its own. They are laid over the file's own tokens in that language's editors. A
language this Passenger does not know is passed over and named.

### Its default layout

```json
"layout": {
  "places": { "rightTop": ["explorer", "commit"], "bottomLeft": ["build", "run"], "bottomRight": ["problems"] },
  "open": ["explorer", "build", "problems"],
  "sizes": { "left": 260, "right": 320, "bottom": 220 },
  "editorTabs": "left",
  "toolWindows": "tabs",
  "closedWindows": "leave",
  "findResults": "window"
}
```

Where the tool windows dock when nobody has arranged them: what a window opens on before any layout is kept, and what
Window | Layout Settings | Restore Default Layout goes back to. A layout you arrange yourself always wins, and is kept as
yours whatever theme you choose; choosing another theme moves, window by window, each one still standing where the theme
before put it, opens or hides it as the new theme says unless you opened or hid it yourself, and gives an area you never
resized the new theme's size. What you moved, floated, put among the editors, opened, hid or resized stays as you left it.

- `places` names, for any of `leftTop`, `leftBottom`, `rightTop`, `rightBottom`, `bottomLeft` and `bottomRight`, the tool
  windows docked there in their order, before those the theme leaves where Passenger puts them. A window docks in one
  place. The windows are named by their ids: `explorer`, `structure`, `bookmarks`, `commit`, `run`, `debug`, `tests`,
  `build`, `problems`, `find`, `git`, `nuget`, `terminal`, `localHistory`, `containers`, `profiler`, `hierarchy`,
  `endpoints`, `requests`, `liveTree`, `game`, `aspire` and `migrations`. `editor` names those shown as tabs among the
  editors instead, their icons on the stripes where Passenger puts them.
- `open` lists the windows open at the start, every other closed; left out, Passenger's own open (the Explorer). A place
  shows one window, the first in its order.
- `sizes` gives the left and right areas' widths and the bottom one's height, each 100 to 2000 pixels; one left out is
  Passenger's own.
- `editorTabs` stands each editor's tabs in a row across its `top`, or in a column down its `left` or `right` side; left
  out, across the top.
- `toolWindows` names and switches the tool windows by their `icons` on the stripes alone, or by `tabs`, no stripe
  standing: titled tabs along the foot of each place where several dock, and a hidden window's tab along the window's
  edge, which opens it over the editors; left out, by icons. A file still giving `stripeIcons`, which once chose the
  icons kept beside titled tabs, reads as though it gave none.
- `closedWindows` says what closing a tool window by its × does to its icon or tab: `keep` it, as hiding it does, or
  `leave` until the window is opened again from View | Tool Windows, Find Action or its keys; left out, keep.
- `findResults` keeps Find in Files' matches in its `popup` alone, or in the Find `window` as well once one is gone to,
  a tab to go back to, where the places Go to Declaration and the like find to choose from are listed too; left out, the
  popup.

What the layout arranges beyond where the windows dock (`editorTabs`, `toolWindows`, `closedWindows`, `findResults`) is each a setting of Settings | Appearance: the
theme's is the default there, and the place you choose wins over it whatever theme you choose, until you choose Theme
default again.

A window or place this Passenger does not have is passed over and named.

## A code colour scheme

The same shape as a theme, giving only the code's tokens: `Editor.*`, `Syntax.*`, `SyntaxStyle.*` and `Diff.*`. It is
laid over the theme in force; `dark` gives its colours under a dark theme and `light` under a light one.

## A theme over a VS Code colour theme

A theme may name a VS Code colour theme as its base, and give only what it changes:

```json
{
  "format": 1,
  "name": "Dusk over Dracula",
  "vscode": { "id": "dracula-theme.theme-dracula", "theme": "Dracula Theme", "version": "2.25.1" },
  "tokens": { "ControlRadius": 0, "Accent": "#FF79C6" }
}
```

- `id` is the extension's [Open VSX](https://open-vsx.org) id, `publisher.name` (open-vsx.org/extension/PUBLISHER/NAME).
- `theme` is the colour theme's label in that extension, as its `package.json` names it under `contributes.themes`.
- `version`, optional, pins the extension's version; left out, Passenger's Refresh takes the newest.
- Or `"vscode": { "file": "dracula.json" }` names a VS Code theme's JSON beside the theme's file (the files it includes
  beside it too).

The VS Code theme gives the code's colours (its token and semantic token colours, its bracket colours up to six) and the
window's where it has them; the theme's own tokens, background, fonts, languages and layout are laid over it. It shows in
the VS Code theme's variant, dark or light, whatever Passenger's Dark or light setting says. Passenger fetches the base
with the theme and keeps it beside it, so it draws offline. Every word and mark is held to WCAG AA: a colour too faint to
read is moved in lightness only as far as it must. See
[docs/themes.md](https://github.com/Zaneris/passenger/blob/main/docs/themes.md) for the colours each VS Code key gives.

## How Passenger reads a file

- Plain JSON in UTF-8: no comments, no trailing commas, no member given twice, at most 1 MB, nested at most 10 deep.
- A file that is not JSON, gives no `format` or another than 1, or gives a value of the wrong kind is refused whole,
  saying the file, the token and what it takes; nothing of it is used.
- A member or token this Passenger does not know is passed over and named, so a typo shows and a file written for a
  later Passenger still reads.

## Proposing a theme

1. Fork this repository and add your theme's file, named as its theme (`Dusk.json`), and its line in `themes` (or
   `codeColours` for a scheme) in `passenger-themes.json`.
2. Try it before you open a pull request: add your fork's folder as a source in Settings | Appearance | Theme sources,
   choose your theme, and look at it Dark and Light. Settings says why a file is refused, and names any token it does
   not know, so a typo shows.
3. Give every colour a person reads at least WCAG AA contrast on what it is drawn on (4.5:1 for words, 3:1 for icons,
   focus rings and the caret), Dark and Light: Passenger's own tests hold its themes to that.
4. Open a pull request saying what your theme looks like, with a screenshot of each variant. A theme is data under this
   repository's MIT licence: give only what you made or may share under it.

The ten generated themes (Sorbet to Phosphor) are written from palettes by Passenger's `tools/themes.py`
(`just themes FOLDER` in a Passenger checkout, FOLDER this repository's); change a palette there rather than its file.
Harbour and Reef are written by hand. The pictures in `pictures/` are drawn by Passenger's `tools/theme-pictures.py` (the
same recipe) from plain geometry and seeded randomness: tide lines, soft glows, a moon and stars, a sunburst, sprinkles,
graph paper, contour lines, orbits, a fern grown by Barnsley's maps and scanlines, nothing taken from elsewhere, and they
are this repository's under its licence.

Nocturne, Slate and Nightjar are laid over VS Code colour themes fetched from Open VSX by their ids, so this repository
carries none of their files: Nocturne over Dracula Theme (`dracula-theme.theme-dracula`, MIT, the Dracula Theme team),
Slate over One Dark Pro (`zhuangtongfa.material-theme`, MIT, Binaryify) and Nightjar over Night Owl (`sdras.night-owl`,
MIT, Sarah Drasner). Their colours are those themes' authors'; what Passenger sets over them, the shapes, fonts,
pictures and layouts, is this repository's.

## Licence

MIT, as [LICENSE](LICENSE) says.
