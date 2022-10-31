<script>
  import Checkout from "./components/Checkout.svelte"
  import Form from "./components/Form.svelte"

  let hidden = false

  const Checkin = () => {
    hidden = false
  }
  const CheckOut = () => {
    hidden = true
  }
</script>

<main class="h-screen w-screen bg-slate-100">
  <div class=" bg-blue-500 p-3 px-10">
    <nav class=" flex gap-10">
      <button on:click={Checkin} class="text-xl font-semibold text-white"
        >Checkin</button>
      <button on:click={CheckOut} class=" text-xl font-semibold text-white"
        >CheckOut</button>
    </nav>
  </div>

  {#if hidden}
    <Checkout />
  {:else}
    <Form />
  {/if}
</main>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>
