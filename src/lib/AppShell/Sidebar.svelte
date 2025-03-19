<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

    interface Props extends HTMLAttributes<HTMLElement> {
        /**
         * If true, this element will stick to the side of the page, remaining fixed as the page is scrolled.
         * @default true
         */
         sticky?: boolean
    }

    const { children, class: classes, sticky = false, ...rest }: Props = $props()
</script>

<aside {...rest} class={[sticky && "sticky top-0 h-full", classes]}>
    {@render children?.()}
</aside>
