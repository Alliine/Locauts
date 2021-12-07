<template>
  <div>
    <Navegacao />
    <div class="container">
      <h1>Adicionar uma nova clinica</h1>
      <b-form @submit.prevent="criarClinica">
        <b-form-group
          id="input-group-1"
          label="Nome da nova clinica:"
          label-for="nome_Clinica"
        >
          <b-form-input
            id="nome_Clinica"
            v-model="form.nome_Clinica"
            placeholder="Entre com um nome"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-2"
          label="Endereço:"
          label-for="endereco_Clinica"
        >
          <b-form-input
             id="endereco_Clinica"
            v-model="form.endereco_Clinica"
            placeholder="Entre com um endereço"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-3"
          label="Instituição Privada:"
          label-for="instituicao_Privada"
        >
          <b-form-input
            id="instituicao_Privada"
            v-model="form.instituicao_Privada"
            placeholder="Entre com true ou false"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-4" label="Telefone:" label-for="telefone">
          <b-form-input
            id="telefone"
            v-model="form.telefone"
            placeholder="Entre com um telefone"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-5"
          label="Especialidade da nova clinica:"
          label-for="especialidade"
        >
          <b-form-input
            id="especialidade"
            v-model="form.especialidade"
            placeholder="Entre com uma especialidade"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-6"
          label="Numero Alas da nova clinica:"
          label-for="numero_Alas"
        >
          <b-form-input
            id="numero_Alas"
            v-model="form.numero_Alas"
            placeholder="Entre com um numero de alas"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-7" label="Cnpj" label-for="cnpj">
          <b-form-input
            id="cnpj"
            v-model="form.cnpj"
            placeholder="Entre com um cnpj"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          id="input-group-8"
          label="Horário Atendimento da nova clinica:"
          label-for="horario_Atendimento"
        >
          <b-form-input
            id="horario_Atendimento"
            v-model="form.horario_Atendimento"
            placeholder="Entre com um horário de atendimento"
            required
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Criar</b-button>
        <b-button type="reset" variant="danger">Limpar</b-button>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      form: {
        nome_Clinica: '',
        endereco_Clinica: '',
        instituicao_Privada: '',
        telefone: '',
        especialidade: '',
        numero_Alas: '',
        cnpj: '',
        horario_Atendimento: '',
      },
    }
  },
  methods: {
    async criarClinica(event) {
      event.preventDefault()

      try {
        let dataClinica = await this.$axios.$post('/clinica/criar', this.form)
        console.log(dataClinica);
        if (dataClinica !== null) {
          this.$bvModal.msgBoxOk('A nova clinica foi criada com sucesso', {
            title: 'Confirmation',
            size: 'sm',
            buttonSize: 'sm',
            okVariant: 'success',
            headerClass: 'p-2 border-bottom-0',
            footerClass: 'p-2 border-top-0',
            centered: true,
          })
          this.limparCampos()
        } else {
          throw new Error(
            `Não possível criar a Clinica ${this.form.nome_Clinica}`
          )
        }
      } catch (error) {
        console.log(error);
      }
    },

    limparCampos() {
      this.form = {
        nome_Clinica: '',
        endereco_Clinica: '',
        instituicao_Privada: '',
        telefone: '',
        especialidade: '',
        numero_Alas: '',
        cnpj: '',
        horario_Atendimento: '',
      }
    },
  },
}
</script>

<style>
</style>