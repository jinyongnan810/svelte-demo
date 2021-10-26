<script lang="ts">
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
	const deleteFeedback = (e: CustomEvent<number>) => {
		const id = e.detail;
		feedbacks = feedbacks.filter((f) => f.id !== id);
	};
</script>

<main class="container">
	<FeedbackList {feedbacks} on:delete-feedback={deleteFeedback} />
</main>
