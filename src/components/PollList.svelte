<script>
    // import { onMount, onDestroy } from "svelte";
    import PollDetails from "./PollDetails.svelte";
    import PollStore from "../store/PollStore.js";
    export let polls = [];

//    const unsub = PollStore.subscribe(data => {
//     polls = data;
//    })

//    onMount(() => {

//    });

//    onDestroy(() => {
//     unsub();
//    });


</script>


    <div class="poll-list">
        {#each $PollStore as poll (poll.id)}
            <div>
                <PollDetails {poll}/>
            </div>
        {/each}
    </div>

<style>
    .poll-list {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>