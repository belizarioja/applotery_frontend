<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <q-page class="flex flex-center">
        <div class="q-pa-md" style="max-width: 400px">

          <q-form
            @submit="onSubmit"
            @reset="onReset"
            class="q-gutter-md"
          >
            <q-input
              filled
              v-model="name"
              label="Usuario"
              hint="Introduzca usuario"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Por favor escriba algo']"
            />

            <q-input
              filled
              type="password"
              v-model="age"
              label="Clave"
              lazy-rules
              :rules="[
                val => val !== null && val !== '' || 'Por favor escriba algo'
              ]"
            />

            <q-toggle v-model="accept" label="Guardar clave" />

            <div>
              <q-btn label="Enviar" type="submit" color="primary"/>
              <q-btn label="Limpiar" type="reset" color="primary" flat class="q-ml-sm" />
            </div>
          </q-form>

        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { useQuasar } from 'quasar'

export default defineComponent({
  name: 'LoginLayout',
  setup () {
    const $q = useQuasar()

    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)

    return {
      name,
      age,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        } else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

      onReset () {
        name.value = null
        age.value = null
        accept.value = false
      }
    }
  }
})
</script>
