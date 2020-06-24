# Markdown

## Formatting

Leading and trailing spaces are usually removed except code. Special characters could be escaped by \ backslash character.

Headings: # First level header, ## Second, ..., ###### Sixth level (a sequence of = or - could be used for 1st or 2nd level)

### ### H3

A paragraph is separated by blank lines and could be single line or multiple lines. Paragraph **\*\*raw\*\*** content is parsed as inlines, .. two spaces or \\\
replaces with a hard line break.

- Inlines: **\*\*Strong emphasis\*\***, _\_emphasis\_ ,_ ~~\~\~strikethrough\~\~~~ _(GitHub's extension)_, `` `code` `` or ` ``code`` `
  - Entities: &amp;amp; = &amp;, &amp;copy; = &copy;, &amp;#35 = &#35;, &amp;#2B21; = &#X2B21; (_See [WHATWG: Entity Reference](https://html.spec.whatwg.org/entities.json), UTF8 reference or ASCII reference_)
- Links: \[Link text](URI "Title")
  - Examples:
    - \[Markdown cheat sheet](https://github.com/xebis/cheatsheets/blob/master/Markdown.md "Absolute link") = [Markdown cheat sheet](https://github.com/xebis/cheatsheets/blob/master/Markdown.md "Absolute link")
    - \[relative link without title](Markdown.md) = [relative link without title](Markdown.md)
  - Autolinks: http://example.com, \<http://example.com>, \<email@example.com>
  - Autolinks _(GitHub's extension)_: example.com email@example.com
  - @user user or @team name reference _(GitHub's extension)_
  - \[Formatting](#formatting) = [Formatting](#formatting)
  - \[Markdown Formatting](Markdown.md#formatting) = [Markdown Formatting](Markdown.md#formatting)

\> Block quotes

> Block quotes

- Lists: 1. numbered, could start by any integer, \*, -, + bulleted

  - Intendation is your friend
  - Todo lists, checklists:
    - [x] - \[x\] Completed list item _(GitHub's extension)_
    - [ ] - \[ \] Incomplete list item _(GitHub's extension)_

- Images: \!\[Alt](source "Title"), e.g.: \!\[Octocat](https://techbootcamp.github.io/book/images/depl/github-logo-transparent.jpg "Octocat")

![Octocat](https://techbootcamp.github.io/book/images/depl/github-logo-transparent.jpg "Octocat")

- [Emojis](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md) :muscle::+1::wink:
- Escape character \ for { \* \_ \` \~ \[ } in text and { \# \- } at the line beginning
- Thematic break: \*\*\* --- \_\_\_ (three or more characters)

---

### Code

....Code block // Replace dot with space, or alternatively:

````
```
Code block, ~~~ works as well
```
````

Or (please note 4 spaces at the beginning):

        Code block

Add language after ``` or ~~~ code block beginning to enable code highlighting

````javascript
// Start with ```javascript
const dummy = () => {
  /* I do nothing */
};
````

### HTML

```html
<p>
  <strong>_I am strong!_</strong> **Nested** *formatting* does not `work` here.
</p>
```

<p>
  <strong>_I am strong!_</strong> **Nested** *formatting* does not `work` here.
</p>

```html
<p>
  <strong>_I am strong!_</strong>

  **Nested** _formatting_ `works` when separated from HTML tags by empty line.
</p>
```

<p>
  <strong>_I am strong!_</strong>

**Nested** _formatting_ `works` when separated from HTML tags by empty line.

</p>

_(GitHub's extension):_ Some HTML elements are filtered out: \<title> \<textarea> \<style> \<xmp> \<iframe> \<noembed> \<noframes> \<script> \<plaintext>

### Tables _(GitHub's extension)_

```
| Column | Left-aligned column | Center-aligned column | Right-aligned column |
| ------ | :------ | :------: | ------: |
| Row 1 | Left | Center | Right |
| **Nested** | *formatting* | `works` |
```

Result:

| Column     | Left-aligned column | Center-aligned column | Right-aligned column |
| ---------- | :------------------ | :-------------------: | -------------------: |
| Row 1      | Left                |        Center         |                Right |
| **Nested** | _formatting_        |        `works`        |

- Include at least three hyphens in each column of the header row

## Sources

- [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)
- [GitHub Guide: Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
- [GitHub Doc: Basic writing and formatting syntax](https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax)
- [GitHub Doc: Organizing information with tables](https://help.github.com/en/github/writing-on-github/organizing-information-with-tables)
- [GitHub Doc: Creating and highlighting code blocks](https://help.github.com/en/github/writing-on-github/creating-and-highlighting-code-blocks)
- [Linguist Doc: Syntax highlighting keywords](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)
- [GitHub Doc: Autolinked references and URLs](https://help.github.com/en/github/writing-on-github/autolinked-references-and-urls)
- [WHATWG: Entity Reference](https://html.spec.whatwg.org/entities.json)
- [GitHub / @ikatyang: Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md)
