<script>
  import QuestionButton from "./components/QuestionButton.svelte";
import QuestionOption from "./components/QuestionOption.svelte";
import QuestionsText from "./components/QuestionsText.svelte";
import { answers } from "../../../store";
import { goto } from "$app/navigation";
  import QuestionProgressCircle from "./components/QuestionProgressCircle.svelte";
  import { onMount } from "svelte";
    let currentQuestionIndex=0;
    let showCorrectAnswer = false;
    let answersValue
    answers.subscribe((value) => {
    answersValue = value;
  });
  const handleChangeOption = (label) => {
    selectedOption = label;
  };
  const handleNext = () => {
    showCorrectAnswer = false;
    selectedOption = null;
    if (currentQuestionIndex === data.questions.length - 1) {
      goto("/results");
    } else {
      currentQuestionIndex++;
    }
  };
  let selectedOption=null;
    export let data;
    $: question = data.questions[currentQuestionIndex];
    const handleSubmit = () => {
    if (!selectedOption) return;

    showCorrectAnswer = true;
    answers.update((currentState) => {
      const updatedAnswerState = currentState;
      updatedAnswerState[currentQuestionIndex].isCorrect =
        selectedOption === question.answer;
      return updatedAnswerState;
    });
  };
  onMount(() => {
    answers.set(
      data.questions.map((question) => {
        return {
          id: question.id,
          isCorrect: null,
        };
      })
    );
  });
</script>
<div class="w-full">
  <div class="flex justify-center">
    {#each answersValue as answer}
      <QuestionProgressCircle isCorrect={answer.isCorrect} />
    {/each}
  </div>
    <QuestionsText text={question.question}/>
    <div class="flex justify-between flex-wrap cursor-pointer">
      {#each question.options as option (option.id) }
      <QuestionOption 
      {option}
      {selectedOption}
      {handleChangeOption}
      {showCorrectAnswer}
      answer={question.answer}
      />
      {/each}
     
    </div>
    <QuestionButton {handleSubmit} {showCorrectAnswer} {handleNext}/>
</div>