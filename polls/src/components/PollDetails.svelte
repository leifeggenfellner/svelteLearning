<script>
	import { tweened } from "svelte/motion";
    import PollStore from "../stores/PollStore.js";
    import Card from "../shared/Card.svelte";
    import Button from "../shared/Button.svelte";

    export let poll;

    $: totalVotes = poll.votesA + poll.votesB;
    $: percentA = Math.floor(poll.votesA / totalVotes * 100) || 0;
    $: percentB = Math.floor(poll.votesB / totalVotes * 100) || 0;

    const tweenedA = tweened(0, {duration: 200});
    const tweenedB = tweened(0, {duration: 200});
    $: tweenedA.set(percentA);
    $: tweenedB.set(percentB);

    const handleVote = (option, id) => {
        PollStore.update(currentPolls => {
            let copiedPolls = [...currentPolls];
            let upvotedPoll = copiedPolls.find((poll) => (poll.id === id));
    
            option === 'a' ? upvotedPoll.votesA++ : upvotedPoll.votesB++;
    
            return copiedPolls;
        });
    };

    const handleDelete = (id) => {
        PollStore.update((currentPolls) => {return currentPolls.filter((poll) => poll.id !== id);});
    };
</script>

<Card>
    <div class="poll">
        <h3>{ poll.question }</h3>
        <p>Total votes: { totalVotes }</p>
        <div class="answer" on:click={() => (handleVote('a', poll.id))}>
            <div class="percent percent-a" style="width: {$tweenedA}%"></div>
            <span>{ poll.answerA } ({ poll.votesA })</span>
        </div>
        <div class="answer" on:click={() => (handleVote('b', poll.id))}>
            <div class="percent percent-b" style="width: {$tweenedB}%"></div>
            <span>{ poll.answerB } ({ poll.votesB })</span>
        </div>
        <div class="delete">
            <Button flat={true} on:click={() => (handleDelete(poll.id))}>Delete</Button>
        </div>
    </div>
</Card>

<style>
    h3 {
        margin: 0 auto;
        color: #555;
    }

    p {
        margin-top: 6px;
        font-size: 14px;
        color: #aaa;
        margin-bottom: 30px;
    }

    .answer {
        background-color: #fafafa;
        cursor: pointer;
        margin: 10px auto;
        position: relative;
    }

    .answer:hover {
        opacity: 0.6;
    }

    span {
        display: inline-block;
        padding: 10px 20px;
    }

    .percent {
        height: 100%;
        position: absolute;
        box-sizing: border-box;
    }

    .percent-a {
        background-color: rgba(217, 27, 66, 0.2);
        border-left: 4px solid #d91b42;
    }

    .percent-b {
        background-color: rgba(69, 196, 150, 0.2);
        border-left: 4px solid #45c496;
    }

    .delete {
        margin-top: 30px;
        text-align: center;
    }
</style>