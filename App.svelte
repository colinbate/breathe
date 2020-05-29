<script>
  let ready = false;
  let done = false;
  let countdown = 0;

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

  function start() {
    countdown = 7;
    setTimeout(dec, 1000);
  }
</script>

<style>
  :global(:root) {
    --primary: #ff3e00;
    --ambient: #fff;
  }
  @media (prefers-color-scheme: dark) {
    :global(:root) {
      --ambient: #111;
    }
  }
  :global(body) {
    background-color: var(--ambient, #fff);
  }

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
    color: var(--primary);
    text-align: center;
  }

  button {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
      Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
    border-radius: 9000px;
    border: 1px solid var(--primary);
    background-color: transparent;
    color: var(--primary);
    font-size: 2rem;
    font-weight: 100;
    text-transform: uppercase;
    width: 4rem;
    height: 4rem;
    padding: 0;
    cursor: pointer;
  }
</style>

<main>
  {#if done}
  <div class="ready">Done</div>
  {:else if ready}
  <svg viewBox="0 0 100 100">
    <circle cx="50" cy="50" r="45" stroke="#ff3e00" stroke-width="8" fill="none" />
  </svg>
  {:else}
  <div class="ready">
    <div>Breathe for 5 min</div>
    <div>Ready?</div>
    <button type="button" on:click|once={start}>{#if countdown > 0}{countdown}{:else}Go{/if}</button>
  </div>
  {/if}
</main>