<script>
    import { onMount } from "svelte";
    import { base } from "$app/paths";

    import ZooBanner from "$lib/Zoo.svelte";
</script>
<style>
    h1.heading {
        font-size: 100px;
        padding: 0;
        margin: 0;
        padding-left: 10px;
        padding-right: 10px;

        background: linear-gradient(90deg, #7d4a4f, #ed3107);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text; /* for Firefox */
    }
    #title span {
        font-size: 150px;
        animation: anim 2s infinite ease-in-out;
        display: inline-block;

        background: linear-gradient(90deg, #b0894f, #beaf06);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text; /* for Firefox */

        user-select: none;
        -webkit-user-select: none;

        cursor: pointer;

    }


    #title span:hover{
        opacity: 70%;
    }


        @keyframes anim {
        0% {
            transform: translateY(0) rotate(0deg);
        }
        50% {
            transform: translateY(-5px) rotate(1.5deg);
        }
        100% {
            transform: translateY(0);
        }
        }

        #title span:nth-child(1) { animation-delay: 0s; }
        #title span:nth-child(2) { animation-delay: 0.2s; }
        #title span:nth-child(3) { animation-delay: 0.4s; }
        #title span:nth-child(4) { animation-delay: 0.6s; }
        #title span:nth-child(5) { animation-delay: 0.8s; }
        #title span:nth-child(6) { animation-delay: 1s; }
        #title span:nth-child(7) { animation-delay: 1.2s; }
        #title span:nth-child(8) { animation-delay: 1.4s; }
        #title span:nth-child(9) { animation-delay: 1.6s; }
        #title span:nth-child(10) { animation-delay: 1.8s; }
        
    .content {
        font-size: 20px;
        padding: 10px;
        padding-left: 30px;
        padding-right: 30px;
        text-align: center;
        color: #e0a7a7;
        line-height: 1.6;

        h1 {
            margin-top: -20px;
            margin-bottom: -20px;
        }

        h2 span {
            color: rgb(231, 57, 57);
        }
        h1 span {
            color: white;
            background-color: rgb(231, 57, 57);
            padding: 10px;
            border-radius: 20px;
        }

        h3 span {
            color: white;
            background-color: rgb(231, 57, 57);
            padding: 10px;
            border-radius: 20px;
            font-size: 30px;
        }
    }

    @media (max-width: 950px) {
        h1 {
            font-size: 60px;
        }
        #title span {
            font-size: 80px;
        }
    }
    @media (max-width: 600px) {
        h1 {
            font-size: 30px;
        }
        #title span {
            font-size: 40px;
        }
        .content h3 span {
            font-size: 15px;
        }
    }

    a {
        text-decoration: none;
        color: white;
    }
    .arrow {
        vertical-align: -0.27em;
    }
</style>

<ZooBanner />
<a href="{ base }">Return Home <span class="material-symbols-outlined arrow">arrow_circle_right</span></a>
<br><br><br>
<h2>TODAY</h2>
<h1 class="heading">RED PANDAS</h1>
<h2>ARE CONSIDERED</h2>
<h1 id="title" class="heading"><span>E</span><span>N</span><span>D</span><span>A</span><span>N</span><span>G</span><span>E</span><span>R</span><span>E</span><span>D</span>
</h1>
<br><br>
<div class="content">
    <h2>Red pandas are endangered and are legally protected in India, Bhutan, China, Nepal and Myanmar. Their primary threats are <span>habitat loss and degradation</span>, <span>human interference</span> and <span>poaching</span>.</h2>
    <h2>Researchers believe that the total population of red pandas has declined by</h2>
    <h1><span>40%</span></h1>
    <h2>in just the last 2 decades.</h2>
    <h2><span>Habitat loss</span> is primarily attributed to logging, grazing livestock, demand for firewood, human encroachment and farming. The decrease in suitable habitat for red pandas has coincided with the increase in human populations throughout Asia</h2>
    <h2>Red pandas are present in some protected areas throughout their range, including parks in Myanmar, Bhutan, India, Nepal and China. Despite regulations, <span>livestock grazing, hunting and logging still occur</span> throughout many of these protected areas.</h2>
</div>
<br>
<h1 class="heading">YOU CAN HELP!</h1>
<br><br>
<div class="content">
    <h3><span>Reduce, reuse and recycle</span></h3>
    <h2>Cut back on single-use goods, and find creative ways to reuse products at the end of their life cycle. Choose recycling over trash when possible.</h2>
    <br>
    <h3><span>Practice ecotourism</span></h3>
    <h2>During your travels, support, visit or volunteer with organizations that protect wildlife. Shop smart too! Avoid buying products made from animals, which could support poaching and the illegal wildlife trade.</h2>
    <br>
    <h3><span>Support organizations</span></h3>
    <h2>Organizations like the Smithsonian’s National Zoo, WCS and Conservation Biology Institute that research better ways to protect and care for Red Pandas and other endangered species.</h2>
</div>
<h1 class="heading" style="padding: 20px;">The future of red pandas depends on readers like you.</h1>
<br>