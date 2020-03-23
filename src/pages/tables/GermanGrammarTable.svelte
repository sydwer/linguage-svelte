<script>
    export let pronouns;
    const nom = pronouns.nom;
    const acc = pronouns.acc;
    const dat = pronouns.dat;
    const gen = pronouns.gen;
    console.log(nom)
    // restructure pronouns so that it's by person rather than case, so that this can be component

</script>


<style>
    div{
        width: 100%;
        border-top: 1px double black;
    }
    h3{
       color: grey;
       border-bottom: 1px double black;
       margin: 0;
       display: grid;
       grid-template-columns: repeat(5, 1fr);
   }
   span{
       /* color: grey; */
       border-right: 1px dotted black;
       display: flex;
       justify-content: center;
   }
   .table-header{
       color: black;
       border-left: 1px dotted black;
   }

   h4{
       margin: 0;
       padding: 7px;
       color: grey;
       display: flex;
       justify-content: center;
       border-bottom: 1px dotted black;
   }
   

  

</style>
<div id="table">
<h3 class="table-header"><span>-</span><span>Nominative</span><span>Accusative</span><span>Dative</span><span>Genitive</span></h3>
    <!-- {#each pronouns as pronoun}
  <h3><span class="table-header">{pronoun.original}</span><span>{pronoun.nominative}</span><span>Acc.</span><span>Dat.</span><span>Gen.</span></h3>

    {/each} -->
<h4>--Singular Pronouns--</h4>
<h3>
    <span class="table-header">I</span><span>{nom.i.latin}</span><span>{acc.i.latin}</span><span>{dat.i.latin}</span>
    <span>{gen.i.latin}</span>
</h3>
<h3>
    <span class="table-header">You</span><span>{nom.you.latin}</span><span>{acc.you.latin}</span>
    <span>{dat.you.latin}</span><span>{gen.you.latin}</span>
</h3>
<h3>
    <span class="table-header">He</span><span>{nom.he.latin}</span><span>{acc.he.latin}</span>
    <span>{dat.he.latin}</span><span>{gen.he.latin}</span>
</h3>
<h3>
    <span class="table-header">She</span><span>{nom.she.latin}</span><span>{acc.she.latin}</span>
    <span>{dat.she.latin}</span><span>{dat.she.latin}</span>
</h3>
<h3>
    <span class="table-header">It</span><span>{nom.it.latin}</span><span>{acc.it.latin}</span>
    <span>{dat.it.latin}</span><span>{dat.it.latin}</span>
</h3>
<h4>--Plurals--</h4>
<h3>
    <span class="table-header">We</span><span>{nom.we.latin}</span><span>{acc.we.latin}</span>
    <span>{dat.we.latin}</span><span>{gen.we.latin}</span>
</h3>
<h3>
    <span class="table-header">You All</span><span>{nom.you_all.latin}</span><span>{acc.you_all.latin}</span>
    <span>{dat.you_all.latin}</span><span>{gen.you_all.latin}</span>
</h3>
<h3>
    <span class="table-header">They</span><span>{nom.they.latin}</span><span>{acc.they.latin}</span>
    <span>{dat.they.latin}</span><span>{gen.they.latin}</span>
</h3>

</div>