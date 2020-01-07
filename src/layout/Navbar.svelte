  <script>
    import { Link } from 'svelte-routing';
  </script>
  
  <nav>
     <div class = "nav-container">
        <!-- <Link to="/"><span class="brand-logo">Linguage</span></Link> -->
        <Link to="/"><span class="logo"><img src= "./media/Linguage_banner.png" alt="logo"/></span></Link>
        <ul id="nav-bar" class="nav-buttons">
        <li><Link to="/">Explore</Link></li>
        <li><Link to="/">Compare</Link></li>
        <li><Link to="/">Create</Link></li>
      </ul>
     </div>
  </nav>

    <!-- <nav>
    <div class="nav-wrapper">
     <div class = "container">
        <Link to="/"><img class = "brand-logo" src= "./media/Linguage_banner.png" alt="logo"/></Link>
        <Link to="/"><span class="logo"><img src= "./media/Linguage_banner.png" alt="logo"/></span></Link>
        <ul id="nav-mobile" class="right hide-on-med-and-down">
        <img class = "logo" src= "./media/Linguage_banner.png" alt="logo"/>
        <li><Link to="/">Explore</Link></li>
        <li><Link to="/">Compare</Link></li>
        <li><Link to="/">Create</Link></li>
      </ul>
     </div>
    </div>
  </nav> -->