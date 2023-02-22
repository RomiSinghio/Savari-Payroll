<template v-for="report in data" :key="report.id">
    <h2 class="mt-2 text-2xl font-bold leading-7 text-white sm:truncate sm:text-3xl sm:tracking-tight">
        Driver: <span class=" uppercase"> {{ report.driver.name }}</span></h2>
    <div class="mt-1 flex flex-col sm:mt-0 sm:flex-row sm:flex-wrap sm:space-x-6">
        <div class="mt-2 flex items-center text-sm text-gray-300">

            ID: {{ report.id }}
        </div>

        <div class="mt-2 flex items-center text-sm text-gray-300">
            <CurrencyDollarIcon class="mr-1.5 h-5 w-5 flex-shrink-0 text-gray-500" aria-hidden="true" />
            {{ report.driver.contract_hours }} Hours per month
        </div>
        <div class="mt-2 flex items-center text-sm text-gray-300">
            <CalendarIcon class="mr-1.5 h-5 w-5 flex-shrink-0 text-gray-500" aria-hidden="true" />
            {{ report.created_at }}
        </div>
    </div>
</template>


<script setup>
const client = useSupabaseClient()

// get all reports with name of driver
const { data } = useAsyncData('reports', async () => {
    const { data, error } = await client
        .from('reports')
        .select('id, driver (name, contract_hours ),  created_at')

    if (error) {
        console.log(error)
    }
    return data
})
</script>