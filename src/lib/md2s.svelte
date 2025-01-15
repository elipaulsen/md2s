<script lang="ts">
    import { onMount } from 'svelte';
    import { marked } from 'marked';
    export let filename: string = '';

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
        if (filename) {
            try {
                const file = await fetch(filename);
                if (!file.ok) {
                    console.error("Markdown file not found");
                    content = `<p>Markdown file not found: ${filename}</p>`;
                    return;
                }
                const markdown: string = await file.text();
                content = insertVariables(marked(markdown), ['md2s', 'world']);
            } catch (error) {
                console.error(error);
                content = `<p>Error loading markdown file: ${filename}</p>`;
            }
        }
    });
</script>

<div class="markdown-body">
    {@html content}
</div>

<style scoped>
    @import 'markdown.css';
</style>
