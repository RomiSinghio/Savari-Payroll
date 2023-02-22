<script setup>

const client = useSupabaseClient()


const createDriver = async (e) => {
    const { name, email, employed, active } = e.target.elements
    const { data, error } = await client.from('drivers').insert([
        {
            name: name.value,
            email: email.value,
            employed: employed.value,
            active: active.value,
        },
    ])
    if (error) {
        console.log(error)
    }

}





</script>
<template>
    <div>
        <h1>Create Driver</h1>
        <form @submit.prevent="createDriver">
            <div class="mb-4">
                <label for="name" class="block text-sm font-medium text-gray-700">Name</label>
                <div class="mt-1">
                    <input type="text" name="name" id="name" autocomplete="name" required
                        class="block w-full shadow-sm sm:text-sm focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md">
                </div>
            </div>
            <div class="mb-4">
                <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
                <div class="mt-1">
                    <input type="email" name="email" id="email" autocomplete="email" required
                        class="block w-full shadow-sm sm:text-sm focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md">
                </div>
            </div>
            <div class="mb-4">
                <label for="phone" class="block text-sm font-medium text-gray-700">Phone</label>
                <div class="mt-1">
                    <input type="text" name="phone" id="phone" autocomplete="phone" required
                        class="block w-full shadow-sm sm:text-sm focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md">
                </div>
            </div>
            <div class="mb-4">
                <label for="employed" class="block text-sm font-medium text-gray-700">Employed</label>
                <div class="mt-1">
                    <select id="employed" name="employed" autocomplete="employed" required
                        class="block w-full shadow-sm sm:text-sm focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md">
                        <option value="true">Yes</option>
                        <option value="false">No</option>
                    </select>
                </div>
            </div>
            <div class="mb-4">
                <label for="active" class="block text-sm font-medium text-gray-700">Active</label>
                <div class="mt-1">
                    <select id="active" name="active" autocomplete="active" required
                        class="block w-full shadow-sm sm:text-sm focus:ring-indigo-500 focus:border-indigo-500 border-gray-300 rounded-md">
                        <option value="true">Yes</option>
                        <option value="false">No</option>
                    </select>
                </div>
            </div>

            <button type="submit"
                class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                Create
            </button>
        </form>
    </div>
</template>