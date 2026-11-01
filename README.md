# HTML syntax for TerminalCode

Syntax highlighting for HTML (`.html`, `.htm`, `.xhtml`) as a [TerminalCode](https://github.com/Tim-kieboom/TerminalCode) plugin.

It is a language and nothing else: there is no code in it and no pane. The plugin is

- `html.wasm`, the tree-sitter grammar built for WebAssembly,
- `manifest.toml`, which says which files are HTML (`[language]`: `extensions`) and has the
  highlight query as text.

TerminalCode loads the grammar in its sandbox (plugin API 1.12, TerminalCode 0.11.0 or later; 1.13 for what is inside `<script>` and `<style>`) and colors the
files with the query, using the colors of your theme (`syntax.keyword`, `syntax.string`, ... in the theme file).

## Use

"Plugins: Manage", install **HTML**, and turn it on. Files ending in `.html`, `.htm`, `.xhtml` are colored when they are opened.

## JavaScript and CSS inside

The text of a `<script>` is colored as JavaScript, and the text of a `<style>` as CSS, with the colors of those languages
(`injections` in `manifest.toml`; plugin API 1.13, TerminalCode 0.12.0 or later). JavaScript is built into the editor. For the
CSS the [CSS plugin](https://github.com/Tim-kieboom/trcode-plugin-css-syntax) has to be on as well; without it the text of a
`<style>` keeps the plain color. Attributes such as `style="..."` and `onclick="..."` are not colored as CSS or JavaScript.

## Where the grammar comes from

The grammar and the query are those of [tree-sitter/tree-sitter-html](https://github.com/tree-sitter/tree-sitter-html) at master 73a3947 (after v0.23.2) (MIT,
`LICENSE-GRAMMAR`). The module was built from that revision with the tree-sitter CLI:

```sh
git clone https://github.com/tree-sitter/tree-sitter-html && cd tree-sitter-html
git checkout 73a3947
tree-sitter build --wasm -o html.wasm
```

A new version of the grammar needs a new `version` in `manifest.toml` and a release (the module is the file the
installer checks). The query is copied into the manifest with its patterns in the opposite order (TerminalCode takes
the first of two patterns on the same text; the grammar's file is written for the last), and the capture names are those of the theme (`tag` is `keyword`).

## Licence

The plugin is MIT or Apache-2.0, as the other plugins; the grammar is MIT (`LICENSE-GRAMMAR`).
