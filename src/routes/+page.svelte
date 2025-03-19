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

    <AppShell.Sidebar class="p-8 space-y-10 max-lg:hidden" position="left">
        <div class="font-bold text-lg">Non-sticky sidebar</div>
        <div class="flex flex-col items-center gap-0.5">
            {#each { length: 10 }, i}
                <div class="preset-tonal hover:preset-tonal-primary size-32 grid place-items-center">(icon)</div>
            {/each}
        </div>
    </AppShell.Sidebar>

    <AppShell.Sidebar class="py-8 px-16 space-y-3 max-md:hidden" position="right" sticky="header">
        <div class="font-bold">On this page</div>
        <ul class="space-y-2">
            {#each { length: 10 }, i}
                <li><a href="#heading-{i}" class="anchor">Go to heading {i}</a></li>
            {/each}
        </ul>
    </AppShell.Sidebar>

    <AppShell.Page class="space-y-4">
        <header class="preset-tonal">
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
        <footer class="mt-8 bg-surface-950-50/5 text-surface-contrast-50-950/60 text-center text-sm">
            <div class="container mx-auto px-8 py-12 space-y-4">
                <p>This is the page footer.</p>
                <p>© 2077 Maybe some copyright reserved, maybe not.</p>
            </div>
        </footer>
    </AppShell.Page>
</AppShell>
