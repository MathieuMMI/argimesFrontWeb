<script>
import Circle from '../icons/circle.svelte'
let name = '';
let age = '';
let email = '';
let errorMessage = '';
function isValidEmail(email) {
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailPattern.test(email);
}
async function handleSubmit() {
  try {
    // Réinitialiser le message d'erreur
    errorMessage = '';
    if (!isValidEmail(email)) {
      throw new Error('Email invalide');
    }
    const response = await fetch('http://localhost:9000/signup', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ name, age, email })
    });
    if (!response.ok) {
      throw new Error('Erreur lors de l\'inscription');
    }
    // Afficher un message de succès
    errorMessage = 'Inscription réussie !';
    // Réinitialiser les champs du formulaire après l'inscription réussie
    name = '';
    age = '';
    email = '';
  } catch (error) {
    console.error(error);
    // Afficher le message d'erreur
    errorMessage = error.message;
  }
}

let isPurple = false; // Variable pour suivre l'état du bouton

function changeColor() {
  isPurple = !isPurple; // Inversion de la valeur de la variable
}
</script>

<style>
  /* Style pour le formulaire lorsqu'il est en mode noir */
  .form-black {
    color: black;
    background-color: black;
  }
</style>

<div class="flex justify-center items-center">
  <!-- Utilisation d'une classe dynamique -->
  <button on:click={changeColor} class="bg-white hover:bg-gray-100 text-black font-bold py-2 px-4 rounded-lg shadow-lg md:py-3 md:px-6 lg:text-xl lg:py-4 lg:px-8 flex items-center">
    <span class="mr-2">Je veux en savoir plus</span>
    <Circle fillColor={isPurple ? 'purple' : 'black'} /> <!-- Utilisation de l'opérateur ternaire pour choisir la couleur -->
  </button>
</div>

<form class="max-w-sm mx-auto mt-8 p-8 bg-purple-600 rounded-lg shadow-lg" class:form-black={!isPurple} on:submit|preventDefault={handleSubmit}>
  <!-- Utilisation de la classe dynamique -->
  <label class="block text-white mb-4" class:form-black={!isPurple}>
    Nom :
    <input class="block text-purple-600 w-full mt-1 rounded-md px-3 py-2 bg-white" type="text" bind:value={name} class:form-black={!isPurple} />
  </label>
  <label class="block text-white mb-4" class:form-black={!isPurple}>
    Âge :
    <input class="block text-purple-600 w-full mt-1 rounded-md px-3 py-2 bg-white" type="number" inputmode="numeric" bind:value={age} class:form-black={!isPurple} style="-webkit-appearance: none; -moz-appearance: textfield;" />
  </label>
  <label class="block text-white mb-4" class:form-black={!isPurple}>
    Email :
    <input class="block text-purple-600 w-full mt-1 rounded-md px-3 py-2 bg-white" type="email" bind:value={email} class:form-black={!isPurple} />
  </label>
  <button class="block w-full bg-white text-purple-600 py-2 px-4 rounded-md hover:bg-purple-400 hover:text-white" type="submit" class:form-black={!isPurple}>S'inscrire</button>
  {#if errorMessage}
    <p class="mt-4 text-red-500">{errorMessage}</p>
  {/if}
</form>
