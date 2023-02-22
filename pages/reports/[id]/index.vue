<template>
    <div class="bg-[#212936]">
        <div class="container px-4 py-4 mx-auto">
            <div class="lg:flex lg:items-center lg:justify-between">
                <div class="min-w-0 flex-1">
                    <template v-for="report in data" :key="report.id">
                        <h2 class="mt-2 text-2xl font-bold leading-7 text-white sm:truncate sm:text-3xl sm:tracking-tight">
                            Driver: <span class=" uppercase"> {{ report.driver.name }}</span></h2>
                        <div class="mt-1 flex flex-col sm:mt-0 sm:flex-row sm:flex-wrap sm:space-x-6">
                            <div class="mt-2 flex items-center text-sm text-gray-300">

                                ID: {{ report.id }}
                            </div>

                            <div class="mt-2 flex items-center text-sm text-gray-300">
                                <CurrencyDollarIcon class="mr-1.5 h-5 w-5 flex-shrink-0 text-gray-500" aria-hidden="true" />
                                {{ report.driver }} Hours per month
                            </div>
                            <div class="mt-2 flex items-center text-sm text-gray-300">
                                <CalendarIcon class="mr-1.5 h-5 w-5 flex-shrink-0 text-gray-500" aria-hidden="true" />
                                {{ report.created_at }}
                            </div>
                        </div>
                    </template>
                </div>
                <div class="mt-5 flex lg:mt-0 lg:ml-4">
                    <span class="sm:ml-3">
                        <button type="button"
                            class="inline-flex items-center rounded-md border border-transparent bg-indigo-500 px-4 py-2 text-sm font-medium text-white shadow-sm hover:bg-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-800">
                            <CheckIcon class="-ml-1 mr-2 h-5 w-5" aria-hidden="true" />
                            Save
                        </button>
                    </span>
                </div>
            </div>
        </div>
    </div>
    <Weeks class="my-12" />
</template>

<script setup>

import {
    BriefcaseIcon,
    CalendarIcon,
    CheckIcon,
    ChevronDownIcon,
    ChevronRightIcon,
    CurrencyDollarIcon,
    LinkIcon,
    MapPinIcon,
    PencilIcon,
} from '@heroicons/vue/20/solid'
import { Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'

const client = useSupabaseClient()

// get all reports with name of driver
const { data } = useAsyncData('reports', async () => {
    const { data, error } = await client
        .from('reports')
        .select('id, driver ( * ),  created_at')

    if (error) {
        console.log(error)
    }
    return data
})

console.log(data);

</script>

