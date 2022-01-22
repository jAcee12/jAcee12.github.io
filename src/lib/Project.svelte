<script lang=ts>
    export let desc: string;
    export let title: string;
    let link: string;

</script>
<!-- 
<div class=" animate-marquee whitespace-nowrap">
    
    


</div> -->
<!-- <div class="dark:bg-[#2b2d3b] bg-white opacity-40 dark:text-white rounded-lg mb-10 w-full md:w-1/3 xl:w-1/4 px-4 flex-shrink-0 inline-flex">

    <div class="p-8 sm:p-9 md:p-7 xl:p-9 text-center">
        <h3 class="text-2xl md:text-3xl pb-1">{title}</h3>
        <p>{desc}</p>
    </div>

</div> -->

<!-- <div class="dark:bg-[#2b2d3b] bg-white opacity-40 dark:text-white rounded-lg flex w-1/3 px-4 flex-shrink-0">
    {title}
    {desc}
</div> -->

<div class="bg-white rounded-lg overflow-hidden mb-10 w-1/2 snap-center shrink-0">
    <div class="p-8 sm:p-9 md:p-7 xl:p-9 text-center">
        <h3 class="text-2xl md:text-3xl pb-1">{title}</h3>
        <p>{desc}</p>
    </div>
</div>

