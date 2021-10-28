<script lang="ts">
    import { fade, scale } from "svelte/transition";
    // import { onDestroy } from "svelte";

    import FeedbackItem from "./FeedbackItem.svelte";
    import { FeedbackStore } from "../stores";

    //#region  first way to get data from store
    // let feedbacks: Feedback[] = [];
    // const unSubscribe = FeedbackStore.subscribe((data) => {
    //     feedbacks = data;
    // });
    // onDestroy(() => {
    //     unSubscribe();
    // });
    //#endregion
</script>

<!-- the second way to get data from store -->
{#each $FeedbackStore as feedback (feedback.id)}
    <div in:scale out:fade>
        <FeedbackItem {feedback} />
    </div>
{/each}
