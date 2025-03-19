<script lang="ts">
    import { getContext, onMount } from 'svelte';
    import type { HTMLAttributes } from 'svelte/elements';

    interface Props extends HTMLAttributes<HTMLElement> {
        /**
         * If non-null, the `scroll-padding-top` CSS property of the root (`<html>` element will be set to this value,
         * with `{height}` replaced with the height of the header, in pixels.
         * @default calc({height}px + 1rem)
         */
        scrollPadding?: string | null;
        /**
         * If true, this element will stick to the top of the page, remaining fixed as the page is scrolled.
         * @default true
         */
        sticky?: boolean;
        /**
         * Hide this header on mobile (narrow screens, as set by {@linkcode hideOnScrollQuery} on the parent `AppShell`)
         * when scrolling down, and show it when scrolling up.
         *
         * Usually used when the header is an AppBar. Only applies when `sticky` is true.
         * @default false
         */
        hideOnScroll?: boolean;
    }

    const {
        children,
        class: classes,
        scrollPadding = 'calc({height}px + 1rem)',
        sticky = true,
        hideOnScroll = false,
        ...rest
    }: Props = $props();

    // Contexts
    const headerHeight = getContext<{ current: number }>('appShell-headerHeight');
    const shouldHide = getContext<{ current: boolean }>('appShell-shouldHideHeaderFooter');

    // Scroll padding logic
    $effect(() => {
        if (sticky && scrollPadding != null)
            document.documentElement.style.scrollPaddingTop = scrollPadding.replace('{height}', String(headerHeight.current));
        else document.documentElement.style.scrollPaddingTop = '';
    });

    // Remove contexts/styles set by this component on unmount
    // So, for example, header is in an {#if} block, the scroll padding is correctly removed when the header is removed
    // Use onMount return instead of onDestroy as onDestroy runs during SSR
    onMount(() => () => {
        headerHeight.current = 0;
        document.documentElement.style.scrollPaddingTop = '';
    });
</script>

<header
    id="appShell-header"
    bind:offsetHeight={headerHeight.current}
    {...rest}
    class={[
        sticky && 'sticky top-0',
        sticky && hideOnScroll && 'transition-[translate] duration-300',
        sticky && hideOnScroll && shouldHide.current && '-translate-y-full',
        classes
    ]}
>
    {@render children?.()}
</header>

<style>
    #appShell-header {
        grid-area: header;
    }
</style>
