<script>
  import { tick } from 'svelte';
  import Product from './Product.svelte';
  import Modal from './Modal.svelte';

  let products = [
    {
      id: 'p1',
      title: 'A Book',
      price: 9.99,
    },
  ];

  let text = 'This is some dummy text!';

  let showModal = false;

  function addToCart(event) {
    console.log(event.detail);
  }

  function deleteProduct(event) {
    console.log(event.detail);
  }

  function transform(event) {
    if (event.key !== 'Tab') {
      return;
    }
    event.preventDefault();

    const selectionStart = event.target.selectionStart;
    const selectionEnd = event.target.selectionEnd;
    const value = event.target.value;

    changeSelectionToUpperCase();

    restoreTextSelection();

    function changeSelectionToUpperCase() {
      text =
        value.slice(0, selectionStart) +
        value.slice(selectionStart, selectionEnd).toUpperCase() +
        value.slice(selectionEnd);
    }

    function restoreTextSelection() {
      // When the DOM updates (triggered by the value change in text), the selection will be lost
      // Use tick().then() to execute code after the current DOM update finishes to restore selection
      tick().then(() => {
        event.target.selectionStart = selectionStart;
        event.target.selectionEnd = selectionEnd;
      });
    }
  }
</script>

{#each products as product}
  <!-- Pass in arguments (id, title, and price) using spread operator. Parameter names have to match exactly. -->
  <!-- Parameters that does not exist (id) in the component can be passed in but cannot be used. -->
  <Product {...product} on:add-to-cart={addToCart} on:delete={deleteProduct} />
{/each}

<button on:click={() => (showModal = true)}>Show Modal</button>

{#if showModal}
  <!-- closeable is the defined variable name in App.svelte with received value  -->
  <!-- didAgree is the custom attribute name for passing in data from child component (Modal.svelte) -->
  <Modal
    on:cancel={() => (showModal = false)}
    on:close={() => (showModal = false)}
    let:didAgree={closeable}
  >
    <h1 slot="header">Hello!</h1>
    <p>This works!</p>
    <!-- Below overrides the default tags in footer slot -->
    <button
      slot="footer"
      on:click={() => (showModal = false)}
      disabled={!closeable}>Confirm</button
    >
  </Modal>
{/if}

<textarea rows="5" on:keydown={transform}>{text}</textarea>
