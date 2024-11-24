<script>
    export let value;
    import { createEventDispatcher } from 'svelte';
    
    const dispatch = createEventDispatcher();
    
    function handleInput(event) {
      dispatch('input', event.target.value);
    }
</script>
    
<style>
    textarea {
        width: 100%;
        height: 90vh;
        font-size: 1rem;
        padding: 1rem;
    }
</style>
    
<textarea
    bind:value
    on:input={handleInput}
    placeholder="Write your Markdown here..."
></textarea>