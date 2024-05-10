<script lang="ts">
    export let textProps = '';
    export let fonctionProps = () => {};
    export let widthProps = 'fit-content'
        
</script>
        
<button class="thisBtn" on:click={fonctionProps} style="width: {widthProps}">{textProps}</button>

    
<style>

.thisBtn {
    padding: 16px 16px;
    margin-left: auto;
    margin-right: auto;
    font-size: 16px;
    display: block;
    margin-bottom: 50px;
    border-radius: 8px;
    color: rgb(255, 255, 255);
    background-color: rgb(15, 163, 15);
    border: 0px;
    transition: all ease 0.2s;
    cursor: pointer;
}

.thisBtn:hover {
    background-color: rgb(13, 147, 13);
    transition: all ease 0.2s;
}

</style>