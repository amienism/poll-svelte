<script>
  // import {createEventDispatcher} from 'svelte';
  import Card from "../shared/Card.svelte";
  import PollStore from "../store/PollStore.js";

  // const dispatch = createEventDispatcher();

    export let poll;

     // Reactive values
     $: totalVotes = poll.votesA + poll.votesB;
     $: percentA = Math.floor(100 / totalVotes * poll.votesA)
     $: percentB = Math.floor(100 / totalVotes * poll.votesB)

    //  const handleVote = (option, id) => {
        // dispatch('vote', {option, id});
    //  }

     const handleVote = (option, id) => {
      
      PollStore.update(currentPolls => {

        let copiedPolls = [...currentPolls];
        let upvotedPoll = copiedPolls.find((poll) => poll.id == id);
  
        if (option === 'a'){
          upvotedPoll.votesA++;
        }
        if (option === 'b'){
          upvotedPoll.votesB++;
        }
        
        return copiedPolls;
      });

    };
</script>

<Card>
  <div class="poll">
      <h3>{poll.question}</h3>
      <p>Total Votes: {totalVotes}</p>
      <div class="answer" on:click={() => handleVote('a', poll.id)}>
          <div class="percent percent-a" style="width: {percentA}%;"></div>
          <span>{poll.answerA} ({poll.votesA})</span>
          
      </div>
      <div class="answer" on:click={() => handleVote('b', poll.id)}>
          <div class="percent percent-b" style="width: {percentB}%;"></div>
          <span>{poll.answerB} ({poll.votesB})</span>
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
    color: #aaa;
    margin-bottom: 30px;
  }
  .answer{
    background: #fafafa;
    cursor: pointer;
    margin: 10px auto;
    position: relative;
  }
  .answer:hover{
    opacity: 0.6;
  }
  span{
    display: inline-block;
    padding: 10px 20px;
  }

  .percent {
    height: 100%;
    position: absolute;
    box-sizing: border-box;
  }

  .percent-a {
    border-left: 2px solid rgba(217, 27, 66, 0.2);
    background: rgba(217, 27, 66, 0.2);

  }

  .percent-b {
    border-left: 2px solid rgba(69, 196, 150, 0.2);
    background: rgba(69, 196, 150, 0.2);
  }
</style>