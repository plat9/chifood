<script>
  import { onMount } from 'svelte';
  import logo from '$lib/assets/logo2.png';
 

  let menuToggle;
  let navbar;
  let isOpen = false;

  function toggleMenu() {
    isOpen = !isOpen;
  }
</script>

<nav class="navbar">
  <img src={logo} alt="Logo">
  <ul class="nav-links" class:open={isOpen}>
    <li><a href="#">Home</a></li>
    <li><a href="#">Order online</a></li>
    <li><a href="#">Menu</a></li>
    <li><a href="#">Location</a></li>
  </ul>
  <span class="menu-toggle" on:click={toggleMenu}>&#9776;</span>
</nav>

<style>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    background: #333;
    color: white;
    position: relative;
  }
  .nav-links {
    list-style: none;
    display: flex;
    gap: 2rem;
  }
  .nav-links li {
    font-size: 1.2rem;
  }
  
  .nav-links li a {
    transition: all 0.3s ease;
    text-decoration: none;
    color: white;
    background: #dc2626;
    padding: 8px 16px;
    border-radius: 4px;
    display: block;
  }
  
  .nav-links li a:hover {
    background: #b91c1c;
    transform: translateY(-2px);
  }
  
  .nav-links.open {
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: #333;
    padding: 10px 0;
    gap: 0;
    z-index: 1000;
  }
  
  .nav-links.open li {
    width: 100%;
  }
  
  .nav-links.open li a {
    width: 100%;
    text-align: center;
  }
.menu-toggle {
  display: none;
  font-size: 2rem;
  cursor: pointer;
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    flex-direction: column;
    background: #333;
    width: 100%;
    padding: 10px 0;
    z-index: 1000;
  }
  
  .nav-links.open {
    display: flex;
  }
  
  .menu-toggle {
    display: block;
  }
}

</style>
