<!-- Layout.svelte -->
<script>
import Pokédex_logo from '$lib/images/Pokédex_logo.png';
</script>
  
  <div class="layout">
    <div class="logoLayoutContainer">
        <a href="/">
            <img class="logoLayout" src="https://archives.bulbagarden.net/media/upload/4/4b/Pok%C3%A9dex_logo.png" alt="" />
        </a>
    </div>
    <slot></slot>
  </div>

<style>


.logoLayout {
    width: 200px;
    cursor: pointer;
    transition: all ease 0.2s;
}

.logoLayout:hover {
    scale: 1.1;
    transition: all ease 0.2s;
}

.logoLayoutContainer {
    width: 96%;
    margin-top: 28px;
    margin-left: auto;
    margin-right: auto;
}

</style>