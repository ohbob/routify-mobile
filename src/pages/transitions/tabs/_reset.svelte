<script>
  import { TabsTransition } from "@roxi/routify/decorators";
  import BottomNav from "./_components/BottomNav.svelte";
  import { url, isActive } from "@roxi/routify";

  const _urls = [
    ["./home", "Home", "darkred"],
    ["./feed", "Feed", "darkred"],
    // ["./updates", "Updates", "#88f0d0"],
    // ["./settings", "Settings", "#a1fac3"],
  ];
  $: urls = _urls.map(([path, name, color]) => ({
    name,
    href: $url(path),
    color,
    active: !!$isActive(path),
  }));
</script>

<style>
  :global(body) {
    padding: 0;
  }
  * :global(.inset) {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  main.inset {
    bottom: 64px;
    overflow: hidden;
  }

  * :global(*) {
    text-align: center;
  }
</style>

<div style="height: 100%">
  <main class="inset">    
      <slot decorator={TabsTransition} />    
  </main>
  <BottomNav {urls} height="64px" />
</div>



<!-- routify:options bundle=true -->
