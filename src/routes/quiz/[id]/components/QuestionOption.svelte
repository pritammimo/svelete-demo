<script>
    export let option
    export let selectedOption
    export let handleChangeOption
    export let showCorrectAnswer;
    export let answer
</script>
<button
  class={`bg-gray-200 rounded w-[49%] text-center p-2 mb-4 py-5 ${
    option.label === selectedOption ? "bg-yellow-200" : null
  } ${
    showCorrectAnswer &&
    (answer === option.label ? "bg-green-300" : "bg-red-300")
  }`}
  on:click={() => handleChangeOption(option.label)}
>
  {option.text}
</button>