<svelte:head>
    <title>Voyager Social's Prompt Customizer 🛠️</title>
    <meta name="description" content="VS Prompt Customizer is a free library and builder for ChatGPT prompts.">
</svelte:head>

<script>
  import Categories from "$lib/components/Categories.svelte";
  import FAQ from "$lib/components/FAQ.svelte";
  import AllPrompts from "$lib/components/AllPrompts.svelte";

  export let data;
  let categories = data.categories;

  let totalPaths = 0;
  categories.forEach(category => {
    if (category.hidden) return;
    totalPaths += category.paths.length;
  });
</script>

<div>
    <div class="flex flex-col items-center">
        <h1 class="text-3xl sm:text-5xl font-bold pt-14">🛠️ Voyager Social's Prompt Customizer</h1>
        <p class="text-xl">No need to study prompt engineering</p>
        <br/>
        <br/>
        <p class="text-lg text-center">
            The VS Prompt Customizer is a free library and builder for customized AI prompts.
            <br/>
            There are currently <span class="font-bold">{totalPaths}</span> total prompt templates available.
        </p>
    </div>
    <h2 class="pt-8">Categories</h2>
    <Categories data={categories}/>
    <div class="mt-16">
        <FAQ/>
    </div>
    <!-- <div class="mt-16">
        <AllPrompts data={categories}/>
    </div> -->
</div>
