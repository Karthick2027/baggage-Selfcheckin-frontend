<script>
  import axios from "axios"
  import { onMount } from "svelte"
  let alldetail = []

  onMount(async () => {
    const { data } = await axios.get("http://localhost:7000/api/checkin")
    alldetail = data
  })
  const disCountnum = (alldetail) => {
    Counternum = false
    console.log(alldetail._id)
  }
</script>

<div class="flex">
  <div class=" w-2/5 object-cover object-center">
    <img
      class="h-full w-full"
      src="https://st.focusedcollection.com/18590116/i/1800/focused_227244226-stock-photo-luggage-baggage-carousel-airport-terminal.jpg"
      alt="" />
  </div>

  <div class="flex w-full flex-col gap-5 p-4  lg:w-3/5">
    {#each alldetail as alldetails}
      <div
        class="flex overflow-hidden rounded-lg border-2 border-slate-200 bg-slate-200">
        <div class="flex  w-1/5 items-center justify-center bg-green-500">
          <h1 class="text-2xl font-bold text-white">
            {alldetails.Counternumber}
          </h1>
        </div>
        <div class="flex w-4/5 px-5 py-2">
          <h1 class=" text-2xl font-semibold ">
            Your Id is : {alldetails._id}
          </h1>
        </div>
      </div>
    {/each}
  </div>
</div>
