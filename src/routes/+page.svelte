<script lang="ts">
	import AppShell from "$lib/AppShell";
	import Main from "$lib/AppShell/Main.svelte";
</script>

<AppShell>
	<AppShell.Header class="preset-tonal-primary p-8 font-semibold" hideOnScroll>
		This is the app bar
	</AppShell.Header>
	<AppShell.Main class="container mx-auto p-8 space-y-6">
		<h1 class="h1">Skeleton App Shell</h1>
		<a class="anchor block text-sm mb-16" href="#heading-3">Go to heading 3</a>
		{#each { length: 10 }, i}
			<h2 id="heading-{i}" class="h2">Heading {i}</h2>
			<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed ornare suscipit orci, vitae elementum sem ultrices in. Nullam cursus, dolor vitae fringilla sollicitudin, lacus sem faucibus ante, in dapibus nunc mi in odio. Aenean auctor a nisl id sodales. Fusce dapibus magna consectetur, pretium nulla a, imperdiet purus. Nam fringilla diam ut eros bibendum varius. Duis id dolor arcu. Praesent vel pretium nisl, ut dapibus nisl. Mauris et varius leo, at suscipit nunc.</p>
		{/each}
	</AppShell.Main>
</AppShell>