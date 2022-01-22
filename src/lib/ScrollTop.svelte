<script lang=ts>
    export let hidden:boolean = true;
</script>


<div id="returnToTop" class="absolute bottom-0 right-8 animate-bounce text-center opacity-30 hover:opacity-100 cursor-pointer duration-[0.3s]" class:hidden on:click={() => window.document.getElementById("hero").scrollIntoView({behavior: "smooth", block: "start", inline: "nearest"})} >
    <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 fill-[#2b2d3b] dark:fill-white" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 0l-3 3a1 1 0 001.414 1.414L9 9.414V13a1 1 0 102 0V9.414l1.293 1.293a1 1 0 001.414-1.414z" clip-rule="evenodd" />
    </svg>
    <p class="absolute bg-white border border-gray-100 px-1 py-2 hover:block text-sm hidden">Return to top</p>
    
</div>


