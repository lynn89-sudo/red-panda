@prerender

<script>
    import { onMount } from "svelte";
    import { base } from "$app/paths";

    import ZooBanner from "$lib/Zoo.svelte";
    let loaded = $state(false);

    let facts = $state([
        {
            "title": "Loading...",
            "description": "",
            "icon": "",
            "id": 0
        }
    ]);
    let currentFact = $state(1);
    let totalFacts = $state(0);

    let fact_desc = $derived(facts[currentFact-1].description);
    let fact_title = $derived(facts[currentFact-1].title);
    let fact_icon = $derived(facts[currentFact-1].icon);

    let viewedFacts = $state([1]);
    function addViewed(fact) {
        if (viewedFacts.includes(fact)) {
            return;
        }
        else {
            viewedFacts.push(fact);
        }
    }
    let unlocked = $derived(viewedFacts.length >= 5);
    $effect(function() {
        if (unlocked) {
            setTimeout(function() {
                const meetSection = document.getElementById("meet");
                if (meetSection) {
                    meetSection.scrollIntoView({ behavior: "smooth" });
                }
            }, 2800)
        }
    });


    onMount (function() {
        fetch(`${ base }/facts.json`)
        .then(response => response.json())
        .then(data => {
            facts = data;
            loaded = true;
            totalFacts = facts.length;
        });
    })

    function minus() {
        currentFact--;
        if (currentFact < 1) {
            currentFact = totalFacts;
        }
        addViewed(currentFact); 
    }
    function plus() {
        currentFact++;
        if (currentFact > totalFacts) {
            currentFact = 1;
        }
        addViewed(currentFact); 
    }
</script>

<ZooBanner />
<h1 id="title"><span>K</span><span>I</span><span>T</span><span>S</span><span>U</span></h1>
<h2>The Red Panda!</h2>

<br><br>
<div id="endangered">
    <h1>Today, Red Pandas are considered Endangered</h1>
    <h3>Learn more</h3>
    <a href="{ base }/endangered"><button><span class="material-symbols-outlined arrow">arrow_circle_right</span></button></a>
</div>
<br>
<h3 class:invisible={loaded}>Content is loading...</h3>
<div id="fact" class:loaded={loaded}>
    <br>
    <h1><span class="material-symbols-outlined displayed">{fact_icon}</span></h1>
    <h1>{fact_title}</h1>
    <h3>{fact_desc}</h3>
    <h4><span>{currentFact}/{totalFacts}</span></h4>
    <br>
    <h3><button onclick={minus}><span class="material-symbols-outlined arrow">arrow_circle_left</span></button>    <button onclick={plus}><span class="material-symbols-outlined arrow">arrow_circle_right</span></button></h3>
    <h4 class:invisible={unlocked}><em>Read through these to unlock</em></h4>
</div>
<br>
<div id="meet" class:loaded={unlocked}>
    <h1>Meet Kitsu</h1>
    <a href="{ base }/kitsu"><button><span class="material-symbols-outlined arrow">arrow_circle_right</span></button></a>
</div>

<br><br>