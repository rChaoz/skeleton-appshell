<script lang="ts">
    import AppShell from '$lib/AppShell';
    import LightSwitch from '$lib/LightSwitch.svelte';
</script>

<AppShell>
    <AppShell.Header class="preset-tonal-primary font-semibold" hideOnScroll>
        <div class="container mx-auto flex p-8 justify-between">
            <span>This is the app bar</span>
            <LightSwitch />
        </div>
    </AppShell.Header>

    <AppShell.Page class="space-y-4">
        <header class="bg-linear-to-b from-secondary-50-950/50 to-transparent">
            <div class="container mx-auto p-8 space-y-4">
                <h1 class="h1">Skeleton App Shell</h1>
                <a class="anchor block text-sm" href="#heading-3">Go to heading 3</a>
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
        <footer class="mt-8 preset-tonal text-sm opacity-70">
            <div class="container mx-auto px-8 py-12 space-y-4">
                <p>This is a footer.</p>
                <p>© 2077 Maybe some copyright reserved, maybe not.</p>
            </div>
        </footer>
    </AppShell.Page>
</AppShell>
