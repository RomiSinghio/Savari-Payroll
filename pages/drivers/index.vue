<template>
    <div class="px-6 lg:px-8">
        <div class="sm:flex sm:items-center">
            <div class="sm:flex-auto">
                <h1 class="text-xl font-semibold text-gray-900">Users</h1>
                <p class="mt-2 text-sm text-gray-700">A list of all the users in your account including their name, title,
                    email and role.</p>
            </div>
            <div class="mt-4 sm:mt-0 sm:ml-16 sm:flex-none">
                <button type="button"
                    class="block rounded-md bg-indigo-600 py-1.5 px-3 text-center text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Add
                    user</button>
            </div>
        </div>
        <div class="mt-8 flow-root">
            <div class="-my-2 -mx-6 overflow-x-auto lg:-mx-8">
                <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
                    <table class="min-w-full divide-y divide-gray-300">
                        <thead>
                            <tr>
                                <th scope="col"
                                    class="py-3.5 pl-6 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-0">Name</th>
                                <th scope="col" class="py-3.5 px-3 text-left text-sm font-semibold text-gray-900">Title</th>
                                <th scope="col" class="py-3.5 px-3 text-left text-sm font-semibold text-gray-900">Email</th>
                                <th scope="col" class="py-3.5 px-3 text-left text-sm font-semibold text-gray-900">Role</th>
                                <th scope="col" class="relative py-3.5 pl-3 pr-6 sm:pr-0">
                                    <span class="sr-only">Edit</span>
                                </th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-gray-200">
                            <tr v-for="driver in data" :key="data.id">
                                <td class="whitespace-nowrap py-4 pl-6 pr-3 text-sm font-medium text-gray-900 sm:pl-0">{{
                                    driver.name }}</td>
                                <td class="whitespace-nowrap py-4 px-3 text-sm text-gray-500">{{ driver.name }}</td>
                                <td class="whitespace-nowrap py-4 px-3 text-sm text-gray-500">{{ driver.email }}</td>
                                <td class="whitespace-nowrap py-4 px-3 text-sm text-gray-500">{{ driver.employed ?
                                    "Employeed" :
                                    "Self-Employed" }}</td>
                                <td class="whitespace-nowrap py-4 px-3 text-sm text-gray-500">{{ driver.active ?
                                    "Active" :
                                    "In-Active" }}</td>
                                <td
                                    class="relative whitespace-nowrap py-4 pl-3 pr-6 text-right text-sm font-medium sm:pr-0">
                                    <a href="#" class="text-indigo-600 hover:text-indigo-900">Edit<span class="sr-only">, {{
                                        driver.name }}</span></a>
                                </td>




                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>


const client = useSupabaseClient()

const { data } = useAsyncData('drivers', async () => {
    const { data, error } = await client.from('drivers').select('*')
    if (error) {
        console.log(error)
    }
    return data
})
</script>
  