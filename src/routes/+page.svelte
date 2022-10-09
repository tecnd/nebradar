<script lang="ts">
  import StyledTd from "./components/styled-td.svelte";
  import StyledTh from "./components/styled-th.svelte";
  function clamp(x: number, min: number, max: number): number {
    if (x < min) return min;
    if (x > max) return max;
    return x;
  }
  let slider: number = 7000;
  $: slider = clamp(slider, 0, 10000);
  let maybe: string;
  $: maybe = slider < 5000 ? "yep" : "nope";
  const shipList = [
    { name: "Sprinter", rcs: 3000 },
    { name: "Raines", rcs: 4000 },
  ];
  let selectedRcs: number;
  let customRcs: number = 1000;
  $: customRcs = customRcs > 0 ? customRcs : 0;
  let targetRcs: number;
  $: targetRcs = selectedRcs === -1 ? customRcs : selectedRcs;
</script>

<div class="mx-auto flex flex-col items-center">
  <h1 class="text-3xl font-bold underline">Welcome to SvelteKit</h1>
  <p>
    Visit <a
      href="https://kit.svelte.dev"
      class="text-blue-400 underline hover:text-blue-600">kit.svelte.dev</a
    > to read the documentation
  </p>
  <select bind:value={selectedRcs} class="rounded outline outline-1">
    {#each shipList as ship}
      <option value={ship.rcs}>{`${ship.name} (${ship.rcs})`}</option>
    {/each}
    <option value={-1}>Custom</option>
  </select>
  {#if selectedRcs === -1}
    <input
      type="number"
      min="0"
      bind:value={customRcs}
      class="rounded outline outline-1"
    />
  {/if}
  <input
    type="range"
    min="0"
    max="10000"
    step="10"
    bind:value={slider}
    class="w-1/2"
  />
  <p>Slider is at:</p>
  <input
    type="number"
    min="0"
    max="10000"
    bind:value={slider}
    class="rounded outline outline-1"
  />
  <p>{maybe}</p>
  <p>Target RCS: {targetRcs}</p>
  <table class="table-auto border-collapse border">
    <thead>
      <tr>
        <StyledTh>Radar</StyledTh>
        <StyledTh>Can See?</StyledTh>
        <StyledTh>Can BRN?</StyledTh>
        <StyledTh>Can Lock?</StyledTh>
      </tr>
    </thead>
    <tbody>
      <tr>
        <StyledTd>Frontline</StyledTd>
        <StyledTd>temp</StyledTd>
        <StyledTd>temp</StyledTd>
        <StyledTd>N/A</StyledTd>
      </tr>
      <tr>
        <StyledTd>Parallax</StyledTd>
        <StyledTd>temp</StyledTd>
        <StyledTd>temp</StyledTd>
        <StyledTd>temp</StyledTd>
      </tr>
      <tr>
        <StyledTd>Spyglass</StyledTd>
        <StyledTd>temp</StyledTd>
        <StyledTd>N/A</StyledTd>
        <StyledTd>N/A</StyledTd>
      </tr>
      <tr>
        <StyledTd>Bullseye</StyledTd>
        <StyledTd>N/A</StyledTd>
        <StyledTd>N/A</StyledTd>
        <StyledTd>temp</StyledTd>
      </tr>
    </tbody>
  </table>
</div>
