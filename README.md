# SIGER - Sistema Integrado de Gestão de Empréstimos e Reservas

> Projeto desenvolvido para a disciplina de **Análise Orientada a Objetos e Projeto Arquitetural**.

## 📖 Sobre o Projeto

O **SIGER (Sistema Integrado de Gestão de Empréstimos e Reservas)** é uma solução destinada ao gerenciamento de recursos institucionais, permitindo o controle centralizado de reservas, empréstimos, devoluções e auditoria de equipamentos e ambientes.

Atualmente, muitas instituições realizam esse processo manualmente através de planilhas e registros dispersos, o que aumenta a ocorrência de conflitos de agendamento, perdas de controle e dificuldades de rastreamento.

O SIGER foi projetado para automatizar e organizar esse processo, garantindo maior eficiência, segurança e rastreabilidade.

---

## 🎯 Objetivos

- Centralizar a gestão dos recursos institucionais.
- Controlar empréstimos e reservas.
- Reduzir conflitos de agendamento.
- Garantir rastreabilidade das operações.
- Facilitar auditorias e aplicação de penalidades.

---

## 🏢 Recursos Gerenciados

O sistema permitirá o gerenciamento dos seguintes recursos:

- 💻 Notebooks
- 📱 Tablets
- 📽️ Projetores
- 📷 Câmeras
- 🏫 Laboratórios
- 🏢 Salas de Reunião

---

# 👥 Atores do Sistema

## Solicitante

Representa:

- Alunos
- Professores
- Colaboradores

Responsável por:

- Consultar disponibilidade
- Solicitar reservas
- Solicitar empréstimos

---

## Administrador

Responsável por:

- Aprovar solicitações
- Rejeitar solicitações
- Gerenciar usuários
- Gerenciar recursos
- Controlar retiradas e devoluções
- Aplicar penalidades
- Consultar auditorias

---

# ✅ Requisitos Funcionais

## RF01 - Gerenciar Usuários

O sistema deve permitir:

- Cadastro de usuários
- Alteração de dados
- Inativação de usuários
- Definição de perfis de acesso

### Critérios de Aceitação

- Criar usuários
- Atualizar usuários
- Inativar usuários
- Associar perfis

---

## RF02 - Consultar Disponibilidade de Recursos

O sistema deve permitir verificar a disponibilidade de recursos em datas e horários específicos.

### Critérios de Aceitação

- Exibir recursos disponíveis
- Exibir recursos indisponíveis
- Filtrar por período

---

## RF03 - Solicitar Reserva de Recursos

O sistema deve permitir registrar reservas de recursos institucionais.

### Critérios de Aceitação

- Selecionar recurso
- Informar período
- Registrar solicitação

---

## RF04 - Solicitar Empréstimo de Equipamentos

O sistema deve permitir solicitar empréstimos de equipamentos.

### Critérios de Aceitação

- Escolher equipamento
- Informar período de uso
- Gerar protocolo

---

## RF05 - Avaliar Solicitações

O administrador deve poder aprovar ou rejeitar solicitações.

### Critérios de Aceitação

- Aprovar solicitação
- Rejeitar solicitação
- Registrar justificativa

---

## RF06 - Controlar Retirada e Devolução

O sistema deve registrar a entrega e a devolução dos recursos.

### Critérios de Aceitação

- Registrar retirada
- Registrar devolução
- Atualizar status

---

## RF07 - Gerenciar Penalidades

O sistema deve controlar atrasos e aplicar penalidades.

### Critérios de Aceitação

- Detectar atraso
- Registrar penalidade
- Bloquear novas solicitações quando necessário

---

## RF08 - Registrar Auditoria e Histórico

O sistema deve armazenar o histórico das ações realizadas.

### Critérios de Aceitação

- Registrar data e hora
- Registrar usuário responsável
- Consultar histórico

---

# 🔒 Requisitos Não Funcionais

| Código | Descrição |
|----------|----------|
| RNF01 | Responder consultas em até 3 segundos |
| RNF02 | Utilizar autenticação por login e senha |
| RNF03 | Disponibilidade mínima de 99% |
| RNF04 | Interface responsiva e intuitiva |
| RNF05 | Registro completo para auditoria |

# 🔒 Regras de Negócio e Restrições

RN01: Um recurso não poderá ser reservado ou emprestado em períodos conflitantes.

RN02: Somente usuários ativos poderão realizar solicitações no sistema.

RN03: Solicitações de recursos específicos exigirão aprovação prévia do Administrador.

RN04: Atrasos na devolução gerarão penalidades e bloqueio de novas solicitações até a regularização.
---

### 📋 Diagrama de Casos de Uso
## Caso de Uso: Solicitar Empréstimo

- Ator: Solicitante

- Fluxo Principal: 1. Solicitante seleciona um recurso. 2. Informa período de uso. 3. Sistema valida a disponibilidade. 4. Sistema registra o empréstimo e emite protocolo.

- Fluxo Alternativo: Se o recurso estiver indisponível no período, o sistema exibe mensagem de erro e solicita novas datas.

## Caso de Uso: Aprovar Solicitação

- Ator: Administrador

- Fluxo Principal: 1. Administrador acessa solicitações pendentes. 2. Seleciona um pedido. 3. Clica em aprovar. 4. Sistema atualiza o status para "Aprovado" e notifica o solicitante.

- Fluxo Alternativo: Se rejeitar, o sistema exige uma justificativa, muda o status para "Rejeitado" e libera o recurso na agenda.

```mermaid
flowchart TD

Solicitante([Solicitante])
Administrador([Administrador])

UC1((Consultar Disponibilidade))
UC2((Solicitar Reserva))
UC3((Solicitar Empréstimo))
UC4((Aprovar Solicitação))
UC5((Rejeitar Solicitação))
UC6((Registrar Retirada))
UC7((Registrar Devolução))
UC8((Gerenciar Usuários))
UC9((Gerenciar Recursos))
UC10((Consultar Auditoria))

Solicitante --> UC1
Solicitante --> UC2
Solicitante --> UC3

Administrador --> UC4
Administrador --> UC5
Administrador --> UC6
Administrador --> UC7
Administrador --> UC8
Administrador --> UC9
Administrador --> UC10
```
# 📊 Diagrama de Classes

```mermaid
classDiagram
    class Usuario {
        - int id
        - String nome
        - String email
        - String senha
        - String perfil
        + solicitarEmprestimo()
        + consultarHistorico()
    }
    
    class Solicitacao {
        - int id
        - DateTime data
        - String status
        - String tipo
        + aprovar()
        + rejeitar()
    }
    
    class Auditoria {
        - int id
        - DateTime dataHora
        - String acao
        - String usuario
        + registrarLog()
    }
    
    class Recurso {
        - int id
        - String nome
        - String categoria
        - String status
        + verificarDisponibilidade()
    }
    
    class Emprestimo {
        - int id
        - DateTime dataRetirada
        - DateTime dataDevolucao
        - String status
        + calcularAtraso()
        + registrarDevolucao()
    }

    Usuario "1" --> "*" Solicitacao : realiza
    Usuario "1" --> "*" Auditoria : gera
    Solicitacao "*" --> "1" Recurso : aloca
    Solicitacao "1" --> "0..1" Emprestimo : transforma-se em
```
---

# 🏛️ Justificativa dos Atores

O modelo foi simplificado para utilizar apenas dois atores:

### Solicitante

Representa qualquer usuário que deseja reservar ou emprestar recursos.

### Administrador

Representa o responsável por todas as operações administrativas do sistema, incluindo aprovações, gestão de recursos, auditoria e penalidades.

Essa abordagem reduz a complexidade do modelo sem comprometer os requisitos de negócio.

---

# Justificativa de Responsabilidades (Padrões GRASP)

1.Emprestimo (Information Expert): A classe possui as datas de retirada e devolução, logo é a especialista responsável por calcular se há atraso.

2.Usuario (Creator): O Usuário fornece os dados principais da solicitação, portanto, tem a responsabilidade de criar (instanciar) as Solicitações.

3.Recurso (High Cohesion): Mantém alta coesão ao lidar apenas com os dados físicos do equipamento, delegando as regras de data para a classe Emprestimo.

4.SistemaController (Controller): Uma classe controladora (não visível no domínio base) será usada para receber requisições da interface e delegar às classes corretas.

5.Auditoria (Low Coupling): Separar a auditoria em uma classe própria diminui o acoplamento, evitando que as classes de negócio fiquem cheias de códigos de log.

---

# Aplicação de SOLID e Padrões de Projeto

- Princípio SOLID aplicado (SRP): O Princípio da Responsabilidade Única foi aplicado na separação entre as regras de negócio de Emprestimo e a gravação de logs na classe Auditoria. Nenhuma classe acumula funções que não sejam de sua natureza.

- Padrão Proposto 1 - Strategy: Como as políticas de penalidade por atraso podem variar, o padrão Strategy será utilizado para criar uma interface de cálculo de penalidade, permitindo alternar entre suspensão ou multa sem alterar a classe Emprestimo.

- Padrão Proposto 2 - Factory Method: Devido à diversidade de recursos (notebooks, laboratórios, etc.), uma Factory será usada para instanciar as subclasses corretas de recursos no momento do cadastro, encapsulando a complexidade da criação.


# 📌 Conclusão

O SIGER foi projetado para oferecer uma solução centralizada para controle de recursos institucionais, permitindo gerenciamento eficiente de reservas, empréstimos, auditorias e penalidades.

A proposta busca aumentar a organização operacional, reduzir conflitos de uso dos recursos e melhorar a rastreabilidade das informações dentro da instituição.
