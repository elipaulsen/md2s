# Md2s

## Overview

**Md2s (Markdown to Svelte)** is a lightweight library that simplifies rendering Markdown files as Svelte components. With a single component, you can supply a `.md` file, and Md2s will handle converting and displaying the content seamlessly in your Svelte applications. Additionally, Md2s supports **placeholders** within your Markdown files, allowing you to use your Markdown files as templates to  update your component with real-time data.

Md2s syntax highlights code blocks, and component styling is consistent with github Markdown styling.

## Installation

Install Md2s via npm:

```bash
npm install md2s
```

## Usage

Import the Md component from md2s

Supply the component the path of the source Markdown file

*example +page.svelte:*
```html
<script lang="ts">
    import Md from "$lib/md2s.svelte";
</script>

<h1>here is the markdown component:</h1>
<Md filename="test.md"></Md>
```

*original Markdown file:*
```md
# Hello World
### How is it going?

| Month    | Savings |
| -------- | ------- |
| January  | $250    |
| February | $80     |
| March    | $420    |

![image info](barry-bonds.jpg "bonds")
```

*view of browser with rendered component:*
![alt text](image.png)

### Placeholders

If you have stuff in your Markdown file that is dynamic you can use `{%}` as a placeholder and pass in an array of strings into the variables prop of the component to update or render dynamic pages.

*example +page.svelte:*
```html
<script lang="ts">
    import Md from "$lib/md2s.svelte";

    const vars: string[] = ["Eli", "penguin", "211.45"];
</script>

<h1>here is the markdown component:</h1>
<Md filename="test.md" variables={vars}></Md>
```

*original Markdown file:*
```md
# Hello {%}
### Your favorite animal is: {%}
### You have ${%} in your bank account
```

*view of browser with rendered component:*
![alt text](image-1.png)


## Creating a svelte project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in my-app
npx sv create my-app
cd my-app
```

## Developing
install dependencies and start a development server.

```bash
npm install
npm run dev
```