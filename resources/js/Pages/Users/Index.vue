<template>
  <app-layout title="Dashboard">
    <template #header>
      <h2 class="text-xl font-semibold leading-tight text-gray-800">Users
        <Link class="float-right" :href="route('users.create')" v-if="$page.props.permission.users.create">
          <jet-button>Create</jet-button>
        </Link>
      </h2>
    </template>

    <div class="py-12">
      <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
        <div class="overflow-hidden bg-white shadow-md sm:rounded-lg">
          <!-- This example requires Tailwind CSS v2.0+ -->
          <div class="flex flex-col">
            <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
              <div
                class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8"
              >
                <div
                  class="overflow-hidden border-b border-gray-200 shadow sm:rounded-lg"
                >
                  <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-gray-50">
                      <tr>
                        <th
                          scope="col"
                          class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase "
                        >
                          Name
                        </th>
                        <th
                          scope="col"
                          class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase "
                        >
                          Status
                        </th>
                        <th
                          scope="col"
                          class="px-6 py-3 text-xs font-medium tracking-wider text-left text-gray-500 uppercase "
                        >
                          Role
                        </th>
                        <th scope="col" class="relative px-6 py-3 text-xs font-medium tracking-wider text-center text-gray-500 uppercase">
                          Edit
                          <span class="sr-only">Edit</span>
                        </th>
                      </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                      <tr v-for="user in users" :key="user.id">
                        <td class="px-6 py-4 whitespace-nowrap">
                          <div class="flex items-center">
                            <div class="flex-shrink-0 w-10 h-10">
                              <img
                                class="w-10 h-10 rounded-full"
                                :src="user.profile_photo_url"
                                alt=""
                              />
                            </div>
                            <div class="ml-4">
                              <div class="text-sm font-medium text-gray-900">
                                {{ user.name }}
                              </div>
                              <div class="text-sm text-gray-500">
                                {{ user.email }}
                              </div>
                            </div>
                          </div>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap">
                          <span
                            class="inline-flex px-2 text-xs font-semibold leading-5 text-green-800 bg-green-100 rounded-full "
                          >
                            Active
                          </span>
                        </td>
                        <td
                          class="px-6 py-4 text-sm text-gray-500 whitespace-nowrap"
                        >
                          {{ user.role }}
                        </td>
                        <td
                          class="px-6 py-4 text-sm font-medium text-center whitespace-nowrap"
                        >
                          <Link
                            :href="route('users.show', user.id)"
                            class="text-indigo-600 hover:text-indigo-900"
                            v-if="user.can.view"
                            >Show</Link
                          >
                          <Link
                            :href="route('users.edit', user.id)"
                            class="ml-2 text-indigo-600 hover:text-indigo-900"
                            v-if="user.can.update"
                            >Edit</Link
                          >
                        </td>
                      </tr>

                      <!-- More people... -->
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout.vue";
import JetButton from "@/Jetstream/Button.vue";
import { Link } from '@inertiajs/inertia-vue3';

export default {
  components: {
    AppLayout,
    Link,
    JetButton,
  },
  props: ['users'],
};
</script>
