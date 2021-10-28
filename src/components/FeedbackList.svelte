<script lang="ts">
    import type { Feedback } from "../type.svelte";
    import { fade, scale } from "svelte/transition";

    import FeedbackItem from "./FeedbackItem.svelte";

    export let feedbacks: Feedback[] = [];
</script>

{#each feedbacks as feedback (feedback.id)}
    <div in:scale out:fade>
        <FeedbackItem {feedback} on:delete-feedback />
    </div>
{/each}
