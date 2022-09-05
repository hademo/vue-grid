<script setup lang="ts">
import VGrid from './components/VGrid.vue'
import GridCell from './components/GridCell.vue'
import SafetyContent from './components/SafetyContent.vue'

type User = {
  firstname: string,
  lastname: string,
  description: string,
  age: number
}

type Drug = {
  title: string,
  dosage: number,
  warning: string,
  interaction: string
}

type Country = {
  country: string,
  acronym: string,
  languages: string[]
}

const users: User[] = [{
  firstname: 'Martina',
  lastname: 'Musterfrau',
  age: 29,
  description: 'Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.',
},
{
  firstname: 'Max',
  lastname: 'Mustermann',
  age: 10,
  description: 'Lorem ipsum dolor sit amet, qui minim labore adipisicing minim sint cillum sint consectetur cupidatat.',
}]


const drugs: Drug[] = [{
  title: 'DrugA',
  dosage: 500,
  warning: "Not for children",
  interaction: "DrugB"
},
{
  title: 'DrugB',
  dosage: 1000,
  warning: "Not for children & pregnant women",
  interaction: ""
}]

const countries: Country[] = [
  {
    country: "Austria",
    acronym: "AT",
    languages: ["German", "English"]
  },
  {
    country: "United Kingdom",
    acronym: "UK",
    languages: ["English", "French", "American-English"]
  }
]

const gridSize = 6;
const gridGap = 2;
</script>

<template>

  <div class="flex flex-col gap-4 custom-grid m-20">
    <SafetyContent :size="gridSize" :gap="gridGap" :items="users">
      <template #header>
        Hello
      </template>

      <template #columns>
        <GridCell class="col-h">Firstname</GridCell>
        <GridCell class="col-h">Lastname</GridCell>
        <GridCell class="col-h" :span="3">Description</GridCell>
        <GridCell class="col-h">Age</GridCell>
      </template>

      <template #item="{ firstname, lastname, description, age }: User">
        <GridCell class="cell">{{ firstname }}</GridCell>
        <GridCell class="cell">{{ lastname }}</GridCell>
        <GridCell :span="3" class="col-user-description">{{ description }}</GridCell>
        <GridCell class="cell">{{ age }}</GridCell>
      </template>
    </SafetyContent>

    <SafetyContent :size="gridSize" :gap="gridGap" :items="drugs">
      <template #header>
        Drugs
      </template>

      <template #columns>
        <GridCell class="col-h">Name</GridCell>
        <GridCell class="col-h" :span="2">Dosage</GridCell>
        <GridCell class="col-h" :span="2">Warning</GridCell>
        <GridCell class="col-h" :span="1">Interaction</GridCell>
      </template>

      <template #item="{ title, warning, dosage, interaction }: Drug">
        <GridCell class="cell">{{ title }}</GridCell>
        <GridCell class="cell">{{ dosage }} mg</GridCell>
        <GridCell class="cell">{{ dosage / 1000 }} g</GridCell>
        <GridCell class="cell" :span="2">{{ warning }}</GridCell>
        <GridCell class="cell">{{ interaction }}</GridCell>
      </template>
    </SafetyContent>

    <SafetyContent :size="gridSize" :gap="gridGap" :items="countries">
      <template #header>Cities</template>

      <template #columns>
        <GridCell class="col-h">Acronym</GridCell>
        <GridCell class="col-h">Country</GridCell>
        <GridCell class="col-h">Language</GridCell>
      </template>

      <template #item="{ country, acronym, languages }">
        <GridCell class="cell">{{ acronym }}</GridCell>
        <GridCell class="cell">{{ country }}</GridCell>
        <GridCell class="cell col-country-languages">
          <span v-for="language in languages">
            {{ language }}
          </span>
        </GridCell>
      </template>
    </SafetyContent>
  </div>
</template>

<style scoped>
div {
  @apply text-white
}

.custom-grid {
  @apply bg-blue-800 p-4
}

.col-user-description {
  @apply bg-red-900
}

.col-country-languages {
  @apply flex flex-col gap-2
}

.col-country-languages>span {
  @apply bg-yellow-900 text-center
}

.custom-grid .cell {
  @apply border text-white p-2
}

.col-h {
  @apply font-bold bg-gray-900 text-white border p-2
}

.section {
  @apply col-span-full bg-green-800
}
</style>
