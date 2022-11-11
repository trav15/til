
# Markdown

## Layout tips

- Use blank lines between before and after headings:
```
Try to put a blank line before...

# Heading

...and after a heading.
```

- The same goes for blockquotes:
```
Try to put a blank line before...

> This is blockquoute
>> This is a nested blockquote

...and after a blockquote.
```

- Don't put tabs or spaces in front of paragraphs
- Use asterisks (\*\*bolding\*\*) for **bolding** instead of underscores because MD apps don't agree on how to handle underscores in the middle of a word. Same with *italicizing* in the middle of a word.
- ==Highlighting== - This isn’t common, but some Markdown processors allow you to highlight text. To highlight words, use two equal signs (==) before and after the words.
- Text can’t be underlined in Markdown. Although this is possible using the `<u>` tags in HTML, it’s usually inadvisable to do so. That’s because underlined text is used for hyperlinks online and it’s best to avoid confusing the two uses.
- For fenced code blocks use \`\`\` before and after the code block. You can add ***syntax highlighting*** by adding an optional language identifier (ex. js, ts, html, jsx, etc.) after the \`\`\`:
````
```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
````
- Use quadruple backticks (\`\`\`\`) when you want the triple backticks (\`\`\`) to display in the code block. For example to display the above example.

## Links/anchors

- For links to a heading section within the same file use:
  - `[Example Title](#example-title)` 
  - The amount of `#` stays at one regardless of heading level (`#`, `##`, `###`). 
  - The heading should be downcased, spaces changed to hyphens, and removed anything not a letter, hyphen, or space. If this id is not unique, you add "-1", "-2", and so forth to the header.
- For links to a heading section in a different file add `#heading` after the file name:
  - `[Different File Title](differentfile.md/#different-file-title)`

## Footnotes

For footnotes in GitHub use bracket syntax:
```
Here is a simple footnote[^1].

Using words instead of numbers for reference[^words].  

[^1]: My simple reference.
[^words]: 
  Named footnotes will still render with numbers instead of the text but allow easier identification and linking.  
  This footnote also has been made with a different syntax using 4 spaces for new lines.
```
Renders as:

Here is a simple footnote[^1].

Using words instead of numbers for reference[^words]. 

Be sure to use lowercase for `[^words]`

[^1]: My simple reference.
[^words]: 
    Named footnotes will still render with numbers instead of the text but allow easier identification and linking.  
    This footnote also has been made with a different syntax using 4 spaces for new lines.

## *Resources*

- [Markdown Guide - Basic Syntax](https://www.markdownguide.org/basic-syntax/)
- [Markdown Guide - Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)
- [Emoji Cheat Sheet](https://github.com/ikatyang/emoji-cheat-sheet)
- [GitHub docs footnotes in Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#footnotes)