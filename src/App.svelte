<!-- App.svelte -->
<script>
  import { Router, Route } from 'svelte-routing';
  import List from './routes/List.svelte';
  import Item from './routes/Item.svelte';
  export let url = '';
  // export let basepath = '/svelte_test/';
</script>

<Router {url} >
  <div>
    <Route path="/" component={List} />
    <Route path="item/:id" component={Item} />
  </div>
</Router>
