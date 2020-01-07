  <script>
    import { Link } from 'svelte-routing';
  </script>

  <style>
    @import url('https://fonts.googleapis.com/css?family=Solway|Sulphur+Point&display=swap');
    /* *{font-family: 'Solway', serif;} */
    .nav-bar{
        height: 15%;
        margin-bottom: 55px;
        font-family: 'Solway', serif;
    }
    .nav-container{
        height: 100%;
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
        text-decoration: none
    }
  </style>
  
  <nav class = "nav-bar">
     <div class = "nav-container">
        <!-- <Link to="/"><span class="brand-logo">Linguage</span></Link> -->
        <!-- <Link to="/"><span class="logo"><img src= "./media/Linguage_banner.png" alt="logo"/></span></Link> -->
        <Link to="/"><img class= "logo" src= "./media/Linguage_banner.png" alt="logo"/></Link>
        <ul class="nav-buttons">
        <li><Link to="/">Explore</Link></li>
        <li><Link to="/">Compare</Link></li>
        <li><Link to="/">Create</Link></li>
      </ul>
     </div>
  </nav>

  