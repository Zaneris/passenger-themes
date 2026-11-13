# Passenger themes

Themes and code colour schemes for [Passenger](https://github.com/Zaneris/passenger), the IDE for C# and modern .NET.
Every Passenger lists this repository from the start: open Settings | Appearance, open the Theme or Colour scheme list,
and choose. A theme you choose is kept on your machine, so it works offline afterwards; Refresh under Theme sources takes
a newer copy.

A theme sets the colours and shapes of Passenger's window and code, Dark and Light; a code colour scheme sets only the
code's colours, under any theme. Both are JSON data, never code: Passenger reads each against its own format and uses
nothing it cannot check.

## The themes

- **Harbour**: Warm and quiet: the app icon's teal on linen by day and a warm charcoal by night, its amber for what wants a glance. Rounder than Passenger's own, the open editor tab a card in the editor's colour joined to it, round badges and chips, and popups with no crown.
- **Sorbet**: Soft pastels on a dusky plum by night and a pale lavender paper by day, a mauve accent and peach for the caret.
- **Nocturne**: A violet night of hot pink keywords, lemon strings and mint calls, its day a lilac-tinted page.
- **Saffron**: Ink-dark slate with saffron and tangerine, sky-blue types and lime strings; by day the same on chalk.
- **Bonbon**: A cool grey night lit with candy pink, butter, mint and sky, its day a blush-white page.
- **Ledger**: Plain neutral greys with a clear blue accent, coral keywords and navy or ice strings: quiet, for long days.
- **Slate**: A soft blue-grey with lilac keywords, sage strings, cornflower calls and wheat types, day and night alike.
- **Orbit**: Deep space with signal teal, aqua and periwinkle and a warm sand for strings; by day a pale observatory.
- **Nightjar**: A navy night sky of violet keywords, apricot strings and seafoam members; its day a cool white page.
- **Moss**: A green-grey woodland, sage and leaf with honey strings and clay types, easy on the eye night and day.
- **Phosphor**: A near-black terminal glass with electric lime, cyan and violet; by day crisp ink on white.

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
three may be left out.

A token is named as its key in [Tokens.axaml](https://github.com/Zaneris/passenger/blob/main/src/Passenger.App/Theme/Tokens.axaml) without `Passenger.`:
`Frame`, `Editor.Background`, `Syntax.Keyword`, `SyntaxStyle.Comment`, `ControlRadius`. Tokens.axaml gives every token
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

Beside those, a theme may give `Syntax.Brace4`, `Syntax.Brace5` and `Syntax.Brace6`: bracket pairs take turns in as many
colours as a theme gives, three to six, so a theme of five draws the sixth depth in `Syntax.Brace1`'s colour
(`Syntax.Brace5` counts only after `Syntax.Brace4`, `Syntax.Brace6` only after both). It may also give
`SyntaxStyle.Parameter`. `Syntax.Parameter`, `Syntax.Local`, `Syntax.Namespace` and `Syntax.Operator` left out are drawn
in the theme's own `Editor.Text`.

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
Harbour and Reef are written by hand.

## Licence

MIT, as [LICENSE](LICENSE) says.
