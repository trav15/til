# Tailwind

## Arbitrary Values

For specific values of `px` or `rem` that are not built in, use square brakcet notion `[]` to define an arbitrary value for a one-off size for anything using the spacing system:

```html
<div class="mt-4 w-[13.5rem]"></div>
``` 

Or specify hex or RBG codes for one-off colors:
```html
<div class="text-[#1012f1] bg-[rbg(123,1,1)"></div>
``` 
https://tailwindcss.com/docs/adding-custom-styles#using-arbitrary-values

# Additional CSS tips

## Avoid use of px when setting font-size

Use `em` or `rem` as it will be in line with relative sizes for the browser. On the web, the deafult font size is `16px`. Some users change this default which can result in overriding the users' preferences. That may make it hard or impossible for them to use your website and harm your design with unintended visual side effects.[^px]

### The difference between `em` and `rem`

`1rem` is always equal to the browser's font size (font size of the `html` element). `rem` stands for "root em", and the rooy webpave is the `<html>` tag. 

`em` is the font size of the _current element_

[^px]: [Why you should never use px to set font-size in CSS by Josh Collingsworth](https://joshcollinsworth.com/blog/never-use-px-for-font-size)

## *Resources*

- [Add fonts to Tailwind](https://dev.to/thomasvanholder/add-a-custom-tailwind-css-fonts-to-your-website-1nn6)
- [Add Tailwind to Gatsby](https://tailwindcss.com/docs/guides/gatsby)
- [Add Tailwind to Next.js](https://tailwindcss.com/docs/guides/nextjs)