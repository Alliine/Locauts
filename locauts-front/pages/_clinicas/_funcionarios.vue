<template>
  <div class="container">
     <Navegacao />
   
      <h1>Funcionários</h1>
      
        <h1>{{ clinicas.nome_Clinica }}</h1>
     
      <div>
        <b-button @click="showModal = true" pill variant="info">
          <b-icon icon="plus"></b-icon>
        </b-button>
      </div>
      
      <li :key="funcionarios.id" v-for="funcionarios in clinicas.funcionarios">
            {{ funcionarios.nome_fun }} - CPF:
            {{ funcionarios.cpf }} - Salario:
            {{ funcionarios.salario }} - Cargo:
            {{ funcionarios.cargo}}
          
        </li>

      <b-modal id="modal-tarefa" size="lg" v-model="showModal" hide-footer>
        <h1>Novo Funcionário</h1>
        <b-container fluid>
          <b-row class="my-1">
            <b-col sm="1">
              <label for="nome_fun">Funcionario:</label>
            </b-col>
            <b-col sm="5">
              <b-form-input
                id="nome_fun"
                size="sm"
                placeholder="Digite o nome:"
                v-model="novoFuncionario.nome_fun"
              ></b-form-input>
            </b-col>
            <b-col sm="1">
              <label for="cpf">Cpf:</label>
            </b-col>
             <b-col sm="5">
              <b-form-input
                id="cpf"
                size="sm"
                placeholder="Digite o cpf:"
                v-model="novoFuncionario.cpf"
              ></b-form-input>
            </b-col>
            <b-col sm="1">
              <label for="salario">Salario:</label>
            </b-col>
             <b-col sm="5">
              <b-form-input
                id="salario"
                size="sm"
                placeholder="Digite o salario:"
                v-model="novoFuncionario.salario"
              ></b-form-input>
            </b-col>
            <b-col sm="1">
              <label for="cargp">Cargo:</label>
            </b-col>
             <b-col sm="5">
              <b-form-input
                id="cargo"
                size="sm"
                placeholder="Digite o cargo:"
                v-model="novoFuncionario.cargo"
              ></b-form-input>
            </b-col>
          </b-row>
        </b-container>
        <b-button class="mt-3" block variant="success" @click="criarNovoFuncionario"
          >Criar Funcionario</b-button
        >
        <b-button class="mt-3" block variant="danger" @click="fecharModal"
          >Fechar</b-button
        >
      </b-modal>
      <b-button class="mt-3" block variant="success" @click="deletarClinica" to="/">deletar</b-button>
    
  
  </div>
</template>

<script>

export default {
 
  async asyncData( {$axios, params} ){
    let clinicas
    try {
        clinicas = await $axios.$get(`/clinica/${params.funcionarios}`)
    } catch (e) {
        console.log(e)
    }
    console.log(JSON.stringify(clinicas))
    return{clinicas}

    
  },

  data: function(){
    return {
      showModal: false,
      novoFuncionario: {
        nome_fun:'',
        cpf: '',
        salario: '',
        cargo: '',
      },
      selecionados: [],
    }
  },
  methods: {
    async criarNovoFuncionario(event) {
      
    try {
        let dataFuncionario = await this.$axios.$post(
            `/clinica/criar_funcionario/${this.clinicas.id}`, this.novoFuncionario
        )
        if(dataFuncionario !== null){
            this.fecharModal(event)
            this.novoFuncionario = {
                nome_fun:'',
                cpf: '',
                salario: '',
                cargo: '',

            }
            this.atualizaClinicasFuncionarios();
             alert(JSON.stringify(`Funcionario para a clinica de id ${this.clinicas.id} foi criada!`));
            }else{
                throw new Error(`Funcionario para a clinica de id ${this.clinicas.id} não foi criada!`);

            }
        }
     catch (error) {
        console.log(error)
    }
    },
    async atualizaClinicasFuncionarios(){
        this.clinicas = await this.$axios.$get(`/clinica/${this.clinicas.id}`);
    },
    fecharModal(event){
        this.$bvModal.hide('modal-tarefa')
    },
    async deletarClinica(){
        this.clinicas = await this.$axios.$delete(`/clinica/deletar_clinica/${this.clinicas.id}`);
       
    }
    

  },


}
</script>

<style>

</style>