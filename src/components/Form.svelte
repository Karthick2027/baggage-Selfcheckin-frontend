<script>
  import axios from "axios"
  let Passengername, Phonenumber, Email, Flightnumber, Destination
  let selfCheckin = []
  let success = false
  let move = false
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
    move = true
    success = true
    ;(Passengername = ""),
      (Phonenumber = ""),
      (Email = ""),
      (Flightnumber = ""),
      (Destination = "")
  }
</script>

<div class="absolute inset-5 px-10 pt-14">
  <form
    on:submit|preventDefault={adddata}
    class=" mx-auto flex w-full flex-col items-center gap-10 rounded-lg bg-blue-100 p-10 shadow-lg  lg:w-1/2">
    <h1 class="text-3xl font-bold">Passenger Details</h1>
    <input
      bind:value={Passengername}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Passengername"
      required />

    <input
      bind:value={Phonenumber}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Phonenumber"
      required />
    <input
      bind:value={Email}
      type="text"
      class="w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
      placeholder="Email"
      required />
    <select
      bind:value={Flightnumber}
      class="w-3/4 rounded border border-gray-300 bg-white py-2 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200">
      <option value="">Flightnumber</option>
      <option value="AI 126">AI 126</option>
      <option value="UA 867">UA 867</option>
      <option value="AA 292">AA 292</option>
      <option value="SG 4001">SG 4001</option>
    </select>

    <select
      bind:value={Destination}
      class="w-3/4 rounded border border-gray-300 bg-white py-2 px-3 text-base leading-8 text-gray-700 outline-none transition-colors duration-200 ease-in-out focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200">
      <option value="">Destination</option>
      <option value="Air India’s flight from Chicago to Delhi"
        >Air India’s flight from Chicago to Delhi</option>
      <option value="United Airlines’ flight from San Francisco to Delhi"
        >United Airlines’ flight from San Francisco to Delhi</option>
      <option value="American Airlines’ flight from New York to New Delhi"
        >American Airlines’ flight from New York to New Delhi</option>
      <option value="SpiceJet’s flight from Hyderabad to Goa"
        >SpiceJet’s flight from Hyderabad to Goa</option>
    </select>
    <button
      class="mx-auto flex rounded border-0 bg-indigo-500 py-2 px-8 text-lg text-white hover:bg-indigo-600 focus:outline-none">
      {#if move}
        <svg
          role="status"
          class="mr-3 h-5 w-5 animate-spin rounded-full border-4 border-white border-r-indigo-500"
          viewBox="0 0 24 24" />
      {/if}
      Submit</button>
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
