<script>
    import Hero from "$lib/components/index/Hero.svelte";
    import IntroBar from "$lib/components/index/IntroBar.svelte";
    import GeneralInformation from "$lib/components/index/GeneralInformation.svelte";
    import Questions from "$lib/components/Questions.svelte";
    import AdditionalInformation from "$lib/components/index/AdditionalInformation.svelte";

    // Stores
    import {filteredThreads} from "$lib/stores/filteredThreads.js";
    import {get} from "svelte/store";

    // Get data
    export let data;

    let threads = get(filteredThreads).length ? get(filteredThreads) : data.threads.threads;
    let members = data.members;
    let tags = data.tags.available_tags;

    filteredThreads.set(threads);
</script>

<Hero/>
<IntroBar/>

<section>
    <!-- General information -->
    <GeneralInformation
            introText="De plek waar jij al jouw code vragen kan: stellen, terugvinden en anderen
		kan helpen."
            {threads}
            {members}
    />

    <!-- Questions -->
    <Questions id="content" {threads} {members} {tags} title="Alle vragen"/>

    <!-- Additional Information (Filter) & Widget -->
    <AdditionalInformation {tags}/>
</section>

<style>
    @media (min-width: 60rem) {
        section {
            padding: 0 2rem;
            display: grid;
            grid-template-columns: 2.5fr 1fr;
            grid-template-rows: auto 1fr;
            grid-template-areas:
				"GeneralInfo Questions AdditionalInfo"
				"GeneralInfo Questions AdditionalInfo";
        }
    }

    @media (min-width: 75rem) {
        section {
            padding: 0 5rem;
            grid-template-columns: 0.6fr 1fr 0.6fr;
            grid-gap: 2rem;
        }
    }
</style>
