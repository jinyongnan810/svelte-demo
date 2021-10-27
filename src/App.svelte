<script lang="ts">
	import FeebackStats from "./components/FeebackStats.svelte";

	import FeedbackList from "./components/FeedbackList.svelte";
	import type { Feedback } from "./type.svelte";

	let feedbacks: Feedback[] = [
		{
			id: 1,
			rating: 10,
			text: "Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.",
		},
		{
			id: 2,
			rating: 9,
			text: "Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.",
		},
		{
			id: 3,
			rating: 8,
			text: "Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.",
		},
	];

	$: count = feedbacks.length;
	$: average =
		count == 0
			? 0
			: feedbacks.reduce((a, { rating }) => a + rating, 0) / count;

	const deleteFeedback = (e: CustomEvent<number>) => {
		const id = e.detail;
		feedbacks = feedbacks.filter((f) => f.id !== id);
	};
</script>

<main class="container">
	<FeebackStats {count} {average} />
	<FeedbackList {feedbacks} on:delete-feedback={deleteFeedback} />
</main>
