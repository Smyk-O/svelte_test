<script>
  import { Col, Media, Button, Table } from 'sveltestrap';
  import { Link } from 'svelte-routing';
  import { targetItem } from '../BearStore.js';

  let item = [];

  targetItem.subscribe((value) => {
    item = value;
  });
</script>

<style>
  img {
    max-width: 250px;
    max-height: 250px;
    width: 100%;
    object-fit: contain;
  }
</style>

<svelte:head>
  <title>{item.name}</title>
  <meta name="description" content={item.description} />
</svelte:head>

<div class="row">
  <Col sm="12" md={{ size: 6, offset: 3 }}>
    <Link to="./">
      <Button>Go back to the list</Button>
    </Link>
    <Media class="mt-5">
      <img src={item.image_url} alt={item.name} class="left" />
      <div class="body">
        <h1 heading>{item.name}</h1>
        <h6>{item.tagline}</h6>
        {item.description}
        <Table>
          <tbody>
            <tr>
              <th>first brewed</th>
              <td>{item.first_brewed}</td>
            </tr>
            <tr>
              <th>abv</th>
              <td>{item.abv}</td>
            </tr>
            <tr>
              <th>food pairing</th>
              <td>{item.food_pairing}</td>
            </tr>
          </tbody>
        </Table>
      </div>
    </Media>
  </Col>
</div>
