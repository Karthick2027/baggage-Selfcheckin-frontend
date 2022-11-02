<script>
  import axios from "axios"
  import { onMount } from "svelte"
  let alldetail = []

  onMount(async () => {
    const { data } = await axios.get("http://localhost:7000/api/checkin")
    alldetail = data
  })
</script>

<div class="flex p-10">
  <div class="object-cover object-center lg:w-2/5">
    <img
      class="hidden p-4 lg:block"
      src="https://thumbs.dreamstime.com/b/baggage-claim-airport-terminal-suitcases-luggage-conveyor-belt-d-illustration-155582239.jpg"
      alt="" />
  </div>

  <div class="flex w-full  flex-col gap-5 p-4 lg:w-3/5">
    <div
      class="flex items-center justify-center gap-5 rounded-lg bg-slate-300 p-2">
      <div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.5em"
          height="1.5em"
          preserveAspectRatio="xMidYMid meet"
          viewBox="0 0 15 15">
          <path
            fill="lightgreen"
            fill-rule="evenodd"
            d="M0 7.5a7.5 7.5 0 1 1 15 0a7.5 7.5 0 0 1-15 0Zm7.072 3.21l4.318-5.398l-.78-.624l-3.682 4.601L4.32 7.116l-.64.768l3.392 2.827Z"
            clip-rule="evenodd" />
        </svg>
      </div>
      <h1 class="text-base font-semibold  md:text-xl">
        Below are the Respective <strong class="text-red-500"
          >Counternumber</strong>
        and their Respective
        <strong class="text-red-500">baggage id's</strong>.....
      </h1>
    </div>

    {#each alldetail as alldetails}
      <div
        class="flex overflow-hidden rounded-lg border-2 border-slate-200 bg-slate-300">
        <div class="flex  w-1/4 items-center justify-center bg-green-500">
          <h1 class="text-2xl font-bold text-white">
            {alldetails.Counternumber}
          </h1>
        </div>
        <div class="flex w-3/4 px-5 md:py-2">
          <h1 class=" text-base font-semibold md:text-xl">
            Your Id is : {alldetails._id}
          </h1>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  img {
    width: 1000px;
    height: 600px;
  }

  h1 {
    font-family: "Aclonica";
  }
</style>
