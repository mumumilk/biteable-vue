<template>
  <div class="container">
    <div class="dot" />
    <div class="dot" />
    <div class="dot" />
    <div class="dot" />
  </div>
</template>

<style scoped>
  .container {
    display: flex;
  }

  .dot {
    width: 1rem;
    height: 1rem;
    border-radius: 50%;
    background-color: #eee;
  }

  @keyframes appear {
    from {
      transform: scale(0);
    }

    to {
      transform: scale(1);
    }
  }
  .dot:first-child {
    animation-name: appear;
    animation-duration: 0.7s;
    animation-iteration-count: infinite;
  }

  @keyframes moveL {
    from {
      transform: translateX(-100%);
    }

    to {
      transform: translateX(50%);
    }
  }
  .dot:nth-child(2) {
    animation-name: moveL;
    animation-duration: 0.7s;
    animation-iteration-count: infinite;
  }

  @keyframes moveR {
    from {
      transform: translateX(-50%);
    }

    to {
      transform: translateX(100%);
    }
  }
  .dot:nth-child(3) {
    animation-name: moveR;
    animation-duration: 0.7s;
    animation-iteration-count: infinite;
  }

  @keyframes disappear {
    from {
      transform: scale(1);
    }

    to {
      transform: scale(0);
    }
  }
  .dot:last-child {
    animation-name: disappear;
    animation-duration: 0.7s;
    animation-iteration-count: infinite;
    animation-delay: 0.7s;
  }
</style>
