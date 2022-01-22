<script lang=ts>
    export let toggled: boolean = false;
</script>


<label class="switch">
    <input type="checkbox" bind:checked={toggled} />
    <span class="slider" />
</label>