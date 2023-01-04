<template>
  <q-page class="container bg-grey-10">
    <p class="text-h4">FORMULARIO</p>
      <q-form
        @submit="onSubmit"
        @reset="onReset"
      class="row q-col-gutter-md"
      ref="myForm"
      >
        <q-input
        outlined
        dark
        v-model="form.nome"
        color="purple"
        label="Nome"
        class="col-md-12 colsm-12 col-xs-12"
        :rules="[
          val => val && val.length > 0 || 'Nome Obrigatorio'
        ]"
        >
          <template v-slot:prepend>
          <q-icon name="person" />
        </template>
        </q-input>

        <q-input
          color="purple"
          dark
          v-model.number="form.idade"
          type="number"
          outlined
          class="col-md-12 colsm-12 col-xs-12"
          label="Idade"
          :rules="[
          val => val !== null && val !== '' || 'Idade Obrigatoria',
          val => val >= 18 && val <100 || 'Voçê tem que ser maior de 18 anos para se cadastrar'
        ]"
        >
        <template v-slot:prepend>
          <q-icon name="event" />
        </template>
        </q-input>

        <q-input
          color="purple"
          dark
          v-model="form.email"
          label="Email"
          suffix="@gmail.com"
          outlined
          class="col-md-12 colsm-12 col-xs-12"
          :rules="[
          val => val && val.length > 0 || 'E-mail Obrigatorio'
        ]"
        >
        <template v-slot:prepend>
          <q-icon name="mails"/>
        </template>
        </q-input>

        <q-input
          color="purple"
          dark
          v-model="form.telefone"
          label="Telefone"
          outlined
          class="col-md-12 colsm-12 col-xs-12"
          mask="(##)#####-####"
          unmasked-value
          :rules="[
          val => val && val.length > 0 || 'Telefone Obrigatorio',
          val => val.length === 11 || 'Coloque um Numero de telefone valido'
        ]"
        />
        <div class="col-12">
          <q-btn
            label="Cadastrar"
            type="submit"
            color="primay"
            class="float-right"
          />
        </div>
        <div class="col-12">
          <q-btn
            label="Limpar"
            type="reset"
            color="primay"
            class="float-right q-mr-md"
          />
          </div>
      </q-form>
  </q-page>
</template>

<script>

export default {
  name: 'IndexPage',
  data () {
    return {
      form: {
        nome: '',
        idade: null,
        email: '',
        telefone: ''
      }
    }
  },
  methods: {
    onSubmit () {
      this.$q.notify({
        message: 'Cadastro Realizado com sucesso',
        color: 'positive',
        icon: 'check_circle_outline'
      })
      this.onReset()
    },
    async onReset () {
      await this.resetForm()
      this.$refs.myForm.resetValidation()
    },
    async resetForm () {
      this.form = {
        nome: '',
        idade: null,
        email: '',
        telefone: ''
      }
    }
  }
}
</script>
