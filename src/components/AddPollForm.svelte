<script>
  import { createEventDispatcher } from "svelte";
  import Button from "../shared/Button.svelte";

  const dispatch = createEventDispatcher();

  let fields = {question:"", answerA:"", answerB:""}
  let errors = {question:"", answerA:"", answerB:""}
  let valid = false;

  const handleSubmit = () => {
    valid = true;

    // validate question
    if (fields.question.trim().length < 5) {
      errors.question = "Question must be atleast 5 characters long";
      valid = false;
    } else {
      errors.question = "";
    }

    // validate answerA
    if (fields.answerA.trim().length < 1) {
      errors.answerA = "Answer A cannot be empty";
      valid = false;
    } else {
      errors.answerA = "";
    }

    // validate answerB
    if (fields.answerB.trim().length < 1) {
      errors.answerB = "Answer B cannot be empty";
      valid = false;
    } else {
      errors.answerB = "";
    }

    if(valid){
      const polls = {...fields, votesA:0, votesB:0, id:Math.random()};
      dispatch("add", polls);
    }
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <div class="form-field">
    <label for="question">Poll Question:</label>
    <input type="text" id="question" bind:value={fields.question}>
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
    max-width: 400px;
    margin: 0 auto;
    text-align: center;
  }

  .form-field {
    margin: 18px auto;
  }

  label {
    margin: 10px auto;
    text-align: left;
  }

  input {
    width: 100%;
    border-radius: 6px;
  }

  .error {
    font-size: 12px;
    font-weight: bold;
    color: #d91b42;
  }
</style>