<script>
  import { onMount } from "svelte";
  let ready = false;
  let done = false;
  let countdown = 7;

  function finish() {
    done = true;
  }

  function dec() {
    countdown = Math.max(countdown - 1, 0);
    if (countdown === 0) {
      ready = true;
      setTimeout(finish, 300000);
    } else {
      setTimeout(dec, 1000);
    }
  }

  onMount(() => {
    setTimeout(dec, 1000);
  });
</script>

<style>
  main {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
      Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }

  svg {
    width: 90vmin;
    height: 90vmin;
  }

  @keyframes pulse {
    from {
      transform: scale(0.95);
    }
    to {
      transform: scale(0.2);
    }
  }

  circle {
    animation-name: pulse;
    animation-duration: 4286ms;
    transform-origin: center center;
    animation-iteration-count: infinite;
    animation-timing-function: cubic-bezier(0.64, 0, 0.36, 1);
    animation-direction: alternate-reverse;
  }

  .ready {
    font-size: 3rem;
    font-weight: 100;
    text-transform: uppercase;
    color: #ff3e00;
    text-align: center;
  }
</style>

<main>
  {#if done}
  <div class="ready">Done</div>
  {:else if ready}
  <svg viewBox="0 0 100 100">
    <circle cx="50" cy="50" r="50" fill="#ff3e00"/>
  </svg>
  {:else}
  <div class="ready">
    <div>Ready?</div>
    <div>{countdown}</div>
  </div>
  {/if}
</main>