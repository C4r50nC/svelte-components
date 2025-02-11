<script>
  import Product from './Product.svelte';
  import Modal from './Modal.svelte';

  let products = [
    {
      id: 'p1',
      title: 'A Book',
      price: 9.99,
    },
  ];

  function addToCart(event) {
    console.log(event.detail);
  }

  function deleteProduct(event) {
    console.log(event.detail);
  }
</script>

{#each products as product}
  <!-- Pass in arguments (id, title, and price) using spread operator. Parameter names have to match exactly. -->
  <!-- Parameters that does not exist (id) in the component can be passed in but cannot be used. -->
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}

<Modal>
  <h1>Hello!</h1>
  <p>This works!</p>
</Modal>
