# Highlight.js theme depending on dark mode
Styles for code blocks processed with highlight.js are switched based on dark mode or light mode.
Currently, following [styles](https://github.com/highlightjs/highlight.js/tree/master/src/styles) are set:
 * light: `tomorrow.css`
 * dark: `an-old-hope.css`

## Switch themes
To switch to different styles, you need to modify the orignal highlight.js [stylesheets](https://github.com/highlightjs/highlight.js/tree/master/src/styles) so that they are only active when the `.dark` class is present (for dark mode) in `<body>` or not (light mode). 
This can be done using the following sed snippets.
It is important that only one stylesheet is present for light mode and one file for dark mode!

### Set dark mode theme
Assuming you would like to enable the hljs theme `dark.css` run the following commands.
```bash
sed  s,^\\.,\.dark\ \.,g dark.css > tmp
mv tmp hljs-dark.css
```
Additionally, find the `background` key in `.hljs` and delete it or comment it out. It will interfere with the variable set in `theme-vars.css`.

### Set light mode theme
Assuming you would like to enable the hljs theme `light.css` run the following commands.
```bash
sed s,^\\.,body:not\(\.dark\)\ \.,g light.css > tmp
mv tmp hljs-light.css
```
Additionally, find the `background` key in `.hljs` and delete it or comment it out. It will interfere with the variable set in `theme-vars.css`.

## Update 09.12.2021
After merge with upstream `papermod` 
 * the syntax highlighting in light mode doesn't quite work. There is some problem with the css.
 * Also, if `an-old-hope.min.css` is renamed to the same name but without `.min.`, hugo cannot compile... Some hard coded dependency?
