<script lang="ts">
  import Pre from "../components/Pre.svelte";
  import { from, fromEvent, Observable } from "rxjs";
  import { debounceTime, map } from "rxjs/operators";
  import { onMount } from "svelte";
  let textInput = null;

  let obs: Observable<any> = null;

  onMount((_) => {
    obs = fromEvent(textInput, "keyup").pipe(
      debounceTime(500),
      map((e: any) => e.target.value)
    );

    obs.subscribe((t) => console.log(t));
  });
</script>

<div class="card">
  <div class="card-header">Card</div>

  <div class="card-body">
    <input type="text" bind:this={textInput} />

    {#if $obs}
      <div>value: {$obs}</div>
    {/if}
  </div>
</div>
