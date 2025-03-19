<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

    interface Props extends HTMLAttributes<HTMLElement> {
    }

    const { children, class: classes, ...rest }: Props = $props()
</script>

<footer {...rest} class={[classes]}>
    {@render children?.()}
</footer>
