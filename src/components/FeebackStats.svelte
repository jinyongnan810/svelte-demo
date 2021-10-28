<script lang="ts">
    import { FeedbackStore } from "../stores";

    $: count = $FeedbackStore.length;
    $: average =
        count == 0
            ? 0
            : $FeedbackStore.reduce((a, { rating }) => a + rating, 0) / count;
</script>

<div class="feedback-stats">
    <h4>{count} Reviews.</h4>
    <h4>Average Rating:{average}</h4>
</div>

<style>
    .feedback-stats {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>
