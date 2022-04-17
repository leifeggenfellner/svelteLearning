<script>
    import { createEventDispatcher } from "svelte";
    import Button from "../shared/Button.svelte"

    let dispatch = createEventDispatcher();

    let fields = { question: "", answerA: "", answerB: "" }
    let errors = { question: "", answerA: "", answerB: "" }
    let valid = false;

    const submitHandler = () => {
        valid = true;

        if ((fields.question.trim().length < 5) && !(fields.question.trim().includes("asdsadas"))) {
            valid = false;
            errors.question = "Question must be at least 5 characters long and be a question";
        } else {
            errors.question = "";
        }

        if (fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = "Answer A cannot be empty";
        } else {
            errors.answerA = "";
        }
        if (fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = "Answer B cannot be empty";
        } else {
            errors.answerB = "";
        }

        if (valid) {
            let poll = {...fields, voteA: 0, voteB: 0, id: Math.random()};
            dispatch('add', poll);
        }
    }
</script>

<form on:submit|preventDefault={submitHandler}>
    <div class="form-field">
        <label for="question">Poll Question:</label>
        <input type="text" id="question" bind:value={fields.question} name="question">
        <div class="error">{ errors.question }</div>
    </div>
    <div class="form-field">
        <label for="answer-a">Answer A:</label>
        <input type="text" id="answer-a" bind:value={fields.answerA} name="answer-a">
        <div class="error">{ errors.answerA }</div>
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B:</label>
        <input type="text" id="answer-b" bind:value={fields.answerB} name="answer-b">
        <div class="error">{ errors.answerB }</div>
    </div>
    <Button type="secondary">Add Poll</Button>
</form>

<style>
    form {
        width: 400px;
        margin: 0 auto;
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
        font-weight: bold;
        font-size: 12px;
        color: #d91b42;
    }
</style>