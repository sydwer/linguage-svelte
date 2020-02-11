<script>
    export let nouns
    export let verbs
    export let adj

    function findWord(array, latinValue){
        const obj = array.find(obj => obj.original === latinValue)
        return obj
    }

   const bear = findWord(nouns, "Bear")
   const die = findWord(verbs, "Die")
   const big = findWord(adj, "Big")
</script>


<h1>{bear.original}</h1>
<h1>{die.original}</h1>
<h1>{big.original}</h1>
<!-- verb kickers, multiple clauses are a must, so is dat/acc verbs and movement/stationary past. -->
<!-- include nach vs zu example -->