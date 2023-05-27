<script>
    import PollStore from '../stores/PollStore.js';
    import { createEventDispatcher } from 'svelte';
    import Button from "../shared/button.svelte";

    const dispatch = createEventDispatcher();   

    let fields = {question: '', answerA: '', answerB: ''};
    let errors = {question: '', answerA: '', answerB: ''};
    let valid = false;

    const submitHandler = (e) => {
        
        valid = true;
        //validate question
        if(fields.question.trim().length < 5){
            valid = false;
            errors.question = 'Question must be at least 5 characters long';
        }
        else{
            errors.question = '';
        }
        //validate answer a
        if(fields.answerA.trim().length < 1){
            valid = false;
            errors.answerA = 'Answer A is required';
        }
        else{
            errors.answerA = '';
        }

        //validate answer b
        if(fields.answerB.trim().length < 1){
            valid = false;
            errors.answerB = 'Answer B is required';
        }
        else{
            errors.answerB = '';
        }

        // add new poll
        if(valid){
            let poll  = { ...fields, votesA: 0, votesB: 0, id: Math.random() };
            PollStore.update(currentPolls => {
                return [poll, ...currentPolls];
            })
            dispatch('add');
        }
    }
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question</label>
        <input type="text" name="" id="question" bind:value={fields.question}>
        <div class="error">{errors.question}</div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A:</label>
        <input type="text" name="" id="answer-a" bind:value={fields.answerA}>
        <div class="error">{errors.answerA}</div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B:</label>
        <input type="text" name="" id="naswer-b" bind:value={fields.answerB}>
        <div class="error">{errors.answerB}</div>
    </div>
    <Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
    form{
        width:400px;
        margin: 0 auto;
        text-align: center;
    }
    .form-field{
        margin-bottom: 18px auto;
    }
    input{
        width: 100%;
        border-radius: 8px;
    }
    label{
        text-align: left;
        margin: 10px auto;
    }
    .error{
        color: #d91b42;
        font-size: 12px;
        font-weight: bold;
    }
    
</style>