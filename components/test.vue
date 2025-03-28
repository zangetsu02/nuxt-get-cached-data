<template>
  <div>
    {{ data }}
  </div>
</template>

<script lang="ts" setup>
const nuxtApp = useNuxtApp()
const { data } = await useFetch<any>('https://icanhazdadjoke.com/j/0189hNRf2g', {
  headers: {
    Accept: 'application/json'
  },
  transform(input) {
    return {
      ...input,
      fetchedAt: new Date()
    }
  },
  getCachedData(key) {
    const data = nuxtApp.payload.data[key] || nuxtApp.static.data[key]
    // If data is not fetched yet
    if (!data) {
      // Fetch the first time
      console.log('FETCHING...')
      return
    }

    // Is the data too old?
    const expirationDate = new Date(data.fetchedAt)
    expirationDate.setTime(expirationDate.getTime() + 10 * 1000)
    const isExpired = expirationDate.getTime() < Date.now()
    if(isExpired) {
      // Refetch the data
      return
    }

    return data
  },
})
</script>
