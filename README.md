### Projeto: Cadastro de Funcionários

Este projeto é uma API RESTful desenvolvida com Spring Boot que realiza o cadastro de funcionários, permitindo operações de CRUD (Criar, Listar, Atualizar e Deletar).
Ela segue uma estrutura bem organizada com camadas (Model, Repository, DTO, Service, Controller), utilizando boas práticas de arquitetura e validações com jakarta.validation.

## Funcionalidades

A API permite:

### Cadastrar um novo funcionário (POST)
Listar todos os funcionários (GET)
Buscar funcionário por ID (GET)
Atualizar um funcionário existente (PUT)
Deletar um funcionário por ID (DELETE)

### Estrutura do Projeto
1. model/Funcionario.java

Contém a entidade JPA Funcionario, mapeada para a tabela funcionario.
O campo email possui uma restrição de unicidade no banco.

### Atributos:

id: identificador único (auto-gerado)

nome: nome do funcionário

email: e-mail do funcionário

cargo: cargo ocupado

## 2. repository/FuncionarioRepository.java

Interface que herda de JpaRepository, oferecendo métodos prontos para operações no banco de dados.
Inclui método adicional existsByEmail(String email) para verificar se o e-mail já foi cadastrado.

## 3. dto/FuncionarioRequestDto.java

Classe que representa os dados recebidos na requisição (entrada do usuário).

### Inclui validações:

@NotBlank para nome, email e cargo

@Email para validar o formato do e-mail

4. dto/FuncionarioResponseDto.java

Classe usada para retornar os dados ao cliente (resposta da API).

## Possui:

Conversor estático fromEntity(Funcionario) para transformar a entidade em DTO

Método toEntity() para converter de volta, se necessário

5. exception/RecursoNaoEncontradoException.java

Classe de exceção personalizada lançada quando o funcionário buscado não é encontrado no banco.

6. service/FuncionarioService.java

Camada que concentra a lógica de negócio.

## Métodos:

criar(): cria novo funcionário (verifica se o e-mail já existe)

listarTodos(): retorna lista de todos os funcionários

buscarPorId(): busca funcionário por ID

atualizar(): atualiza os dados do funcionário

deletar(): exclui um funcionário por ID

7. controller/FuncionarioController.java

Controlador REST responsável por receber e responder às requisições.

## Rotas:

POST /api/funcionarios

GET /api/funcionarios

GET /api/funcionarios/{id}

PUT /api/funcionarios/{id}

DELETE /api/funcionarios/{id}

Utiliza @Valid para aplicar validações nos DTOs de entrada.

### Tecnologias Utilizadas

Java 21+

Spring Boot

Spring Web

Spring Data JPA

Jakarta Validation

Banco de dados relacional (ex: MySQL, PostgreSQL, H2)

Maven

### Como Executar

Clone o repositório:

git clone https://github.com/Thiagoho/Desafio----Cadastro-Funcionario.git
cd cadastro_funcionarios


Configure o application.properties com seu banco de dados (exemplo com H2 ou MySQL)

Execute a aplicação:

./mvnw spring-boot:run
### Validações e Tratamento de Erros

Caso o e-mail já exista, retorna erro 400 - E-mail já cadastrado

Se o ID não for encontrado, lança RecursoNaoEncontradoException com status 404

Campos obrigatórios validados com mensagens personalizadas

Teste os endpoints com Insomnia, Postman ou Swagger.

## Exemplos de Requisições
GET /api/funcionarios<br>
Retorna todos os funcionários cadastrados.<br>
POST /api/funcionarios<br>
```json
{
  "nome": "Maria Silva",
  "email": "maria@empresa.com",
  "cargo": "Analista de RH"
}
