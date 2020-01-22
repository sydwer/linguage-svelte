<script>
    import { Link } from 'svelte-routing';
    let explore = './media/explore_button.png'
    let create = './media/create_button.png'
    let compare = './media/compare_button.png'
    let bgImage = './media/enso2.png'

    let greeting = 'Hello,'
    // var greetings = ['Willkommen zu', 'Bienvenido a', 'karibu', 'へようこそ','欢迎来到','어서 오십시오',];
    const greetings = [',اهلا','Hola,','こんにちは,','Hallo,','Aloha,','안녕하세요,','你好,',"Yá'át'ééh,",'Hamjambo,','Hello,']

    textSequence(0);
    function textSequence(i) {
        if (greetings.length > i) {
            setTimeout(function() {
                greeting = greetings[i];
                // greeting = greetings[Math.floor(Math.random()*greetings.length)]
                textSequence(++i);
                }, 3000); 
            } else if (greetings.length == i) { 
                textSequence(0);
            }
        }

</script>

<style>
 @import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    .main{
        padding-left: 3rem;
        padding-right: 3rem;
        display: flex;
        justify-content: space-between
    }
    .info{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 30%;
        padding-right: 4rem;
        font-family: 'Solway', serif;
    }
    .circle{
        height:43.2rem;
        width: 75%;
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
        display: grid;
        grid-template-columns: repeat(12, 1fr);
        grid-template-rows: repeat(12,1fr);
    }
   img{
       height:11rem
   }

   
   #explore-link{
       grid-column: 5;
       grid-row: 7
   }
   #compare-link{
       position: relative;
       right: 2rem;
       grid-column-end: 9;
       grid-row: 7;
   }
    #create-link{
       position: relative;
       left: 1.4rem;
       grid-column-end: 7;
   }
   .circle-link:hover{
       transform: scale(1.05)
   }
   .circle-link:active{
       transform: scale(1)
   }
   span{
       font-weight: bolder;
       text-decoration: underline;
   }
  h1{
      height: 2rem;
      width: 100%;
      margin: 0;
      display: flex;
      justify-content: flex-start;
  }
  #greeting{
      color:#598502; 
  }
  
</style>


<div class = "main">
<div class="circle" style="background-image: url('{bgImage}')">
    <div id = "explore-link" class="circle-link">
        <Link to="/explore"  >
            <img class="exploreImg" src= { explore } alt="explore"/>
        </Link>
    </div>
 
    <div id="create-link" class="circle-link">
        <Link to="/create" >
            <img class="comingImg" src= { create } alt="create"/>
        </Link>
    </div>
    <div id="compare-link" class="circle-link">
        <Link to="/compare" >
            <img class="compareImg" src= { compare } alt="compare"/>   
        </Link>
    </div> 
</div> 
<div class = "info">
<h1 id="greeting">{greeting}</h1>
<br/>
<h1> Welcome to Lin-guage</h1>
<p>Lin-guage is a language exploration website. It's main function is to allow you, the user, 
to learn about and play with languages in a number of ways.
<br> 
<br>
<span>"Explore":</span><br> Learn about specific languages. How many speakers does it have? How do you say "Hello"? What grammar system does it use?
<br>
<br>
<span>"Compare":</span><br> See a list of language comparisons, ordered from easiest to hardest to learn. 
<br>
<br>
<span>"Create":</span><br> Make your own language. Pick traits you want your language to have, and Lin-guage will generate a totally unique mini grammar and dictionary for you.

</p>
</div>
</div> 
