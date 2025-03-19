<script lang="ts">
    import type { HTMLAttributes } from 'svelte/elements';
    import { getContext } from 'svelte';
    import type { AppShellContext } from '$lib/AppShell/context';

    interface Props extends HTMLAttributes<HTMLElement> {
        /**
         * If true, this element will stick to the side of the page, remaining fixed as the page is scrolled.
         * @default true
         */
        sticky?: boolean;
        /**
         * Sidebar position.
         */
        position: 'left' | 'right';
    }

    const { children, class: classes, sticky = false, position, ...rest }: Props = $props();

    // Contexts
    const context = getContext<AppShellContext>('appShell');
</script>

<div style:grid-area="sidebar-{position}">
    <aside {...rest} class={[sticky && 'sticky', classes]} style:top={context.headerHeight + 'px'}>
        {@render children?.()}
    </aside>
</div>
