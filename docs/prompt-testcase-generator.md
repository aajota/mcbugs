# CRIAÇÃO DE CASOS DE TESTE FUNCIONAIS

## Objetivo

Atue como um Analista de Qualidade (QA) Sênior especialista em testes funcionais.

Analise completamente o sistema **McBugs** e gere uma documentação completa de Casos de Teste Funcionais baseada nas funcionalidades encontradas.

## Regras Gerais

* Realizar análise completa de todas as funcionalidades disponíveis.
* Identificar regras de negócio.
* Criar cenários positivos, negativos e alternativos.
* Criar cenários para validações de campos.
* Criar cenários para permissões de acesso.
* Criar cenários para mensagens de erro e sucesso.
* Criar cenários para filtros, consultas e paginações.
* Não avaliar performance.
* Não criar testes automatizados.
* Não gerar código de automação.

## Formato Obrigatório

Toda documentação deve ser gerada em **Markdown (.md)**.

Os arquivos devem ser criados na pasta:

```text
/docs
```

Exemplos:

```text
/docs/login.md
/docs/chamados.md
/docs/usuarios.md
/docs/relatorios.md
```

## Estrutura do Documento Markdown

Cada caso de teste deve seguir exatamente o modelo abaixo:

```markdown
# Casos de Teste - [Nome da Funcionalidade]

## CT001 - Nome do Caso de Teste

### Objetivo

Descrever claramente o objetivo do teste.

### Pré-Condições

- Usuário autenticado
- Dados previamente cadastrados

### Massa de Teste

| Campo | Valor |
|---------|---------|
| Exemplo | Teste |

### Passos

| ID | Ação | Resultado Esperado |
|----|--------|-------------------|
| 1 | Acessar a funcionalidade | Funcionalidade carregada com sucesso |
| 2 | Executar ação | Resultado esperado obtido |

### Pós-Condição

Estado esperado após execução.

### Prioridade

Alta

### Severidade

Alta
```

## Cobertura Obrigatória

Para cada funcionalidade encontrada, criar casos de teste contemplando:

* Fluxo principal (Happy Path)
* Fluxos alternativos
* Fluxos negativos
* Campos obrigatórios
* Campos opcionais
* Valores inválidos
* Valores limites
* Inclusão de registros
* Alteração de registros
* Exclusão de registros
* Consultas
* Filtros
* Ordenações
* Paginação
* Upload de arquivos
* Download de arquivos
* Controle de acesso
* Mensagens de erro
* Mensagens de sucesso

## Critérios de Qualidade

* Não criar casos genéricos.
* Criar cenários detalhados e executáveis.
* Numerar sequencialmente os testes (CT001, CT002, CT003...).
* Utilizar linguagem profissional de QA.
* Garantir rastreabilidade dos testes.
* Maximizar a cobertura funcional.

## Resultado Esperado

Gerar arquivos Markdown completos na pasta `/docs`, organizados por módulo ou funcionalidade, contendo uma suíte de testes funcionais pronta para uso por equipes de QA e homologação.
