<script lang="ts">
    export let textProps = '';
    export let fonctionProps = () => {};
    export let widthProps = 'fit-content'
    export let enabledProps = true
        
</script>
{#if enabledProps}   
    <button class="thisBtn" on:click={fonctionProps} style="width: {widthProps}">{textProps}</button>
    {:else}
    <button class="thisBtnDisabled" style="width: {widthProps}" disabled>{textProps}</button>
{/if}
    
<style>

.thisBtn, .thisBtnDisabled {
    padding: 16px 16px;
    margin-left: auto;
    margin-right: auto;
    font-size: 16px;
    display: block;
    margin-bottom: 50px;
    border-radius: 8px;
    border: 0px;
    transition: all ease 0.2s;
}

.thisBtn {
    background-color: rgb(15, 163, 15);
    color: rgb(255, 255, 255);
    cursor: pointer;
}

.thisBtn:hover {
    background-color: rgb(13, 147, 13);
    transition: all ease 0.2s;
}

.thisBtnDisabled {
    background-color: rgb(219, 219, 219);
    color: #333333;
    opacity: 0.8;
}

</style>