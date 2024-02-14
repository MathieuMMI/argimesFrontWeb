<script setup>
import Footer from "../components/footer.svelte"
import Filter from "../components/sectionFilter.svelte"
import Form from "../components/sectionForm.svelte"
</script>


<div>
    <main class="mb-20">
      <img src="/LogoW.svg" alt="Logo" class="w-[10%] ml-5 mt-5 md:w-[5%]">
      <h1 class="text-white text-center text-3xl md:text-5xl mb-5">Argimes</h1>
      <Filter />
      <Form />
    </main>
    <Footer />
</div>

<style>
/* Importation de la police de caractères Arimo depuis Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Arimo&display=swap');
/* Application de la police de caractères Arimo au titre h1 */
h1 {
  font-family: 'Arimo', sans-serif;
}

p {
    font-family: 'Inter', sans-serif;
}
</style>