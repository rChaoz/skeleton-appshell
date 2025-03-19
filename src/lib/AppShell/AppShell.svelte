<script lang="ts">
    import type { HTMLAttributes } from 'svelte/elements';
    import { onMount, setContext } from 'svelte';
    import { MediaQuery } from 'svelte/reactivity';

    interface Props extends HTMLAttributes<HTMLDivElement> {
        /**
         * Media query that controls when {@linkplain hideOnScroll} applies.
         * @default max-width: 600px
         */
        hideOnScrollQuery?: string;
    }

    const { children, class: classes, hideOnScrollQuery = 'max-width: 600px', ...rest }: Props = $props();

    // Header height context - set by Header and used by Sidebars to set top for sticky scrolling
    // SSR-friendly as if the page is not scrolled, the sidebars will still be placed correctly regardless of this
    const headerHeight = $state({ current: 0 });
    setContext('appShell-headerHeight', headerHeight);

    // Auto-hide logic
    let shouldHide = $state(false);
    const smallScreen = $derived(new MediaQuery(hideOnScrollQuery));
    const shouldHideHeaderFooter = $derived(shouldHide && smallScreen.current);
    setContext('appShell-shouldHideHeaderFooter', {
        get() {
            return shouldHideHeaderFooter;
        }
    });

    let lastScrollTop = 0;

    function onRootScroll() {
        const scrollTop = document.documentElement.scrollTop;
        const header = document.getElementById('appShell-header');
        // Can't hide the header if document is not scrolled enough to have content in place of the header
        if (header && scrollTop < header.offsetHeight) {
            shouldHide = false;
            lastScrollTop = scrollTop;
            return;
        }

        // Show/hide header after 50px of scrolling in respective direction
        const delta = scrollTop - lastScrollTop;
        if (!shouldHide && delta > 0) {
            if (delta > 100) shouldHide = true;
            else return;
        } else if (shouldHide && delta < 0) {
            if (delta < -100) shouldHide = false;
            else return;
        }
        lastScrollTop = scrollTop;
    }

    onMount(() => {
        document.addEventListener('scroll', onRootScroll, { passive: true });
        return () => document.removeEventListener('scroll', onRootScroll);
    });
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
