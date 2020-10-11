<script>
  // import { onMount } from 'svelte';
  import { Row, Col, FormGroup, Input } from 'sveltestrap';

  import List from '../component/ItemList.svelte';
  import Pagination from '../component/Pagination.svelte';

  let apiUrl = 'https://api.punkapi.com/v2/';
  let apiListParams = {
    page: 1,
    per_page: 26,
  };
  export let listItem = {};
  let searchText = '';
  let searchParam = '';

  let apiGetList = (page, per_page, search_param = '') => {
    return async function () {
      let res = await fetch(
        apiUrl + `beers?page=${page}&per_page=${per_page}${search_param}`
      );
      listItem = await res.json();
    };
  };

  // onMount(apiGetList(apiListParams.page, apiListParams.per_page));

  const switchPage = (newPage) => {
    apiListParams.page = newPage;
    apiGetList(apiListParams.page, apiListParams.per_page, searchParam)();
  };

  const search = () => {
    apiListParams.page = 1;
    searchText
      ? (searchParam = `&beer_name=${searchText}`.replace(/ /g, '_'))
      : (searchParam = '');
    apiGetList(apiListParams.page, apiListParams.per_page, searchParam)();
  };

  $: if (searchText.length >= 0) {
    search();
  }
</script>

<svelte:head>
  <title>Home</title>
</svelte:head>

<h1 class="text-primary text-center display-2 font-weight-bolder">Beer list</h1>

<Row>
  <Col sm="12" md={{ size: 6, offset: 3 }}>
    <FormGroup>
      <Input
        type="search"
        name="search"
        id="exampleSearch"
        placeholder="Search by beer name"
        bind:value={searchText} />
    </FormGroup>
    <List {listItem} />
    <Pagination
      page={apiListParams.page}
      per_page={apiListParams.per_page}
      listItemLenght={Object.keys(listItem).length}
      {switchPage} />
  </Col>
</Row>
