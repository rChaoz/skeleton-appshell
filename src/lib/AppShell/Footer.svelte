<script lang="ts">
    import { onMount } from 'svelte';
    import type { HTMLAttributes } from 'svelte/elements';
    import { MediaQuery } from 'svelte/reactivity';

    interface Props extends HTMLAttributes<HTMLElement> {
        /**
         * If true, this element will stick to the top of the page, remaining fixed as the page is scrolled.
         * @default true
         */
        sticky?: boolean;
    }

    const { children, class: classes, sticky = true, ...rest }: Props = $props();
</script>

<footer id="appShell-footer" {...rest} class={[sticky && 'sticky bottom-0', classes]}>
    {@render children?.()}
</footer>

<style>
    #appShell-footer {
        grid-area: footer;
    }
</style>
