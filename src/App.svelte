<script lang="ts">
  import { derived, writable } from "svelte/store";

  const state = writable({
    playercount: 3,
    level: 1,
    battlecount: 4,
  });

  const MeqBudget = derived(
    state,
    ($state) => [0, 1, 2, 3, 5, 7, 9, 11][$state.playercount]
  );

  const parLevel = derived(state, ({ level, battlecount }) => {
    const base = level < 5 ? level : level < 8 ? level + 1 : level + 2;
    return battlecount === 3 ? base + 1 : base;
  });
</script>

<main class="container">
  <h1>13th Age Battle Calculator</h1>

  <div class="row">
    <div class="column column-33">
      <label for="playercount">I have this many players:</label>
      {$state.playercount} <input type=range min=1 max=7 bind:value={$state.playercount} />
    </div>
    <div class="column column-33">
      <label for="level">They are this level:</label>
      {$state.level} <input type=range min=1 max=10 bind:value={$state.level} />
    </div>
    <div class="column column-33">
      <label for="battlecount">I'll be running this many battles today:</label>
      3 <input type=range min=3 max=4 bind:value={$state.battlecount} /> 4
    </div>
  </div>

  <h2>Results</h2>
  <p>My budget is <strong>{$MeqBudget} MEQ.</strong></p>

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
    <tbody>
      <tr>
        <td>{$parLevel - 2}</td>
        <td>0.5</td>
        <td>0.7</td>
        <td>1</td>
        <td>1.5</td>
      </tr>
      <tr>
        <td>{$parLevel - 1}</td>
        <td>0.7</td>
        <td>1</td>
        <td>1.5</td>
        <td>2</td>
      </tr>
      <tr>
        <td><strong>{$parLevel}</strong></td>
        <td><strong>1</strong></td>
        <td><strong>1.5</strong></td>
        <td><strong>2</strong></td>
        <td><strong>3</strong></td>
      </tr>
      <tr>
        <td>{$parLevel + 1}</td>
        <td>1.5</td>
        <td>2*</td>
        <td>3*</td>
        <td>4*</td>
      </tr>
      <tr>
        <td>{$parLevel + 2}</td>
        <td>2*</td>
        <td>3**</td>
        <td>4**</td>
        <td>6**</td>
      </tr>
    </tbody>
  </table>

  <p>
    * Be careful. A monster like this might pack an uncomfortable amount of
    damage into a single swing.
  </p>
  <p>
    ** Probably a mistake to build a battle around monsters that dish out damage
    like these do.
  </p>
</main>
