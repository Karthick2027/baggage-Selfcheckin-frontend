<script>
  import CheckoutPage from "./components/CheckoutPage.svelte"
  import Form from "./components/Form.svelte"

  let hidden = false

  const Checkin = () => {
    hidden = false
  }
  const CheckOut = () => {
    hidden = true
  }
</script>

<main class="h-screen w-screen bg-slate-100 bg-gradient-to-r">
  <!-- <img src="https://wallpaper.dog/large/10792408.jpg" alt="" /> -->
  <div class=" bg-blue-500 p-3 px-10 pb-2">
    <nav class=" flex gap-10">
      <button on:click={Checkin} class="text-xl font-semibold text-white"
        >Checkin</button>
      <button on:click={CheckOut} class=" text-xl font-semibold text-white"
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
</style>
