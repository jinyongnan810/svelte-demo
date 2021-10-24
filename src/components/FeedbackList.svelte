<script lang="ts">
    import type { Feedback } from "../type.svelte";

    import FeedbackItem from "./FeedbackItem.svelte";

    export let feedbacks: Feedback[] = [];
</script>

{#each feedbacks as feedback (feedback.id)}
    <FeedbackItem {feedback} />
{/each}
