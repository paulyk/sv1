<style>
  .action-bar {
    padding: 0.7rem 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .action-bar > * {
    margin: 0 0.5rem;
  }
</style>

<div class="action-bar">
  <slot><a href="/">Action 1</a> <a href="/">Action 2</a></slot>
</div>
