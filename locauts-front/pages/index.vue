<template>
  <div>
    <Navegacao/>
    <div class="container">
      <h1>Lista de Funcionários</h1>
      <b-table striped responsive hover :items="clinicas" :fields="campos">
        <template v-slot:cell(nome_Clinica)="data">
          <NuxtLink :to="`/clinicas/${data.item.id}`">
            <span>{{ data.value }}</span>
          </NuxtLink>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let clinicas
    try {
      clinicas = await $axios.$get("/clinica");
      
    } catch (e) {
      
      console.log(e)
    }
    console.log(JSON.stringify(clinicas));
    return {clinicas}
  },
  data: function () {
    return {
      campos: [
        {
          key: 'nome_Clinica',
        },
        {
          key: 'endereco_Clinica',
        },
        {
          key: 'instituicao_Privada',
        },
        {
          key: 'telefone',
        },
        {
          key: 'especialidade',
        },
        {
          key: 'numero_Alas',
        },
        {
          key: 'cnpj',
        },
        {
          key: 'horario_Atendimento',
        },
      ],


    }
  },
}
</script>
