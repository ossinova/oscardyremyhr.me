---
title: "What is Markdown, and why you should learn it. "
subtitle: Learn the power of the Markdown syntax
date: 2022-06-02T00:19:30.263Z
summary: Why you should utilize Markdown in your new project
draft: false
featured: false
image:
  filename: featured
  focal_point: Smart
  preview_only: false
---
{{< table_of_contents >}}

## What is Markdown?

Markdown has gained popularity because it's easy to use and it's widely accepted across platforms.

You can use markdown to write content that can be conveyed in plain text. A good example would be a blog post.

In this article, you'll learn what markdown is and how to use it.

What is Markdown?
Markdown is a markup language just like HTML. We use it to parse text and convert it into a specific format. You can also think of it as a text to HTML converter tool.

Many developers like writing in markdown because it gives them fine-grained control over their text and code. We'll see how and why in the coming paragraphs.

## Getting started

In this guide we'll cover the following topics.

* How to create your first markdown file.
* Discuss how markdown can be rendered in VS Code
* Tools that Support Markdown

Markdown works in any browser even if you use a simple notepad. But there are certain tools that can help enhance your productivity by providing a real time view (of markdown and rich text) side by side.

### Common .md writing tools

The following are some of the tools that support working with markdown:

* VSCode (We'll cover this in this article)
* Atom
* Haroopad
* Sublime text
* MarkPad

How to Work with Markdown
Download VSCode and enable the plugin
VSCode is a text editor like notepad, but it has many more capabilities. You can also use it for coding and it supports numerous programming languages.

#### Using VSCode

We'll be using VSCode to write and render markdown files.

You can download VSCode from here.

Once your download is completed, activate the below extension:

image-118
VS code extension
How to create your first markdown file
To work with markdown, simply save the text file with .md extension. After that, you'll be able to apply markdown syntax.

After creating your file and activating the plugin, the workspace should look something like this.

## Markdown in action (Syntax)

In markdown, we use a specific syntax to denote headings, bold text, lists, and other text formatting. Similar to that of HTML. 

Here are the basics in terms of the syntax:

### Headings

```
# Heading 1
## Heading 2
### Heading 3
```

Headings in Markdown are any line which is prefixed with a # symbol. The number of hashes indicates the level of the heading. One hash is converted to an h1, two hashes to an h2 and so on. There are a total of 6 levels which you can make use of - but for most writing, you’ll rarely ever need more than 3.

### Text

```
*italic*
**bold**
***bold-italic***
[link](https://example.com)
```

If you want to emphasise a word a *little* bit, wrap it in asterisks. For something that needs **more** emphasis: double asterisks. If you really want to ***drive*** the point home, use triple asterisks. If you prefer, you can also use underscores - they’re completely interchangeable.

To add a link: wrap the text which you want to be linked in square brackets, followed by the URL to be linked to in parenthesis. An easy way to remember this one is to think of it like turning a word into a button. \[button] and (place to go when the button is clicked) combine to form a [link](https://www.youtube.com/watch?v=dQw4w9WgXcQ).

### Images

```
![Programming meme](https://i.pinimg.com/originals/1f/af/97/1faf970bd2131343530726ca4ac6192e.jpg)
```

Markdown images have exactly the same formatting as a link, except they’re prefixed with a `!`. This time, the text in brackets is the alt text - or the descriptive text for the image.

![Programming meme](https://i.pinimg.com/originals/1f/af/97/1faf970bd2131343530726ca4ac6192e.jpg)

### Lists

Lists are a formatting nightmare in HTML, but Markdown lists are incredibly easy to manage. For a bullet list, just prefix each element with a `* - or - or +` and they will be converted to dots. You can also create nested lists; just indent a line with 4 spaces and it will be nested under the line above.

* Milk
* Bread
* Wholegrain
* Butter

For numbered lists, do exactly the same thing - but use numbers!

### Quotes

When you want to add a quote in Markdown, it’s exactly the same as the formatting which you may already be familiar with from your email app of choice when you reply to someone.

> Markdown is so cool!

Prefixing the line with a > converts it into a block-quote.

### Code Snippets & Blocks

Snippets

Some text with an inline ``` `code` ``` snippet

Some text with an inline `code` snippet

```
    .my-link {
        text-decoration: underline;
    }
```

If you’re a technical writer, you may want to use example snippets of code to teach your readers a particular syntax (like I’m doing, with this very blog post). Using a single back-tick around a word in a sentence, you can show a quick code snippet.

Indenting by 4 spaces will turn an entire paragraph into a code-block.

Blocks

````
```python
print("Hello World!")
```
````

You can add syntaxed code if your markdown application / renderer supports it (like Github) by using three  backticks followed by the language ```` ```python````  

```python
# Python printing
print("Hello World!")
```

This is especially useful for documenting code in the **readme.md** file. 

## Wrapping up

By now I hope you're confident enough to write your own markdown. Once you get the hang of it, it's easy enough. Apart from being simple, it is also very powerful and widely accepted.

If you found this post helpful, share it :)