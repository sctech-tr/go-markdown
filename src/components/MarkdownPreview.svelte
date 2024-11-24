<script>
    export let markdown = ''; // Rendered HTML from the parent
</script>
    
<div class="preview">
    {@html markdown}
</div>
    
<style>
    .preview {
        width: 100%;
        height: 90vh;
        overflow: auto;
        padding: 1rem;
        border-left: 1px solid #ccc;
    }
</style>