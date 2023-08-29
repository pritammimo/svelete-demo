<script>
  import Card from "../components/Card.svelte";
import quizes from "../data.json";
import * as images from "../image";
</script>
{#each quizes as quiz (quiz.id)}
<Card {quiz}/>
{/each}

