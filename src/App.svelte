<script>
  import CheckoutPage from "./pages/CheckoutPage.svelte"
  import Form from "./pages/Form.svelte"

  let hidden = false

  const Checkin = () => {
    hidden = false
  }
  const CheckOut = () => {
    hidden = true
  }
</script>

<!--  -->
<main
  class="background h-full w-full bg-slate-300 bg-cover bg-fixed bg-center ">
  <div
    class="bg-gradient-to-rp-3 flex items-center gap-5 bg-gradient-to-r from-sky-400 to-blue-500 px-5 opacity-75 shadow-lg">
    <div>
      <img
        src="https://upload.wikimedia.org/wikipedia/commons/7/75/Plane1120.png"
        class="h-14 w-14 rounded"
        alt="" />
    </div>
    <h2 class=" text-2xl font-semibold md:text-3xl ">Self Checkin</h2>
    <nav class="ml-auto flex gap-10">
      <button
        on:click={Checkin}
        class="cursor-pointer text-xl font-semibold hover:underline"
        >Checkin</button>
      <button
        on:click={CheckOut}
        class="cursor-pointer text-xl font-semibold hover:underline"
        >CheckOut</button>
    </nav>
  </div>

  {#if hidden}
    <CheckoutPage />
  {:else}
    <Form />
  {/if}
</main>

<style global lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;

  button {
    font-family: "Aclonica";
  }
  h2 {
    font-family: "Orelega One";
  }
  .background {
    background-image: url(https://upload.wikimedia.org/wikipedia/commons/7/75/Plane1120.png);
  }
</style>
