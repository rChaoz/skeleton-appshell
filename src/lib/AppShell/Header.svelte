<script lang="ts">
	import { onMount } from "svelte";
	import type { HTMLAttributes } from "svelte/elements";
    import { MediaQuery } from 'svelte/reactivity';

    interface Props extends HTMLAttributes<HTMLElement> {
        /**
         * If non-null, the `scroll-padding-top` CSS property of the root (`<html>` element will be set to this value,
         * with `{headerHeight}` replaced with the height of the header, in pixels.
         * @default calc({headerHeight}px + 1rem)
         */
        scrollPadding?: string | null
        /**
         * If true, this element will stick to the top of the page, remaining fixed as the page is scrolled.
         * @default true
         */
        sticky?: boolean
        /**
         * Hide this header on mobile (narrow screens, as set by {@linkcode hideOnScrollQuery}) when scrolling down, and show it when scrolling up.
         * Usually used when the header is an AppBar. Only applies when `stickyHeader` is true.
         * @default false
         */
        hideOnScroll?: boolean
        /**
         * Media query that controls when {@linkplain hideOnScroll} applies.
         * @default max-width: 800px
         */
        hideOnScrollQuery?: string
    }

    const { children, class: classes, scrollPadding = "calc({headerHeight}px + 1rem)", sticky = true, hideOnScroll = false, hideOnScrollQuery = "max-width: 600px", ...rest }: Props = $props()

    // Scroll padding logic
    $effect(() => {
        if (sticky && element && scrollPadding != null)
            document.documentElement.style.scrollPaddingTop = scrollPadding.replace("{headerHeight}", String(headerHeight))
        else document.documentElement.style.scrollPaddingTop = ""
    })

    // Auto-hide logic
    const smallScreen = $derived(new MediaQuery(hideOnScrollQuery))
    let element = $state<HTMLElement>()
    let shouldHide = $state(false)
    let headerHeight = $state(0)
    let lastScrollTop = 0

    function onRootScroll() {
        const scrollTop = document.documentElement.scrollTop
        // Can't hide the header if document is not scrolled enough to have content in place of the header
        if (element && scrollTop < element.offsetHeight) {
            shouldHide = false
            lastScrollTop = scrollTop
            return
        }

        // Show/hide header after 50px of scrolling in respective direction
        const delta = scrollTop - lastScrollTop
        if (!shouldHide && delta > 0) {
            if (delta > 100) shouldHide = true
            else return
        } else if (shouldHide && delta < 0) {
            if (delta < -100) shouldHide = false
            else return
        }
        lastScrollTop = scrollTop
    }

    onMount(() => {
        document.addEventListener("scroll", onRootScroll, { passive: true })
        return () => document.removeEventListener("scroll", onRootScroll)
    })
</script>

<header
    bind:this={element}
    bind:offsetHeight={headerHeight}
    {...rest}
    class={[
        sticky && "sticky top-0",
        sticky && hideOnScroll && "transition-[translate] duration-300",
        sticky && hideOnScroll && shouldHide && smallScreen.current && "-translate-y-full ",
        classes
    ]}>
    {@render children?.()}
</header>