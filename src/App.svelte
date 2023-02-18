<script lang="ts">
  import { writable } from 'svelte/store';

  const state = writable({
    playercount: 3,
    level: 1,
    battlecount: 4,
  })
</script>

<main class="container">
  <h1>13th Age Battle Calculator</h1>

  <div class="row">
    <div class="column column-33">
      <label for="playercount">I have this many players:</label>
      <input type="number" name="playercount" bind:value={$state.playercount} />
    </div>
    <div class="column column-33">
      <label for="level">They are this level:</label>
      <input type="number" name="level" bind:value={$state.level} />
    </div>
    <div class="column column-33">
      <label for="battlecount">I'll be running this many battles today:</label>
      <input type="number" name="battlecount" bind:value={$state.battlecount} />
    </div>
  </div>

  <h2>Results</h2>
  <p>My MEQ budget is: <strong>NNN</strong></p>

  <table>
    <thead>
      <tr>
        <th>Monster level</th>
        <th>Standard/5 mooks</th>
        <th>Elite/7-8 mooks</th>
        <th>2x/large/10 mooks</th>
        <th>3x/huge/15 mooks</th>
      </tr>
    </thead>
    <tbody />
  </table>
</main>
