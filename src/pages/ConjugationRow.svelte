<script>
    export let pronoun;
    export let generatedPronoun;
</script>

<style>
   h3{
       border: 2px solid black;
       margin: 0;
   }
   #pronoun{
       border-right: 1px solid grey;
   }
</style>


<h3><span id="pronoun">{pronoun}</span>  <span>{generatedPronoun}</span></h3>
