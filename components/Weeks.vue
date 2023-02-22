<template>
    <div class="px-12 ">
        <div class="sm:flex sm:items-center">
            <div class="sm:flex-auto">
                <h1 class="text-xl font-semibold text-gray-900">Weeks</h1>
                <p class="mt-2 text-sm text-gray-700">A list of all the weeks for this driver.</p>
            </div>
            <div class="mt-4 sm:mt-0 sm:ml-16 sm:flex-none">
                <button type="button"
                    class="block rounded-md bg-indigo-600 py-1.5 px-3 text-center text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Create
                    Week</button>
            </div>
        </div>
        <div class="mt-8 flow-root">
            <div class="-my-2 -mx-6 overflow-x-auto lg:-mx-8">
                <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
                    <div class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg">
                        <table class="min-w-full divide-y divide-gray-300">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th scope="col" class="py-3.5 pl-6 pr-3 text-left text-sm font-semibold text-gray-900">
                                        Name</th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Hours
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Base
                                        Rate
                                    </th>
                                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Total
                                    </th>
                                    <th scope="col" class="relative py-3.5 pl-3 pr-6">
                                        <span class="sr-only">Edit</span>
                                    </th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-200 bg-white">
                                <tr v-for="week in data" :key="data.id">
                                    <td class="whitespace-nowrap py-4 pl-6 pr-3 text-sm font-medium text-gray-900">{{
                                        week.name }}</td>
                                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ week.total_hours }}
                                    </td>
                                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">£{{ week.base_rate }}
                                    </td>
                                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">£{{ week.total_amount }}
                                    </td>
                                    <td class="relative whitespace-nowrap py-4 pl-3 pr-6 text-right text-sm font-medium">
                                        <a href="#" class="text-indigo-600 hover:text-indigo-900">Edit<span
                                                class="sr-only">, {{ week.name }}</span></a>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>

const route = useRoute()
const client = useSupabaseClient()

const { data, error } = await client.from('weeks').select('*').eq('reports', route.params.id)
if (error) {
    console.log('error', error)
}



</script>