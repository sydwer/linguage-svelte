  <script>
    import { Link } from 'svelte-routing';
  </script>

  <style>
    @import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    .nav-bar{
        padding-left: 3rem;
        padding-right: 3rem;
        height: 15%;
        margin-bottom: 10px;
        font-family: 'Solway', serif;
    }
    .nav-container{
        height: 7rem;
        display: flex;
        flex-direction: row;
        justify-content: space-between
    }
    .logo{
    height: 100%;
    }
    .nav-buttons{
        display: flex;
        flex-direction: row;
        list-style-type: none;
    }
    .nav-buttons>li{
        padding: 5px;
    }

  
    :any-link { color: black !important }
    :any-link:active { color: #bfda01 !important }
    :any-link:hover { color: #5fa40f !important} 
   
  </style>
  
  <nav class = "nav-bar">
     <div class = "nav-container">
        <!-- <Link to="/"><span class="brand-logo">Linguage</span></Link> -->
        <!-- <Link to="/"><span class="logo"><img src= "./media/Linguage_banner.png" alt="logo"/></span></Link> -->
        <Link to="/"><img class= "logo" src= "./media/Linguage_banner.png" alt="logo"/></Link>
        <ul class="nav-buttons">
        <li><Link to="/">Home</Link></li>
        <li><Link to="/explore">Explore</Link></li>
        <li><Link to="/compare">Compare</Link></li>
        <li><Link to="/create">Create</Link></li>
      </ul>
     </div>
  </nav>

  