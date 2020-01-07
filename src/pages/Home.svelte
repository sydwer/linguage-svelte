<script>
    let explore = "./media/explore_button.png"
    let create = "./media/create_button.png"
    let compare = "./media/compare_button.png"
    let bgImage = './media/enso2.png'
</script>

<style>
    .main{
        padding: 3rem;
        display: flex;
        justify-content: space-between
    }
    .info{
        width: 25%;
        padding-right: 4rem
    }
    .circle{
        height:43.2rem;
        width: 75%;
        background-size: cover;
        background-position: center;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-template-rows: 1fr 1fr 1fr;
    }
   img{
       height:10rem
   }
</style>
<!-- style="background-image: url('{bgImage}')" -->
<div class = "main">
<div class="circle" style="background-image: url('{bgImage}')">
    <a class = "explore-link" href="/">
        <img class="exploreImg" src= { explore } alt="explore"/>
    </a>

    <a class="create-link" href="/">
        <img class="comingImg" src= { create } alt="create"/>
    </a>
            
    <a class="compare-link" href="/">
         <img class="compareImg" src= { compare } alt="compare"/>   
    </a>
</div> 
<div class = "info">
<h1> What is Lin-guage?</h1>
<p>Lin-guage is a language exploration website. It's main function is to allow you, the user, 
to learn about languages in a number of ways.<br> 
<br>
You can "Explore" and learn about specific languages, like how many speakers they have, to what grammar system they use.<br>
You can "Compare" and see a list of language comparisons, in order of easies to hardest to learn. <br>
<br>
And finally, you can "Create" a language. Taking in details about languages you like, Lin-guage will generate your own unique language.

</p>
</div>
</div> 
