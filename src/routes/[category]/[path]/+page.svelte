<script>
  import FormFactory from "$lib/components/form/FormFactory.svelte";
  import Categories from "$lib/components/Categories.svelte";
  import Sidebar from "$lib/components/Sidebar.svelte";

  export let data
  $: console.log("Data:", data)

  let categories = data.categories
  let category = categories.find(c => c.slug === data.category)
  $: console.log("Category", category)

  let path = category.paths.find(p => p.slug === data.path)
  $: console.log("Path", path)
</script>

<svelte:head>
    <title>{path.name.replaceAll("-", " ")} prompt for Toby AI - Voyager Social Prompt Customizer</title>
    <meta name="description" content="{path.description} using Toby AI">
</svelte:head>

<Sidebar categories="{data.categories}"/>
<section>
    <div class="flex flex-col items-center mr-12">
        <div class="w-full">
            <div class="flex flex-col items-center">
                <h1 class="text-3xl sm:text-5xl mb-2 font-bold">{path.name}</h1>
                <p class="text-xl mb-6 text-gray-400">{path.description}</p>
                <a class="btn btn-ghost btn-sm" href="https://app.voyagersocial.ai/tobypro" target="_blank">Try this Prompt With Toby AI</a>
                {#if path.long}
                    <p class="text-center">{@html path.long.replaceAll("\n", "<br/>")}</p>
                {/if}
            </div>
            <FormFactory pathData="{path}"/>
        </div>

        {#if category.paths.length > 1}
            <div class="divider mt-36">Other {data.category} prompts</div>
            <Categories data="{category.paths}" exclude="{data.path}" isPath="true"/>
        {/if}
    </div>
</section>
