<script>
    import { onMount } from "svelte";
    import { base } from "$app/paths";
    import ZooBanner from "$lib/Zoo.svelte";

    let face = $state("sleeping");
    let period = $state("");
    let hunger = $state(Math.random()*5 + 1);
    let anger = $state(0);
    let splash = $state("");
    let loaded = $state(false);

    $effect(function() {
        if (splash != "") {
            loaded = true;
        }
    })

    let time  = new Date();
    let hour = time.getHours();
    //let hour = 6;

    if (hour >= 3 && hour <= 9) {
        face = "happy";
        period = "awake";
    }
    else if (hour >= 17 && hour <= 19) {
        face = "happy";
        period = "awake";
    }
    else {
        face = "sleeping";
        period = "sleeping";
    }

    $effect(function() {
        if (period === "sleeping") {
            splash = "Kitsu is sleeping, we shouldn't disturb her.";
        }
        else if (period === "awake") {
            if (hunger > 6.5) {
                splash = "Kitsu is happy, maybe pet her?";
            }
            else {
                splash = "Kitsu is hungry, maybe feed her?";
            }
        }
    })

    function pet() {
        if (period === "sleeping") {
            anger++;
        }
        else if (period === "awake") {
            if (face === "happy") {
                face = "playful";
                setTimeout(function() {face = "happy";}, 3500);
            }
        }
    }
    function eat() {
        if (period === "awake") { // should be but just to be safe + debug catch
            if (face === "happy") {
                face = "eating";
                hunger++;
                console.log(hunger);
                if (hunger > 6.5) {
                    splash = "Kitsu is full!";
                } 
                else {
                    splash = "Kitsu is still hungry.";
                }
                setTimeout(function() {face = "playful";}, 3500);
                setTimeout(function() { face = "happy";}, 4500);
            }
        }
    }
    $effect(function() {
        if (anger == 1) {
            face = "annoyed";
            splash = "Kitsu is annoyed, maybe leave her alone?";
            setTimeout(function() {if (anger == 1) {face = "sleeping";}}, 3500);
        }
        if (anger == 2) {
            face = "annoyed";
            splash = "Kitsu is very annoyed, leave her alone.";
            setTimeout(function() {if (anger == 2) {face = "sleeping";}}, 3500);
        }
        if (anger == 3) {
            face = "angry";
            splash = "Kitsu is angry now. Beware her attack!";
            setTimeout(function() {window.location.href = "https://www.youtube.com/watch?v=q-Y0bnx6Ndw&list=RDq-Y0bnx6Ndw&start_radio=1"}, 4500);
        }
    })
</script>

<style>

    a {
        text-decoration: none;
        color: white;
    }
    .arrow {
        vertical-align: -0.27em;
    }
    #cage {
        position: relative;
        width: 30%;
        aspect-ratio: 1/1;
        margin: 0 auto;
        background-color: rgb(222, 125, 103);
        border-radius: 20px;
    }
    @media (max-width: 950px) {
        #cage {
            width: 50%;
        }
    }
     @media (max-width: 650px) {
        #cage {
            width: 70%;
        }
    }
    #cage img {
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;

        -webkit-user-drag: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;

        cursor: grab;
    }
    #cage img#-tail {
        transform: rotate(-5deg);
        transform-origin: 50% 85%;
        animation: tail-wag 3s infinite;
    }
    #cage img#-face {
        transform-origin: 60% 60%;
        transition: transform 0.3s ease-in-out;
    }
    #cage img#-face:hover {
        transform: rotate(3deg);
    }
    @keyframes tail-wag {
        0% { transform: rotate(-5deg); }
        50% { transform: rotate(5deg); }
        100% { transform: rotate(-5deg); }
    }

    #splash {
        opacity: 0;
        transform: translateY(-15px);    
    }
    @media (max-width: 700px) {
        #splash {
            font-size: 20px;
        }
    }
    #splash.loaded {
        transition: opacity 0.3s ease-in-out, transform 1s ease-in-out;
        opacity: 1;
        transform: translateY(0px);
    }
    #splash span {
        background-color: rgb(154, 61, 7);
        padding: 10px;
        border-radius: 10px;
        margin: 5px;
    }

    #feed {
        display: none;
        opacity: 0;
        height: 0;
        width: 0;
        margin: 0 auto;
        padding: 10px;
        background-color: rgb(87, 126, 36);
        color: white;
        border-radius: 10px;
    }
    #feed.loaded {
        display: block;
        opacity: 1;
        height: 50px;
        width: 55%;
    }
    #feed button {
        font-size: 25px;
        padding: 5px;
        border-radius: 10px;
        background-color: rgb(50, 84, 6);
        font-family: Phantom Sans, 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }
    #feed button:hover {
        background-color: rgb(30, 52, 2);
        cursor: pointer;
    }
    #feed button span {
        vertical-align: -0.2em;
        font-size: 30px;
    }
</style>

<ZooBanner />
<br>
<a href="{ base }">Return Home <span class="material-symbols-outlined arrow">arrow_circle_right</span></a>
<br><br>
<h2 id="splash" class:loaded={loaded}><span>{ splash }</span></h2>
<div id = "feed" class:loaded={ hunger < 6.5 && loaded && period === "awake" }>
    <button onclick = { eat }>Feed Bamboo Leaves<span class="material-symbols-outlined displayed">psychiatry</span></button>
</div>
<h4>(Tap/Click to Pet)</h4>
<div id="cage">
    <img src="kitsu/tail.png" alt = "kitsu's tail" id="-tail"/>
    <img src="kitsu/body.png" alt = "kitsu's torso" id="-torso"/>
    <a href="/kitsu" onclick={function() {event.preventDefault(); pet();}}><img src="kitsu/{face}.png" alt = "kitsu's face" id="-face"/></a>
</div>