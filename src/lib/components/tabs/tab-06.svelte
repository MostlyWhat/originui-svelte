<script lang="ts">
	import { Tabs, TabsContent, TabsList, TabsTrigger } from '$lib/components/ui/tabs';
</script>

<Tabs value="tab-1" class="items-center">
	<TabsList
		class="h-auto -space-x-px bg-background p-0 shadow-sm shadow-black/5 rtl:space-x-reverse"
	>
		<TabsTrigger
			value="tab-1"
			class="relative overflow-hidden rounded-none border border-border py-2 after:pointer-events-none after:absolute after:inset-x-0 after:bottom-0 after:h-0.5 first:rounded-s last:rounded-e data-[state=active]:bg-muted data-[state=active]:after:bg-primary"
		>
			Tab 1
		</TabsTrigger>
		<TabsTrigger
			value="tab-2"
			class="relative overflow-hidden rounded-none border border-border py-2 after:pointer-events-none after:absolute after:inset-x-0 after:bottom-0 after:h-0.5 first:rounded-s last:rounded-e data-[state=active]:bg-muted data-[state=active]:after:bg-primary"
		>
			Tab 2
		</TabsTrigger>
		<TabsTrigger
			value="tab-3"
			class="relative overflow-hidden rounded-none border border-border py-2 after:pointer-events-none after:absolute after:inset-x-0 after:bottom-0 after:h-0.5 first:rounded-s last:rounded-e data-[state=active]:bg-muted data-[state=active]:after:bg-primary"
		>
			Tab 3
		</TabsTrigger>
	</TabsList>
	<TabsContent value="tab-1">
		<p class="p-4 text-center text-xs text-muted-foreground">Content for Tab 1</p>
	</TabsContent>
	<TabsContent value="tab-2">
		<p class="p-4 text-center text-xs text-muted-foreground">Content for Tab 2</p>
	</TabsContent>
	<TabsContent value="tab-3">
		<p class="p-4 text-center text-xs text-muted-foreground">Content for Tab 3</p>
	</TabsContent>
</Tabs>
