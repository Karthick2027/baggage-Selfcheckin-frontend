<script>
  import axios from "axios"
  import { onMount } from "svelte"
  let alldeatil = []
  let Counternum = true

  onMount(async () => {
    const { data } = await axios.get("http://localhost:7000/api/checkin")
    alldeatil = data
  })
  const disCountnum = () => {
    Counternum = false
  }
</script>

<div class="m-10 flex justify-center">
  <div
    class="flex w-full flex-col items-center gap-5 rounded-lg bg-blue-100 p-7 shadow-lg lg:w-1/2">
    {#each alldeatil as alldeatils}
      {#if Counternum}
        <button
          on:click={disCountnum}
          class="text-start text-xl font-bold hover:bg-blue-300 md:text-2xl">
          <strong> Your Id : </strong>
          {alldeatils._id}
        </button>
      {:else}
        <span class=" text-xl font-bold hover:bg-blue-300 md:text-2xl">
          <strong> Your Counter Number : </strong>
          {alldeatils.Counternumber}
        </span>

        <!-- <button class="text-2xl font-bold">
          <strong> Your Id : </strong>{alldeatils._id}</button> -->
      {/if}
    {/each}
  </div>
</div>
