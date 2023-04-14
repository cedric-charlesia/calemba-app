<script setup>
import SubTitle from './components/SubTitle.vue';
</script>

<template>
  <div id="app" class="w-4/5 md:max-w-5xl mx-auto my-4 px-4 py-4 bg-white space-y-4">

    <h1 class="text-2xl font-bold font-poppins">
      Calculer ma capacité d'emprunt
    </h1>

    <form>

      <div class="border-gray-900/10 pb-12">

        <!-- Loaner(s) general details -->

        <SubTitle title="Situation emprunteur(s)" />

        <div class="mt-4 grid grid-cols-1 gap-x-6 gap-y-3 sm:grid-cols-6 lg:grid-cols-12">

          <div class="sm:col-span-3 lg:col-span-4">
            <label for="number-of-loaner" class="block text-sm font-medium leading-6 text-gray-900">Nombre d'adulte(s)
              (2 si couple)</label>
            <div class="mt-2">
              <select id="number-of-loaner" name="number-of-loaner"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-3 lg:max-w-xs sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
                <option value="1">1</option>
                <option value="2">2</option>
              </select>
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-4">
            <label for="number-of-children" class="block text-sm font-medium leading-6 text-gray-900">Nombre d'enfant(s)
              à charge</label>
            <div class="mt-2">
              <select id="number-of-children" name="number-of-children"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:max-w-xs sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
                <option value="6">6</option>
                <option value="7">7</option>
                <option value="8">8</option>
                <option value="9">9</option>
                <option value="10">10</option>
              </select>
            </div>
          </div>

          <!-- Incomes -->

          <SubTitle title="Revenus" />

          <div class="sm:col-span-3 lg:col-span-3 col-start-1">
            <label for="monthly-wage" class="block text-sm font-medium leading-6 text-gray-900">Salaire
              mensuel</label>
            <div class="mt-2">
              <input type="number" name="monthly-wage" id="monthly-wage"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-3">
            <label for="annual-bonus" class="block text-sm font-medium leading-6 text-gray-900">Prime annuelle</label>
            <div class="mt-2">
              <input type="number" name="annual-bonus" id="annual-bonus"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-3">
            <label for="rental-income" class="block text-sm font-medium leading-6 text-gray-900">Revenus locatifs
              mensuels</label>
            <div class="mt-2">
              <input type="number" name="rental-income" id="rental-income"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-3">
            <label for="other-income" class="block text-sm font-medium leading-6 text-gray-900">Autres revenus
              mensuels</label>
            <div class="mt-2">
              <input type="number" name="other-income" id="other-income"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <!-- Expenses -->

          <SubTitle title="Charges" />

          <div class="sm:col-span-3 lg:col-span-3 lg:col-start-1">
            <label for="current-loan" class="block text-sm font-medium leading-6 text-gray-900">Crédit immo.
              mensuel</label>
            <div class="mt-2">
              <input type="number" name="current-loan" id="current-loan"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-3">
            <label for="current-debt" class="block text-sm font-medium leading-6 text-gray-900">Autre crédit
              mensuel</label>
            <div class="mt-2">
              <input type="number" name="current-debt" id="current-debt"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-3">
            <label for="rent" class="block text-sm font-medium leading-6 text-gray-900">Loyer</label>
            <div class="mt-2">
              <input type="number" name="rent" id="rent"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

          <div class="sm:col-span-3 lg:col-span-3">
            <label for="other-expense" class="block text-sm font-medium leading-6 text-gray-900">Autres charges
              mensuelles</label>
            <div class="mt-2">
              <input type="number" name="other-expense" id="other-expense"
                class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            </div>
          </div>

        </div>
      </div>

      <!-- Submit form -->

      <div class="flex items-center justify-end gap-x-3">
        <button type="reset"
          class="text-sm font-semibold leading-6 text-gray-900 px-3 py-2 rounded-md bg-neutral-100">Annuler</button>
        <button type="submit"
          class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Calculer</button>
      </div>

    </form>

    <div
      class="hidden grid grid-cols-1 gap-x-3 gap-y-6 sm:col-span-2 md:grid-cols-2 lg:grid-cols-3 bg-blue-100 px-6 py-6 rounded-md">

      <div class="lg:border-r-2 lg:border-gray-400 px-4">
        <p class="block text-sm font-medium leading-6 text-gray-900 font-bold">Taux d'endettement</p>
        <p class="font-normal">30%</p>
      </div>

      <div class="lg:border-r-2 lg:border-gray-400 px-4">
        <p class="block text-sm font-medium leading-6 text-gray-900 font-bold">Reste à vivre
        </p>
        <p class="font-normal">1400€</p>
      </div>

      <div class="px-4">
        <p class="block text-sm font-medium leading-6 text-gray-900 font-bold">Capacité de remboursement</p>
        <p class="font-normal">474€</p>
      </div>

      <div class="lg:border-r-2 lg:border-gray-400 px-4">
        <p class="block text-sm font-medium leading-6 text-gray-900 font-bold">Apport requis
        </p>
        <p class="font-normal">8000€</p>
      </div>

      <div class="flex gap-2 items-center lg:border-r-2 lg:border-gray-400 px-4">
        <p class="block text-sm font-medium leading-6 text-gray-900 font-bold">J'ai cet apport ?</p>
        <input type="radio" id="yes" name="possible-contribution" checked
          class="block border-0 py-2 px-2 text-indigo-600">
        <label for="yes" class="block text-sm font-medium leading-6 text-gray-900">Oui</label>

        <input type="radio" id="no" name="possible-contribution" class="block border-0 py-2 px-2 text-indigo-600">
        <label for="no" class="block text-sm font-medium leading-6 text-gray-900">Non</label>
      </div>

      <div class="px-4">
        <p class="block text-sm font-medium leading-6 text-gray-900 font-bold">Capacité d'emprunt</p>
        <p class="font-normal">8000€</p>
      </div>

      <div class="px-4">
        <label for="loan-duration" class="block text-sm font-medium leading-6 text-gray-900 font-bold">Durée
          (ans)</label>
        <div class="mt-2">
          <select id="loan-duration" name="loan-duration"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:max-w-xs sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
            <option value="10">10</option>
            <option value="15">15</option>
            <option value="20">20</option>
            <option value="25">25</option>
          </select>
        </div>
      </div>

      <div class="px-4">
        <label for="loan-rate" class="block text-sm font-medium leading-6 text-gray-900 font-bold">Taux (%)</label>
        <div class="mt-2">
          <input type="number" name="loan-rate" id="loan-rate"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
        </div>
      </div>

      <div class="px-4">
        <label for="insurance-rate" class="block text-sm font-medium leading-6 text-gray-900 font-bold">Assurance
          (%)</label>
        <div class="mt-2">
          <input type="number" name="insurance-rate" id="insurance-rate"
            class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
        </div>
      </div>
    </div>

  </div>
</template>
