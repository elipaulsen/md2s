<script lang="ts">
    import { onMount } from 'svelte';
    import { marked } from 'marked';
    import Prism from "prismjs";
    import "prismjs/themes/prism.css";
    export let src: string = '';
    export let variables: string[] = [];

    let content: string = '';

    function insertVariables(htmlString: string, replacements: string[]): string {
        let replacementIndex = 0;
        return htmlString.replace(/{%}/g, () => {
            return replacementIndex < replacements.length 
                ? replacements[replacementIndex++] 
                : "";
        });
    }

    onMount(async () => {
        if (src) {
            try {
                const file = await fetch(src);
                if (!file.ok) {
                    console.error("Markdown file not found");
                    content = `<p>Markdown file not found: ${src}</p>`;
                    return;
                }
                const markdown: string = await file.text();
                content = insertVariables(await marked(markdown), variables);
                await 0;
                Prism.highlightAll()
            } catch (error) {
                console.error(error);
                content = `<p>Error loading markdown file: ${src}</p>`;
            }
        }
        return () => {
            console.log('Unmounted!');
        };
    });
</script>

<div class="markdown-body">
    {@html content}
</div>

<style>
    @import 'markdown.css';
</style>
