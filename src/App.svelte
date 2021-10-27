<script lang="ts">
	import FeebackStats from "./components/FeebackStats.svelte";
	import FeedbackForm from "./components/FeedbackForm.svelte";

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
	const onFormSubmitted = (
		e: CustomEvent<{ text: string; rating: number }>
	) => {
		// this not work
		// feedbacks.push({
		// 	id: feedbacks.length + 1,
		// 	rating: e.detail.rating,
		// 	text: e.detail.text,
		// });
		// this works
		feedbacks = [
			{
				id: feedbacks.length + 1,
				rating: e.detail.rating,
				text: e.detail.text,
			},
			...feedbacks,
		];
		// console.log(JSON.stringify(feedbacks));
	};
</script>

<main class="container">
	<FeedbackForm on:form-submit={onFormSubmitted} />
	<FeebackStats {count} {average} />
	<FeedbackList {feedbacks} on:delete-feedback={deleteFeedback} />
</main>
