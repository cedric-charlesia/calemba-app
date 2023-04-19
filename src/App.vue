<script setup>
import SubTitle from './components/SubTitle.vue'
import NavBar from './components/NavBar.vue'

import { ref } from 'vue'

const showResult = ref(false)
const showInputError = ref(false)
const showDebtError = ref(false)
const showMoneyToLiveError = ref(false)
const showLoanError = ref(false)

const numberOfLoaner = ref('1')
const numberOfChildren = ref('0')
const monthlyWage = ref('')
const annualBonus = ref('')
const rentalIncome = ref('')
const otherIncome = ref('')
const currentLoan = ref('')
const currentDebt = ref('')
const currentRent = ref('')
const otherExpense = ref('')

const moneyToLive = ref('')
const moneyLeft = ref('')
const debtRate = ref('')

const contribution = ref('')
const possibleContribution = ref('yes')

const maxLoanCapacity = ref('')

const loanDurationInYears = ref(20)
const displayLoanRate = ref('')
const displayInsuranceRate = ref(0.25)

const resetResult = () => {
  if (showInputError.value === true) {
    showInputError.value = !showInputError.value
  }

  if (showResult.value === true) {
    showResult.value = !showResult.value

    monthlyWage.value = ''
    annualBonus.value = ''
    rentalIncome.value = ''
    otherIncome.value = ''
    currentLoan.value = ''
    currentDebt.value = ''
    currentRent.value = ''
    otherExpense.value = ''

    moneyToLive.value = ''
    moneyLeft.value = ''
    debtRate.value = ''

    contribution.value = ''
    maxLoanCapacity.value = ''
  }
}

const getMaxLoan = () => {
  if (showInputError.value === false && monthlyWage.value === '' && annualBonus.value === '' && rentalIncome.value === '' && otherIncome.value === '') {
    showInputError.value = true
  }
  else {
    showInputError.value = false
  }

  if (showResult.value === false && (monthlyWage.value !== '' || annualBonus.value !== '' || rentalIncome.value !== '' || otherIncome.value !== '')) {
    showResult.value = !showResult.value
  }

  // Calculate the total income
  const totalIncome = Math.round(Number(monthlyWage.value) + (Number(annualBonus.value) / 12) + (Number(rentalIncome.value) * 0.7) + Number(otherIncome.value))

  // Calculate the total expenses
  const totalExpense = Math.round(Number(currentLoan.value) + Number(currentDebt.value) + Number(currentRent.value) + Number(otherExpense.value))

  // Loan and insurance rates (in percentage)
  let loanRate = 0

  if (Number(loanDurationInYears.value) === 7) {
    loanRate = 0.25
    displayLoanRate.value = 2.50
  }
  else if (Number(loanDurationInYears.value) === 10) {
    loanRate = 0.255
    displayLoanRate.value = 2.55
  }
  else if (Number(loanDurationInYears.value) === 15) {
    loanRate = 0.26
    displayLoanRate.value = 2.60
  }
  else if (Number(loanDurationInYears.value) === 20) {
    loanRate = 0.28
    displayLoanRate.value = 2.80
  }
  else if (Number(loanDurationInYears.value) === 25) {
    loanRate = 0.31
    displayLoanRate.value = 3.10
  }

  const insuranceRate = 2.5 / 100

  // Loan duration (in months)
  const loanDurationInMonths = Number(loanDurationInYears.value) * 12

  // Max Debt rate (in percentage)
  const maxDebtRate = 35 / 100

  // Maximum monthly loan amount
  moneyToLive.value = Math.round(totalIncome - totalExpense)

  if (moneyToLive.value <= ((800 * numberOfLoaner.value) + (350 * numberOfChildren.value))) {
    showMoneyToLiveError.value = true
    showLoanError.value = true
  }
  else {
    showMoneyToLiveError.value = false
    showLoanError.value = false
  }

  moneyLeft.value = Math.round((totalIncome * maxDebtRate) - totalExpense)
  debtRate.value = Math.round((totalExpense / totalIncome) * 100)

  if (debtRate.value >= 35) {
    showDebtError.value = true
    showLoanError.value = true
  }
  else {
    showDebtError.value = false
    showLoanError.value = false
  }

  const loanInsurance = (Number(moneyLeft.value) * insuranceRate) / 2
  const maxMonthlyLoan = Math.round(Number(moneyLeft.value) + loanInsurance)

  const maxMonthlyLoanWithLoanRate = maxMonthlyLoan * loanRate
  const trueMoneyLeftAfterAllRate = maxMonthlyLoan - maxMonthlyLoanWithLoanRate

  maxLoanCapacity.value = Math.round(trueMoneyLeftAfterAllRate * loanDurationInMonths)
  if (maxLoanCapacity.value < 0) {
    maxLoanCapacity.value = 0
  }

  // My contribution
  contribution.value = Math.round(Number(maxLoanCapacity.value) * 0.1)

  if (possibleContribution.value === 'no') {
    showLoanError.value = true
  }
  else {
    showLoanError.value = false
  }

}

</script>

<template>
  <div id="app" class="w-4/5 md:max-w-5xl mx-auto my-4 pb-4 bg-white space-y-4">

    <NavBar />

    <div class="px-4">
      <h1 class="py-4 text-2xl font-bold font-poppins">
        Calculer ma capacité d'emprunt
      </h1>

      <form>

        <div class="border-gray-900/10 pb-6">

          <!-- Loaner(s) general details -->

          <SubTitle title="Situation emprunteur(s)" />

          <div class="mt-4 grid grid-cols-1 gap-x-6 gap-y-3 sm:grid-cols-6 lg:grid-cols-12">

            <div class="sm:col-span-3 lg:col-span-4">
              <label for="number-of-loaner" class="block text-sm font-medium leading-6 text-gray-900">Nombre d'adulte
                (2 si couple)</label>
              <div class="mt-2">
                <select id="number-of-loaner" name="number-of-loaner" v-model="numberOfLoaner"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-sky-600 sm:col-3 lg:max-w-xs lg:text-sm sm:col-span-2 lg:leading-6">
                  <option value="1">1</option>
                  <option value="2">2</option>
                </select>
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-4">
              <label for="number-of-children" class="block text-sm font-medium leading-6 text-gray-900">Nombre d'enfant(s)
                à charge</label>
              <div class="mt-2">
                <select id="number-of-children" name="number-of-children" v-model="numberOfChildren"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:max-w-xs lg:text-sm sm:col-span-2 lg:leading-6">
                  <option value="0">0</option>
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

            <SubTitle title="Revenus (€)" />

            <div class="sm:col-span-3 lg:col-span-3 col-start-1">
              <label for="monthly-wage" class="block text-sm font-medium leading-6 text-gray-900">Salaire
                mensuel</label>
              <div class="mt-2">
                <input type="number" name="monthly-wage" id="monthly-wage" v-model="monthlyWage"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-3">
              <label for="annual-bonus" class="block text-sm font-medium leading-6 text-gray-900">Prime annuelle
              </label>
              <div class="mt-2">
                <input type="number" name="annual-bonus" id="annual-bonus" v-model="annualBonus"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-3">
              <label for="rental-income" class="block text-sm font-medium leading-6 text-gray-900">Revenus locatifs
                mensuels</label>
              <div class="mt-2">
                <input type="number" name="rental-income" id="rental-income" v-model="rentalIncome"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-3">
              <label for="other-income" class="block text-sm font-medium leading-6 text-gray-900">Autres revenus
                mensuels</label>
              <div class="mt-2">
                <input type="number" name="other-income" id="other-income" v-model="otherIncome"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 sm:col-span-2 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <!-- Expenses -->

            <SubTitle title="Charges (€)" />

            <div class="sm:col-span-3 lg:col-span-3 lg:col-start-1">
              <label for="current-loan" class="block text-sm font-medium leading-6 text-gray-900">Crédit immo.
                mensuel</label>
              <div class="mt-2">
                <input type="number" name="current-loan" id="current-loan" v-model="currentLoan"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-3">
              <label for="current-debt" class="block text-sm font-medium leading-6 text-gray-900">Autre crédit
                mensuel</label>
              <div class="mt-2">
                <input type="number" name="current-debt" id="current-debt" v-model="currentDebt"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-3">
              <label for="rent" class="block text-sm font-medium leading-6 text-gray-900">Loyer mensuel</label>
              <div class="mt-2">
                <input type="number" name="rent" id="rent" v-model="currentRent"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

            <div class="sm:col-span-3 lg:col-span-3">
              <label for="other-expense" class="block text-sm font-medium leading-6 text-gray-900">Autres charges
                mensuelles</label>
              <div class="mt-2">
                <input type="number" name="other-expense" id="other-expense" v-model="otherExpense"
                  class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
              </div>
            </div>

          </div>
        </div>

        <!-- Submit form -->

        <p class="flex items-center justify-center gap-x-3 text-rose-500 pb-3" v-if="showInputError">Veuillez entrer au
          moins un
          revenu</p>
        <div class="flex items-center justify-center gap-x-3">
          <button type="reset" @click="resetResult"
            class="text-sm font-semibold leading-6 text-gray-900 px-3 py-2 rounded-md bg-neutral-100">Annuler</button>
          <button type="submit" @click.prevent="getMaxLoan"
            class="rounded-md bg-sky-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-sky-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-sky-600">Calculer</button>
        </div>

      </form>

      <div v-if="showResult"
        class="grid grid-cols-1 gap-x-3 gap-y-6 sm:col-span-2 md:grid-cols-2 lg:grid-cols-3 bg-blue-100 mt-6 px-6 py-6 rounded-md">

        <div class="lg:border-r lg:border-gray-400 px-4">
          <p class="block text-sm leading-6 text-gray-900 font-bold">Taux d'endettement</p>
          <p class="font-bold text-2xl text-rose-500" v-if="showDebtError">{{ debtRate }} %</p>
          <p class="font-bold text-2xl text-green-500" v-else="showDebtError">{{ debtRate }} %</p>
          <p class="flex items-center gap-x-3 text-rose-500 pb-3" v-if="showDebtError">Taux d'endettement trop élevé</p>
        </div>

        <div class="lg:border-r lg:border-gray-400 px-4">
          <p class="block text-sm leading-6 text-gray-900 font-bold">Reste à vivre</p>
          <p class="font-bold text-2xl text-rose-500" v-if="showMoneyToLiveError">{{ moneyToLive }} €</p>
          <p class="font-bold text-2xl text-green-500" v-else="showMoneyToLiveError">{{ moneyToLive }} €</p>
          <p class="flex items-center gap-x-3 text-rose-500 pb-3" v-if="showMoneyToLiveError">Le reste à vivre est
            insuffisant</p>
        </div>

        <div class="px-4">
          <p class="block text-sm leading-6 text-gray-900 font-bold">Capacité de remboursement</p>
          <p class="font-bold text-2xl">{{ moneyLeft }} €</p>
        </div>

        <div class="lg:border-r lg:border-gray-400 px-4">
          <p class="block text-sm leading-6 text-gray-900 font-bold">Apport requis
          </p>
          <p class="font-bold text-2xl">{{ contribution }} €</p>
        </div>

        <div class="flex gap-2 items-center lg:border-r lg:border-gray-400 px-4">
          <p class="block text-sm leading-6 text-gray-900 font-bold">J'ai cet apport ?</p>
          <input type="radio" id="yes" value="yes" name="possible-contribution" v-model="possibleContribution"
            @change="getMaxLoan" checked class="block border-0 py-2 px-2 text-sky-600">
          <label for="yes" class="block text-sm font-medium leading-6 text-gray-900">Oui</label>

          <input type="radio" id="no" value="no" name="possible-contribution" v-model="possibleContribution"
            @change="getMaxLoan" class="block border-0 py-2 px-2 text-sky-600">
          <label for="no" class="block text-sm font-medium leading-6 text-gray-900">Non</label>
        </div>

        <div class="px-4">
          <p class="block text-sm leading-6 text-gray-900 font-bold">Capacité d'emprunt (+/- 10%)</p>
          <p class="font-bold text-2xl text-rose-500" v-if="showLoanError">{{ maxLoanCapacity }} €</p>
          <p class="font-bold text-2xl text-green-500" v-else="showLoanError">{{ maxLoanCapacity }} €</p>
          <p class="flex items-center gap-x-3 text-rose-500 pb-3" v-if="showLoanError">Difficile d'obtenir ce prêt</p>
        </div>

        <div class="px-4">
          <label for="loan-duration" class="block text-sm leading-6 text-gray-900 font-bold">Durée
            (ans)</label>
          <div class="mt-2">
            <select id="loan-duration" name="loan-duration" v-model="loanDurationInYears" @change="getMaxLoan"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:max-w-xs lg:text-sm sm:col-span-2 lg:leading-6">
              <option value="7">7</option>
              <option value="10">10</option>
              <option value="15">15</option>
              <option value="20">20</option>
              <option value="25">25</option>
            </select>
          </div>
        </div>

        <div class="px-4">
          <label for="loan-rate" class="block text-sm leading-6 text-gray-900 font-bold">Taux (%)</label>
          <div class="mt-2">
            <input type="number" name="loan-rate" id="loan-rate" v-model="displayLoanRate" @change="getMaxLoan"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
          </div>
        </div>

        <div class="px-4">
          <label for="insurance-rate" class="block text-sm leading-6 text-gray-900 font-bold">Assurance
            (%)</label>
          <div class="mt-2">
            <input type="number" name="insurance-rate" id="insurance-rate" v-model="displayInsuranceRate"
              class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-sky-600 lg:text-sm sm:col-span-2 lg:leading-6">
          </div>
        </div>
      </div>
    </div>

  </div>
</template>
