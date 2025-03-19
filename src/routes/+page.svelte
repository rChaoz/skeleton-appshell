<script lang="ts">
    import AppShell from '$lib/AppShell';
    import LightSwitch from '$lib/LightSwitch.svelte';
</script>

<AppShell>
    <AppShell.Header class="text-primary-contrast-100-900 bg-primary-100-900/85 backdrop-blur-sm" hideOnScroll>
        <div class="container mx-auto flex px-8 py-4 justify-between font-semibold text-lg">
            <div class="space-y-1">
                <div><strong>AppShell</strong> • AppBar goes here</div>
                <div class="font-normal text-sm opacity-70">This is hidden automatically on mobile when scrolling</div>
            </div>
            <LightSwitch />
        </div>
    </AppShell.Header>

    <AppShell.Footer class="text-primary-contrast-900-100 bg-primary-900-100/85 p-1 text-sm text-center backdrop-blur-sm">
        <strong>Alert:</strong>
        This is the page footer. I made it tiny since it's sticky, it's not recommended to be used, but it exists to cover use-cases.
    </AppShell.Footer>

    <AppShell.Page class="space-y-4">
        <header class="bg-linear-to-b from-secondary-50-950/50 to-transparent">
            <div class="container mx-auto p-8 space-y-6">
                <h1 class="h1">Skeleton App Shell</h1>
                <p class="text-surface-700-300">This is the page header.</p>
            </div>
        </header>
        <main class="container mx-auto p-8 space-y-6">
            {#each { length: 10 }, i}
                <h2 id="heading-{i}" class="h2">Heading {i}</h2>
                <p>
                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ornare suscipit orci, vitae elementum sem ultrices in.
                    Nullam cursus, dolor vitae fringilla sollicitudin, lacus sem faucibus ante, in dapibus nunc mi in odio. Aenean auctor a
                    nisl id sodales. Fusce dapibus magna consectetur, pretium nulla a, imperdiet purus. Nam fringilla diam ut eros bibendum
                    varius. Duis id dolor arcu. Praesent vel pretium nisl, ut dapibus nisl. Mauris et varius leo, at suscipit nunc.
                </p>
            {/each}
        </main>
        <footer class="mt-8 preset-tonal text-center text-sm opacity-70">
            <div class="container mx-auto px-8 py-12 space-y-4">
                <p>This is the page footer.</p>
                <p>© 2077 Maybe some copyright reserved, maybe not.</p>
            </div>
        </footer>
    </AppShell.Page>
</AppShell>
