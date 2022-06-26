<script>
  let name = "";
  let email = "";
  let description = "";
  let hasBeenClicked = false;

  function validateEmail(email) {
    var emailRegEx = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;  
    return emailRegEx.test(String(email).toLowerCase());
  }

  function handleSubmission() {
    hasBeenClicked = true;

    if (isValidName && isValidEmail && isValidDescription) {
      // Send data somewhere
      alert("submitted");
    }
  }

  $: isValidName = name.length > 0;
  $: isValidDescription = description.length > 0;
  $: isValidEmail = validateEmail(email);
</script>

<style>
  .validation-error {
    color: red;
    margin-top: 5px;
  }
</style>

<main>
  <div class="min-h-screen bg-gray-100 text-gray-800 antialiased px-4 py-6 flex flex-col justify-center sm:py-12">
    <div class="relative py-3 sm:max-w-xl mx-auto text-center">
      <span class="text-2xl font-light">Contact Form</span>
      <div class="relative mt-4 bg-white shadow-md sm:rounded-lg text-left">
        <div class="h-2 bg-indigo-400 rounded-t-md"></div>
        <div class="py-6 px-8">
          
          <!-- svelte-ignore a11y-label-has-associated-control -->
          <label class="block font-semibold">Name<label>
          <input type="text" bind:value={name} placeholder="Name" class="border w-full h-5 px-3 py-5 mt-2 hover:outline-none focus:outline-none focus:ring-1 focus:ring-indigo-600 rounded-md">
          {#if hasBeenClicked && !isValidName} 
            <p class="validation-error">Please enter a name</p>
          {/if}
          
          <label class="block pt-4 font-semibold">Email<label>
          <input type="text" bind:value={email} placeholder="Email" class="border w-full h-5 px-3 py-5 mt-2 hover:outline-none focus:outline-none focus:ring-1 focus:ring-indigo-600 rounded-md">
          {#if hasBeenClicked && !isValidEmail} 
            <p class="validation-error">Invalid email</p>
          {/if}
          
          <label class="block pt-4 font-semibold">Description<label>
          <textarea bind:value={description} placeholder="Description" class="border block w-full px-3 py-1.5 mt-2 hover:outline-none focus:outline-none focus:ring-1 focus:ring-indigo-600 rounded-md"></textarea>
          {#if hasBeenClicked && !isValidName} 
            <p class="validation-error">Please enter a description</p>
          {/if}
          
          <div class="flex justify-center">
            <button on:click={handleSubmission} class="mt-4 bg-indigo-500 text-white py-2 px-6 rounded-lg">Submit</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>