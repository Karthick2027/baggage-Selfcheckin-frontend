<script>
  import axios from "axios"
  let Passengername, Phonenumber, Email, Flightnumber, Destination
  let selfCheckin = []
  let success = false
  const adddata = async () => {
    const sample = {
      Passengername: Passengername,
      Phonenumber: Phonenumber,
      Email: Email,
      Flightnumber: Flightnumber,
      Destination: Destination,
    }
    console.log("b4 data", sample)
    const { data } = await axios.post(
      "http://localhost:7000/api/checkin",
      sample
    )
    console.log("after data", data)
    selfCheckin = data
    success = true
    ;(Passengername = ""),
      (Phonenumber = ""),
      (Email = ""),
      (Flightnumber = ""),
      (Destination = "")
  }
</script>

<div class="px-10 pt-10">
  <form
    on:submit|preventDefault={adddata}
    class=" mx-auto flex w-full flex-col items-center gap-10 rounded-lg bg-blue-200 p-10 shadow-lg  lg:w-1/2">
    <h1 class="text-3xl font-bold">Passenger Details</h1>
    <input
      bind:value={Passengername}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Passengername" />
    <input
      bind:value={Phonenumber}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Phonenumber" />
    <input
      bind:value={Email}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Email" />
    <input
      bind:value={Flightnumber}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Flightnumber" />

    <select
      bind:value={Flightnumber}
      class="w-16 rounded-lg p-2 text-2xl font-bold">
      <option value="+">+</option>
      <option value="-">-</option>
    </select>

    <input
      bind:value={Destination}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Destination" />

    <button
      class="mx-auto flex rounded border-0 bg-indigo-500 py-2 px-8 text-lg text-white hover:bg-indigo-600 focus:outline-none"
      >Submit</button>
  </form>
  {#if success}
    <div class="mx-auto mt-5 w-full rounded-lg bg-green-300 lg:w-1/2">
      <h1 class="mx-5 p-2 text-xl font-bold ">
        Succesfully checked in, and your id is: <strong
          >{selfCheckin._id}</strong>
      </h1>
    </div>
  {/if}
</div>
