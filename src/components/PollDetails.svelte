<script>
    import Card from "../shared/card.svelte";
    import PollStore from "../stores/PollStore.js";
    import Button from "../shared/button.svelte";
    import { tweened } from 'svelte/motion'
    export let poll;


    $: totalVotes = poll.votesA + poll.votesB;
    $: percentA = Math.floor(poll.votesA / totalVotes * 100) || 0;
    $: percentB = Math.floor(poll.votesB / totalVotes * 100) || 0;

    //tweened percentages
    const tweenedA = tweened(0);
    const tweenedB = tweened(0);
    $: tweenedA.set(percentA);
    $: tweenedB.set(percentB);
    // $: console.log(tweenedA, tweenedB);

    //handleing votes
    const handleVote = (option, id) => {

        PollStore.update(currentPolls => {
            let copiedPolls = [...currentPolls];
            let upvotedPolls = copiedPolls.find(poll => poll.id === id);
    
            if(option === 'a'){
                upvotedPolls.votesA += 1;
            }
            if(option === 'b'){
                upvotedPolls.votesB += 1;
            }
    
            return copiedPolls;
        });
};

const handleDelete = (id) => {
    PollStore.update(currentPolls => {
        return currentPolls.filter(poll => poll.id !== id);
    });
}; 
</script>

<Card>
    <div class="poll">
        <h3>{ poll.question }</h3>
        <p>Total Votes: {totalVotes }</p>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="answer" on:click={ () => handleVote('a', poll.id)}>
            <div class="percent percent-a" style="width: {$tweenedA}%"></div>
            <span> {poll.answerA} ({poll.votesA}) </span>
        </div>
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="answer" on:click={ () => handleVote('b', poll.id)}>
            <div class="percent percent-b" style="width: {$tweenedB}%"></div>
            <span> {poll.answerB} ({poll.votesB}) </span>
        </div>
        <div class="delete">
            <Button flat={true} on:click = {()=> {handleDelete(poll.id)}}>Delete</Button>
        </div>
    </div>  
</Card>


<style>
    h3{ 
        margin: 0 auto;
        color: #555;
    }
    p{
        margin-top: 6px;
        font-size: 14px;
        margin-bottom: 30px;
        color: #aaa;
    }
    .answer{
        background: #fafafa;
        position: relative;
        cursor: pointer;
        margin: 10px auto;
    }
    .answer:hover{
        opacity: 0.8;
    }
    span{
        display: inline-block;
        padding: 10px 20px;
    }
    .percent{
        position: absolute;
        top: 0;
        left: 0;
        height: 100%;
        background: #f44336;
        box-sizing: border-box;
    }
    .percent-a{
        border-left: 4px solid #d91b42;
        background: rgba(217, 27, 66, 0.2);
    }

    .percent-b{
        border-left: 4px solid #42c496;
        background: rgba(66,196, 150, 0.2);
    }
    .delete{
        margin-top: 30px;
        text-align: center;
    }
</style>
