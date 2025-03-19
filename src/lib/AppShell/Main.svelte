<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";

    interface Props extends HTMLAttributes<HTMLElement> {}

    const { children, class: classes, ...rest }: Props = $props()
</script>

<main {...rest} class={[classes]}>
    {@render children?.()}
</main>
