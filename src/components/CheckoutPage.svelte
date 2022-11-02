<script>
  import axios from "axios"
  import { onMount } from "svelte"
  import { fly } from "svelte/transition"
  let alldetail = []
  let displayDetails = []
  onMount(async () => {
    const { data } = await axios.get("http://localhost:7000/api/checkin")
    alldetail = data
  })

  const displaydata = async (id) => {
    console.log(id)
    const { data } = await axios.get(`http://localhost:7000/api/checkin/${id}`)

    displayDetails = data
    console.log(displayDetails)
  }
</script>

<!-- bg-[radial-gradient(ellipse_at_bottom,_var(--tw-gradient-stops))] from-amber-200 via-violet-300 to-sky-300 -->
<div class="flex flex-col p-10 lg:flex-row">
  <div class="flex w-full  flex-col gap-5 p-4 lg:w-3/5">
    <div class="flex items-center justify-center gap-5 rounded-lg bg-white p-2">
      <div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="1.5em"
          height="1.5em"
          preserveAspectRatio="xMidYMid meet"
          viewBox="0 0 15 15">
          <path
            fill="green"
            fill-rule="evenodd"
            d="M0 7.5a7.5 7.5 0 1 1 15 0a7.5 7.5 0 0 1-15 0Zm7.072 3.21l4.318-5.398l-.78-.624l-3.682 4.601L4.32 7.116l-.64.768l3.392 2.827Z"
            clip-rule="evenodd" />
        </svg>
      </div>
      <h1 class="text-base font-semibold  md:text-xl">
        Below are the Respective <strong class="text-red-500"
          >Counternumber</strong>
        and their Respective
        <strong class="text-red-500">Baggage Id's</strong>.....
      </h1>
    </div>

    {#each alldetail as alldetails}
      <div
        class="flex overflow-hidden rounded-lg border-2  border-slate-200 bg-white">
        <div class="flex w-1/4 items-center justify-center bg-purple-700">
          <h1 class="text-2xl font-bold text-white">
            {alldetails.Counternumber}
          </h1>
        </div>
        <!-- svelte-ignore missing-declaration -->
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div
          class="flex w-3/4 px-5 md:py-5"
          on:click={displaydata(alldetails._id)}>
          <h1 class=" text-base font-semibold md:text-xl">
            Baggage Id is : {alldetails._id}
          </h1>
        </div>
      </div>
    {/each}
  </div>

  <div class="w-full p-4 lg:w-2/5">
    <div class="height  w-full rounded-lg bg-slate-300 opacity-75 shadow-lg">
      <h1 class="pt-5 text-center text-3xl  font-semibold text-violet-700">
        SUMMARY CARD
      </h1>
      {#each displayDetails as display}
        <div class="flex flex-col space-y-5 p-10">
          <h1 class="text-xl font-semibold">
            Passengername :<strong class=" text-red-700">
              {display.Passengername}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Baggage Id : <strong class=" text-red-700">{display._id}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Counternumber: <strong class=" text-red-700"
              >{display.Counternumber}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Phonenumber : <strong class=" text-red-700"
              >{display.Phonenumber}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Email : <strong class=" text-red-700"> {display.Email}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Flightnumber : <strong class=" text-red-700"
              >{display.Flightnumber}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Destination :<strong class=" text-red-700"
              >{display.Destination}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Time :<strong class=" text-red-700"
              >{new Date(display.Time).toLocaleTimeString()}</strong>
          </h1>
          <h1 class="text-xl font-semibold">
            Date :<strong class=" text-red-700"
              >{new Date(display.Date).toLocaleDateString()}</strong>
          </h1>
        </div>
      {:else}
        <h1
          transition:fly={{ x: 300, duration: 1000 }}
          class="text-2xl font-bold text-center p-10 text-violet-800">
          No Details Available
        </h1>
      {/each}
    </div>
  </div>
</div>

<style>
  h1 {
    font-family: "Aclonica";
  }
  .height {
    height: 38rem;
  }
</style>
