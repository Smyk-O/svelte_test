<script>
  import { navigate } from 'svelte-routing';
  import { targetItem } from '../BearStore.js';

  import { Table } from 'sveltestrap';
  export let listItem;

  const setTargetIteId = (item) => {
    targetItem.set(item);
    navigate(`./item/${item.id}`);
  };
</script>

<style>
  tbody tr:hover {
    cursor: pointer;
  }
</style>

<Table class="text-center" hover>
  {#if Object.keys(listItem).length}
    <thead>
      <tr class="row">
        <th class="align-middle col">#</th>
        <th class="align-middle col-8">Name</th>
        <th class="align-middle col">ABV</th>
      </tr>
    </thead>
    <tbody>
      {#each listItem as item}
        <tr
          class="row"
          on:click={setTargetIteId(item)}>
          <th class="align-middle col" scope="row">{item.id}</th>
          <td class="align-middle col-8">{item.name}</td>
          <td class="align-middle col">{item.abv}</td>
        </tr>
      {/each}
    </tbody>
  {:else}
    <tr class="row">
      <th class="align-middle col-12" scope="row">
        По вашему запросу ничего не найдено
      </th>
    </tr>
  {/if}
</Table>
