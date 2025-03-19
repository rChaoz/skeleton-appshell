<script lang="ts">
    import { Switch } from "@skeletonlabs/skeleton-svelte"

    let checked = $state(true)

    function onCheckedChange(change: { checked: boolean }) {
        checked = change.checked
        if (checked) document.documentElement.classList.remove("dark")
        else document.documentElement.classList.add("dark")
    }
</script>

<Switch {checked} {onCheckedChange}/>