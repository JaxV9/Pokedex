<!-- Layout.svelte -->
<script>
import Pokédex_logo from '$lib/images/Pokédex_logo.png';
</script>
  
  <div class="layout">
    <div class="logoLayoutContainer">
        <div>
            <a href="/">
                <img class="logoLayout" src="https://archives.bulbagarden.net/media/upload/4/4b/Pok%C3%A9dex_logo.png" alt="" />
            </a>
        </div>
        <div class="navLinkContainer">
            <a class="navLink" href="/search">
                <div>
                        Search
                </div>
            </a>
        </div>
    </div>
    <slot></slot>
  </div>

<style>

.logoLayoutContainer {
    width: 96%;
    margin-top: 28px;
    margin-left: auto;
    margin-right: auto;
}

.logoLayout {
    width: 200px;
    cursor: pointer;
    transition: all ease 0.2s;
}

.navLinkContainer {
    display: grid;
    grid-template-columns: repeat(auto-fill);
	column-gap: 16px;
    width: 70%;
    margin-top: 28px;
}

.navLinkContainer > a {
    border: 1px #FFFFFF solid;
    text-align: center;
    width: fit-content;
}

.navLink {
    width: 100%;
    color: #FFFFFF;
    display: block;
    padding: 8px 16px;
    transition: all ease 0.2s;
}

.navLink:hover {
    background-color: #FFFFFF;
    color: #333333;
    transition: all ease 0.2s;
}

.logoLayout:hover {
    scale: 1.1;
    transition: all ease 0.2s;
}



</style>