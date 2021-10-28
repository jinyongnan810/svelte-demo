<script lang="ts">
    import { createEventDispatcher } from "svelte";
    import { FeedbackStore } from "../stores";

    import Button from "./Button.svelte";
    import Card from "./Card.svelte";
    import RatingSelect from "./RatingSelect.svelte";

    let text = "";
    let rating = 7;
    let submitEnabled = true;
    let message = "";
    let minLength = 10;
    const dispatch = createEventDispatcher<{
        "form-submit": { text: string; rating: number };
    }>();
    const handleInput = () => {
        if (text.trim().length < minLength) {
            message = `Comment should have at leave ${minLength} characters.`;
            submitEnabled = true;
        } else {
            message = "";
            submitEnabled = false;
        }
    };
    const ratingSelected = (e: CustomEvent<number>) => {
        rating = e.detail;
        console.log(rating);
    };
    const handleSubmit = () => {
        FeedbackStore.update((current) => {
            return [
                {
                    id: current.length + 1,
                    rating: rating,
                    text: text,
                },
                ...current,
            ];
        });
        text = "";
    };
</script>

<Card>
    <header>
        <h2>How would you like to rate us?</h2>
    </header>
    <form on:submit|preventDefault={handleSubmit}>
        <RatingSelect on:rating-selected={ratingSelected} />
        <div class="input-group">
            <input
                type="text"
                bind:value={text}
                on:input={handleInput}
                placeholder="Please leave us a comment."
            />
            <Button type="submit" disabled={submitEnabled}>Send</Button>
        </div>
        {#if message}
            <div class="message">{message}</div>
        {/if}
    </form>
</Card>

<style>
    header {
        max-width: 400px;
        margin: auto;
    }
    header h2 {
        font-size: 22px;
        font-weight: 600;
        text-align: center;
    }
    .input-group {
        display: flex;
        flex-direction: row;
        border: 1px solid #ccc;
        padding: 8px 10px;
        border-radius: 8px;
        margin-top: 15px;
    }
    input {
        flex-grow: 2;
        border: none;
        font-size: 16px;
    }
    input:focus {
        outline: none;
    }
    .message {
        padding-top: 10px;
        text-align: center;
        color: rebeccapurple;
    }
</style>
