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

  let showModal = false;

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

<button on:click={() => (showModal = true)}>Show Modal</button>

{#if showModal}
  <Modal
    on:cancel={() => (showModal = false)}
    on:close={() => (showModal = false)}
  >
    <h1 slot="header">Hello!</h1>
    <p>This works!</p>
    <!-- Below overrides the default tags in footer slot -->
    <button slot="footer" on:click={() => (showModal = false)}>Confirm</button>
  </Modal>
{/if}
