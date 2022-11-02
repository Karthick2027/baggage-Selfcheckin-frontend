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

<main class="h-screen w-screen bg-gradient-to-r from-sky-200 to-lime-200">
  <!-- <img src="https://wallpaper.dog/large/10792408.jpg" alt="" /> -->
  <div
    class="bg-gradient-to-rp-3 flex items-center gap-5 bg-gradient-to-r from-sky-400 to-blue-500 px-5 py-2.5 shadow-lg">
    <div>
      <img
        src="https://upload.wikimedia.org/wikipedia/commons/7/75/Plane1120.png"
        class="h-10 w-10 rounded"
        alt="" />
    </div>
    <h2 class="  text-3xl font-semibold ">Self Checkin</h2>
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
</style>
