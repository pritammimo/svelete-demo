<script>
import quizes from "../data.json";
import * as images from "../image";
</script>
{#each quizes as quiz (quiz.id)}
<button
class="quiz-card shadow w-[250px] rounded overflow-hidden cursor-pointer m-2"
>
 <img class="h-44" src={images[quiz.imageUrl]} alt="" /> 
<div class="flex items-center justify-between py-3 px-2">
  <h1 class="font-bold">{quiz.name}</h1>
  <p>{quiz.questions.length} Quiz</p>
</div>
</button>
{/each}

