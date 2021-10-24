<script lang="ts">
    import type { Feedback } from "../type.svelte";
    import Card from "./Card.svelte";
    export let feedback: Feedback = null;
</script>

<Card>
    <div class="rate">{feedback.rating}</div>
    <button class="close">x</button>
    <div class="comment">{feedback.text}</div>
</Card>

<style>
    .rate {
        position: absolute;
        top: -10px;
        left: -10px;
        width: 50px;
        height: 50px;
        background: #ff6a95;
        color: #fff;
        border: 1px #eee solid;
        border-radius: 50%;
        padding: 10px;
        text-align: center;
        font-size: 19px;
    }
    .close {
        position: absolute;
        top: 10px;
        right: 20px;
        cursor: pointer;
        background: none;
        border: none;
    }
</style>
