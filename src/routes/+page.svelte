<script lang="ts">
    import Md from "$lib/md2s.svelte";

    const vars: string[] = ["Eli", "penguin", "211.45"];
</script>

<h1>Hello here is the markdown content in html:</h1>
<Md src="test.md" variables={vars}></Md>