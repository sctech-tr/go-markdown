<script>
    import { marked } from 'marked';
    import hljs from 'highlight.js';
    import 'highlight.js/styles/github.css';
    import MarkdownInput from './components/MarkdownInput.svelte';
    import MarkdownPreview from './components/MarkdownPreview.svelte';
    
    let markdownText = '# Hello, Markdown!';
    let renderedMarkdown = marked(markdownText);
    
    marked.setOptions({
        highlight: function(code, lang) {
            if (hljs.getLanguage(lang)) {
                return hljs.highlight(code, { language: lang }).value;
            }
            return hljs.highlightAuto(code).value; // Fallback for unknown languages
        }
    });
    
    function handleInput(newText) {
        markdownText = newText;
        renderedMarkdown = marked(markdownText);
    }
    
    function saveFile(content) {
        const blob = new Blob([content], { type: 'text/markdown' });
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;
        link.download = 'document.md';
        link.click();
        URL.revokeObjectURL(url);
    }

    async function loadFile(event) {
        const file = event.target.files[0];
        const content = await file.text();
        markdownText = content; // Update the bound variable
        handleInput(content); // Update the rendered markdown
    }

    console.log(hljs.listLanguages()); // debug
</script>
    
<style>
    .container {
        display: flex;
        gap: 1rem;
    }
</style>
    
<div class="container">
    <MarkdownInput bind:value={markdownText} on:input={(event) => handleInput(event.detail)} />
    <MarkdownPreview markdown={renderedMarkdown} />
</div>

<button on:click={() => saveFile(markdownText)}>Save</button>

<input type="file" accept=".md" on:change={loadFile} />