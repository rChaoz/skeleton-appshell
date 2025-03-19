<script lang="ts">
    import type { HTMLAttributes } from 'svelte/elements';
    import { setContext } from 'svelte';

    interface Props extends HTMLAttributes<HTMLDivElement> {}

    const { children, class: classes, ...rest }: Props = $props();

    // Contexts
    const headerHeight = $state({ current: 0 });
    setContext('appShell-headerHeight', headerHeight);
</script>

<div id="appShell" {...rest} class={[classes]}>
    {@render children?.()}
</div>

<style>
    :global(body, html) {
        min-height: 100%;
    }

    #appShell {
        display: grid;
        grid-template-areas: 'header header header' 'sidebar-left page sidebar-right' 'footer footer footer';
        grid-template-columns: auto 1fr auto;
    }
</style>
