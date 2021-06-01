<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="nom"
        label="Votre nom *"
        hint="Votre nom"
        lazy-rules
        :rules="[ val => val && val.length > 3|| 'Veuillez saisir un nom valide']"
      />

      <q-input
        filled
        v-model="prenom"
        label="Votre prenom *"
        hint="Votre prenom"
        lazy-rules
        :rules="[ val => val && val.length > 3|| 'Veuillez saisir un nom valide']"
      />

        <q-input
            filled
            v-model="email"
            label="Your email *"
            hint="Votre email"
            lazy-rules
            :rules="[val => !!val || 'Email is missing', isValidEmail]"
        />

      <!--q-date
        v-model="naissance"
        :options="optionsFn"
      /-->

      <q-input filled v-model="naissance" mask="date" :rules="['naissance']" hint="Date de naissance *" label="Date de naissance *">
      <template v-slot:append>
        <q-icon name="event" class="cursor-pointer">
          <q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
            <q-date v-model="naissance" :options="optionsFn">
              <div class="row items-center justify-end">
                <q-btn v-close-popup label="Close" color="primary" flat />
              </div>
            </q-date>
          </q-popup-proxy>
        </q-icon>
      </template>
    </q-input>

    <q-input
        label="Année du BAC *"
        hint="Année du BAC"
        v-model.number="model"
        type="number"
        filled
    />

      <q-input
        filled
        type="password"
        v-model="pass"
        label="Mot de passe *"
        lazy-rules
        :rules="[ val => val && val.length > 7|| 'Mot de passe réquis']"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
export default {
    name: 'Signup',

  data () {
    return {
      email: null,
      pass: null,
      naissance: '1990/02/01',

      accept: false
    }
  },

  methods: {
    optionsFn (naissance) {
      return naissance >= '1900/02/03' && naissance <= '2005/02/15'
    },
    onSubmit () {
      if (this.accept !== true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning',
          message: 'You need to accept the license and terms first'
        })
      }
      else {
        this.$q.notify({
          color: 'green-4',
          textColor: 'white',
          icon: 'cloud_done',
          message: 'Submitted'
        })
      }
    },
    isValidEmail (val) {
      const emailPattern = /^(?=[a-zA-Z0-9@._%+-]{6,254}$)[a-zA-Z0-9._%+-]{1,64}@(?:[a-zA-Z0-9-]{1,63}\.){1,8}[a-zA-Z]{2,63}$/;
      return emailPattern.test(val) || 'Invalid email';
    },

    onReset () {
      this.name = null
      this.age = null
      this.accept = false
    }
  }
}
</script>
<style>

</style>