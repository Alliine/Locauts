<h1>Projeto Locauts</h1>

Nomes:  

Aline Gonçalves de Paula 

Emyle Oliveira de Souza 

Geovanna Caroline Rodrigues 

Maria Gabrielle Minnitti Honório Soares 


<br><br>

<h3>Tabela de paths/endpoints </h3>

Verbo HTTP | Caminhos (Endpoints) |Descrição 
-----------|----------------------|---------
GET        |/clinica              |Retorna todas as clinicas salvas 
POST       |/clinica/criar        |Criar uma nova clinica  
PUT        |/clinica/alterar_funcionario/{id} |Alterar um funcionário de uma clinica 
DELETE     |/clinica/deletar_funcionario/{id} |Deletar um funcionário de uma clinica 
POST       |/clinica/criar_funcionario/{id} | Criar um novo funcionário de uma clinica 
GET        |/clinica/{id}         | Retorna todos os itens de funcionarios de uma clinica 


 
<br><br>

<h3>Modelos JSON:</h3>


**Inserindo uma nova Clinica** 

{ 

“nome_Clinica”: “Clinica exemplo”,  

“endereco_Clinica”: “rua trinta”,  

“instituicao_Privada”: true,   

“telefone”: 40314444,  

“especialidade”: “fonoaudiologia”,  

“numero_alas”: 20,  

“cnpj”: “298168617”,   

“horario_atendimento”: 15  

}

<br><br>
 
 

**Inserindo um novo Funcionario**

{ 

“nome_fun”: “Alberto Fonseca”, 

“cpf”: 12359876236, 

“salario”: 1200,00, 

“cargo”: “secretario” 

} 
