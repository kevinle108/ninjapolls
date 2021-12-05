<script>
  import Button from "../shared/Button.svelte";
  import { createEventDispatcher } from "svelte";

  let dispatch = createEventDispatcher();
  let fields = {
    question: '',
    answerA: '',
    answerB: ''
  };

  let errors = {
    question: '',
    answerA: '',
    answerB: ''
  };

  let valid = false;



  const submitHandler = () => {
    valid = true;
    
    if (fields.question.length < 5) {
      errors.question = 'Question must be at least 5 characters long'
      valid = false;
    } else {
      errors.question = '';
    }

    if (fields.answerA.length < 1) {
      errors.answerA = 'Answer A cannot be empty';
      valid = false;
    } else {
      errors.answerA = '';
    }

    if (fields.answerB.length < 1) {
      errors.answerB = 'Answer B cannot be empty';
      valid = false;
    } else {
      errors.answerB = '';
    }

    if (valid) {
      console.log('valid', fields);
      let poll = {...fields, votesA: 0, votesB: 0};
      dispatch('add', poll)
    }    
  }


</script>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-field">
    <label for="question">Poll Question:</label>
    <input type="text" id="question" bind:value={fields.question}/>
    <div class="error">{errors.question}</div>
  </div>
  <div class="form-field">
    <label for="answer-a">Answer A:</label>
    <input type="text" id="answer-a" bind:value={fields.answerA}>
    <div class="error">{errors.answerA}</div>
  </div>
  <div class="form-field">
    <label for="answer-b">Answer B:</label>
    <input type="text" id="answer-b" bind:value={fields.answerB}>
    <div class="error">{errors.answerB}</div>
  </div>
  <Button type="secondary" flat={true}>Add Poll</Button>
</form>


<style>
  form {
    margin: 0 auto;
    width: 400px;
    text-align: center;
  }
  .form-field {
    margin: 18px auto;
  }
  input {
    width: 100%;
    border-radius: 6px;
  }
  label {
    margin: 10px auto;
    text-align: left;
  }
  .error {
    color: #d91b42;
    font-size: 12px;
    font-weight: bold;
  }

</style>