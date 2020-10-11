<script>
  import { Button } from 'sveltestrap';
  export let page;
  export let per_page;
  export let listItemLenght;
  export let switchPage;
</script>

<div ariaLabel="Page navigation example">
  <Button disabled={page === 1} previous on:click={switchPage(page - 1)}>
    {@html '<'}
  </Button>
  <Button
    disabled={listItemLenght < per_page}
    next
    on:click={switchPage(page + 1)}>
    {@html '>'}
  </Button>
</div>
