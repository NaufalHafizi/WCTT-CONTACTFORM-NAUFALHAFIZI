<script>
  let name = "";
  let email = "";
  let description = "";
  let hasBeenClicked = false;
  let showLoading = false;
  let apiMessage = '';
  let apiIsFailed = false;

  function validateEmail(email) {
    var emailRegEx = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;  
    return emailRegEx.test(String(email).toLowerCase());
  }

  async function handleSubmission() {
    hasBeenClicked = true;

    if (isValidName && isValidEmail && isValidDescription) {

      showLoading = true;

      const res = await fetch('http://localhost:8080/users', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json'
        },
        body: JSON.stringify({
            "name": name,
            "email": email,
            "description": description
        })
      })
      .then(async response => {
        if(response.status != 201){
          apiMessage = 'Something went wrong happened. Please try again!';
          apiIsFailed = true;
        } else {
          apiMessage = 'The form has been successfully submitted';
          apiIsFailed = false;
        }
      })
      .catch(err => {
        apiMessage = 'Something went wrong happened. Please try again!';
        apiIsFailed = true;
      })

      showLoading = false;
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

          {#if apiMessage.length > 0}
          <div class="{apiIsFailed ? 'bg-red-100 border-red-400 text-red-700' : 'bg-blue-100 border-blue-400 text-blue-700'} border px-4 py-3 rounded relative mb-5" role="alert">
            <strong class="font-bold">{apiIsFailed ? 'Oops!' : 'Thank You!'}</strong>
            <span class="block sm:inline">{apiMessage}</span>
          </div>
          {/if}
          
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
          {#if hasBeenClicked && !isValidDescription} 
            <p class="validation-error">Please enter a description</p>
          {/if}
          
          {#if !showLoading}
          <div class="flex justify-center">
            <button on:click={handleSubmission} class="mt-4 bg-indigo-500 text-white py-2 px-6 rounded-lg">Submit</button>
          </div>
          {:else}
          <div class="flex justify-center">
            <svg role="status" class="mt-5 w-8 h-8 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-indigo-400" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
              <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
            </svg>
          </div>
          {/if}
        </div>
      </div>
    </div>
  </div>
</main>