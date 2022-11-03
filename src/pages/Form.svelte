<script>
  import axios from "axios"
  import Successmsg from "../Components/Successmsg.svelte"

  let Flightnumber, Destination
  let selfCheckin = []

  let success = false
  let move = false
  let fields = {
    Passengername: "",
    Phonenumber: "",
    Email: "",
  }
  let error = { Passengername: "", Phonenumber: "", Email: "" }
  let valid = false

  $: if (Flightnumber == "AI 126") {
    Destination = "Air India’s flight from Chicago to Delhi"
  } else if (Flightnumber == "UA 867") {
    Destination = "United Airlines’ flight from San Francisco to Delhi"
  } else if (Flightnumber == "AA 292") {
    Destination = "American Airlines’ flight from New York to New Delhi"
  } else if (Flightnumber == "SG 4001") {
    Destination = "SpiceJet’s flight from Hyderabad to Goa"
  }

  const adddata = async () => {
    valid = true
    if (fields.Passengername == "") {
      error.Passengername = "Passengername can't be empty"
      valid = false
    } else {
      error.Passengername = ""
    }
    if (fields.Passengername != "") {
      if (fields.Passengername.trim().length < 6) {
        error.Passengername = "Passenger name must be 6 characters long"
        valid = false
      } else {
        error.Passengername = ""
      }
    }
    const ref = /^\(?([0-9]{3})\)?[-. ]?([0-9]{3})[-. ]?([0-9]{4})$/g
    const result = fields.Phonenumber.match(ref)
    if (fields.Phonenumber == "") {
      error.Phonenumber = "Phone number can't be empty"
      valid = false
    } else if (!result) {
      error.Phonenumber = "Please enter correct Format"
      valid = false
    } else {
      error.Phonenumber = ""
    }

    const mail = /\S+@\S+\.\S+/g
    const result1 = mail.test(fields.Email)
    if (fields.Email == "") {
      error.Email = "Email can't be empty"
      valid = false
    } else if (!result1) {
      error.Email = "Please enter valid mail id"
      valid = false
    } else {
      error.Email = ""
    }
    if (valid) {
      move = true
      const sample = {
        Passengername: fields.Passengername,
        Phonenumber: fields.Phonenumber,
        Email: fields.Email,
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
      move = false
      success = true
      ;(fields.Passengername = ""),
        (fields.Phonenumber = ""),
        (fields.Email = ""),
        (Flightnumber = ""),
        (Destination = "")
    }
  }
</script>

<div class="px-10 pb-28 pt-12 lg:pt-10 lg:pb-32 ">
  <div class="w-full lg:w-2/5">
    <form
      on:submit|preventDefault={adddata}
      class="mt-7 flex w-full flex-col items-center rounded-lg bg-blue-200 py-10 shadow-lg">
      <h1 class=" text-3xl font-bold">Passenger Details</h1>
      <input
        bind:value={fields.Passengername}
        type="text"
        class="mt-7 w-3/4 rounded border border-gray-300 py-1 px-3 text-xl leading-8 outline-none transition-colors duration-200 ease-in-out placeholder:text-base placeholder:font-semibold placeholder:text-slate-600 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
        placeholder="Passengername" />

      <div class="text-base font-semibold  text-red-500 md:text-xl">
        {error.Passengername}
      </div>

      <input
        bind:value={fields.Phonenumber}
        type="text"
        class="mt-7 w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-xl leading-8  outline-none transition-colors duration-200 ease-in-out placeholder:text-base placeholder:font-semibold placeholder:text-slate-600 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
        placeholder="Phonenumber" />
      <div class="text-base font-semibold  text-red-500 md:text-xl">
        {error.Phonenumber}
      </div>
      <input
        bind:value={fields.Email}
        type="text"
        class="mt-7 w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-xl leading-8 outline-none transition-colors duration-200 ease-in-out placeholder:text-base placeholder:font-semibold placeholder:text-slate-600 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
        placeholder="Email" />
      <div class="text-base font-semibold text-red-500 md:text-xl">
        {error.Email}
      </div>
      <select
        bind:value={Flightnumber}
        class="mt-7 w-3/4 rounded border border-gray-300 bg-white py-2 px-3 text-base font-semibold leading-8 text-slate-600 outline-none transition-colors duration-200 ease-in-out placeholder:text-base placeholder:font-semibold placeholder:text-slate-600 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200">
        <option value="">Flightnumber</option>
        <option value="AI 126">AI 126</option>
        <option value="UA 867">UA 867</option>
        <option value="AA 292">AA 292</option>
        <option value="SG 4001">SG 4001</option>
      </select>
      <input
        bind:value={Destination}
        type="text"
        class="mt-7 w-3/4 rounded border border-gray-300 bg-white py-1 px-3 text-xl leading-8 outline-none transition-colors duration-200 ease-in-out placeholder:text-base placeholder:font-semibold placeholder:text-slate-600 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200"
        placeholder="Destination" />

      <button
        class=" mx-auto mt-7 flex rounded bg-gradient-to-r from-emerald-400 to-blue-500 py-2 px-8  text-xl  hover:from-pink-500 hover:to-yellow-500 focus:outline-none disabled:cursor-not-allowed">
        {#if move}
          <svg
            role="status"
            class="mr-3 h-5 w-5 animate-spin rounded-full border-4 border-white border-r-indigo-500"
            viewBox="0 0 24 24" />
        {/if}
        Submit</button>
    </form>
    {#if success}
      <Successmsg id={selfCheckin._id} />
    {/if}
  </div>
</div>

<style>
  :global h1 {
    font-family: "Aclonica";
  }
</style>
