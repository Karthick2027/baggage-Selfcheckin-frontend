<script>
  export let id
</script>

<div class=" mt-5 w-full rounded-lg bg-emerald-200">
  <div class="mx-5 flex  items-center justify-center">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-8 w-8"
      preserveAspectRatio="xMidYMid meet"
      viewBox="0 0 15 15">
      <path
        fill="green"
        fill-rule="evenodd"
        d="M0 7.5a7.5 7.5 0 1 1 15 0a7.5 7.5 0 0 1-15 0Zm7.072 3.21l4.318-5.398l-.78-.624l-3.682 4.601L4.32 7.116l-.64.768l3.392 2.827Z"
        clip-rule="evenodd" />
    </svg>
    <div>
      <h1 class="mx-5 p-4 text-lg font-semibold text-green-900 ">
        Succesfully checked in, and your id is: <strong>{id}</strong>
      </h1>
    </div>
  </div>
</div>
