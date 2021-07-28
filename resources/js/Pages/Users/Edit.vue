<template>
  <app-layout title="Dashboard">
    <template #header>
      <h2 class="text-xl font-semibold leading-tight text-gray-800">Edit</h2>
    </template>

    <div class="py-12">
      <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
        <jet-form-section @submitted="updateProfileInformation">
          <template #form>
            <!-- Name -->
            <div class="col-span-6 sm:col-span-4">
              <jet-label for="name" value="Name" />
              <jet-input
                id="name"
                type="text"
                class="block w-full mt-1"
                v-model="form.name"
                autocomplete="name"
              />
              <jet-input-error :message="form.errors.name" class="mt-2" />
            </div>

            <!-- Email -->
            <div class="col-span-6 sm:col-span-4">
              <jet-label for="email" value="Email" />
              <jet-input
                id="email"
                type="email"
                class="block w-full mt-1"
                v-model="form.email"
              />
              <jet-input-error :message="form.errors.email" class="mt-2" />
            </div>
          </template>

          <template #actions>
            <jet-action-message :on="form.recentlySuccessful" class="mr-3">
              Saved.
            </jet-action-message>

            <jet-button
              :class="{ 'opacity-25': form.processing }"
              :disabled="form.processing"
            >
              Save
            </jet-button>
          </template>
        </jet-form-section>
      </div>
    </div>
  </app-layout>
</template>

<script>
import AppLayout from "@/Layouts/AppLayout.vue";
import JetButton from "@/Jetstream/Button.vue";
import JetFormSection from "@/Jetstream/FormSection.vue";
import JetInput from "@/Jetstream/Input.vue";
import JetInputError from "@/Jetstream/InputError.vue";
import JetLabel from "@/Jetstream/Label.vue";
import JetActionMessage from "@/Jetstream/ActionMessage.vue";
import JetSecondaryButton from "@/Jetstream/SecondaryButton.vue";

export default {
  components: {
    AppLayout,
    JetActionMessage,
    JetButton,
    JetFormSection,
    JetInput,
    JetInputError,
    JetLabel,
    JetSecondaryButton,
  },
  props: ["user"],

  data() {
    return {
      form: this.$inertia.form({
        _method: "PUT",
        name: this.user.name,
        email: this.user.email,
        photo: null,
      }),
    };
  },

  methods: {
    updateProfileInformation() {
      // if (this.$refs.photo) {
      //   this.form.photo = this.$refs.photo.files[0];
      // }
      // console.log(route("users.update", this.user.id));
      // return;
      this.form.post(route("users.update", this.user.id), {
        preserveScroll: true,
        onSuccess: () => console.log('Updated successfully'),
      });
    },
  },
};
</script>
