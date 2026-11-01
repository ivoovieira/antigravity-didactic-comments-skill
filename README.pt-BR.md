# Antigravity Skill: Explicador Didático (`explicador-didatico`)

> 🌐 **Language / Idioma**: [🇺🇸 English Version (README.md)](README.md) | **🇧🇷 Português (Brasil)**

Custom Skill para o **Antigravity** focada em engenharia reversa de código para fins pedagógicos, padronização visual por blocos lógicos e documentação contextual com foco no **"porquê"** (causa-raiz e mecânica da linguagem) em vez do óbvio.

---

## 🎯 Propósito da Skill

Em ambientes educacionais, documentações técnicas, treinamentos corporativos e processos de onboarding, o código gerado ou mantido por desenvolvedores muitas vezes peca por dois extremos:
1. **Ausência total de documentação**: Dificulta a compreensão do fluxo lógico por iniciantes ou novos membros do time.
2. **Comentários redundantes e óbvios**: Comentários como `i++ // incrementa i`, que apenas poluem o código sem agregar valor conceitual.

A skill **`explicador-didatico`** estabelece um padrão rigoroso e reproduzível baseado em três pilares:
- **Contrato Inicial Estruturado**: Define no topo de cada rotina o objetivo pedagógico, tipos e contratos de parâmetros e de retornos.
- **Divisórias Visuais por Fases Lógicas**: Demarcação clara de blocos lógicos (`Validação`, `Processamento`, `Fallback / Retorno`) com espaçamento padronizado.
- **Comentários Conceituais**: Explicações focadas nas regras de negócio, idiomatismos de linguagem, complexidade, edge cases e notas didáticas.

---

## 📂 Estrutura de Arquivos

```
.
├── .agents/
│   └── skills/
│       └── explicador-didatico/
│           └── SKILL.md       # Definição formal e diretrizes da skill
└── README.md                  # Documentação e guia de uso
```

---

## 🚀 Como Instalar e Utilizar no Antigravity

O sistema de extensão do Antigravity suporta dois níveis de escopo: **Workspace (Local)** e **Global (Máquina)**.

### Opção 1: Escopo do Workspace (Recomendado para Projetos Específicos)
Mantenha a pasta `.agents/` na raiz do seu repositório:
```
meu-projeto/
└── .agents/
    └── skills/
        └── explicador-didatico/
            └── SKILL.md
```
* **Comportamento**: O Antigravity carrega a skill automaticamente ao trabalhar no repositório. O time compartilha a configuração via controle de versão (Git).

### Opção 2: Escopo Global (Disponível em Qualquer Projeto na Máquina)
Copie o diretório da skill para o diretório de configuração global do Antigravity:

- **Linux / macOS**:
  ```bash
  mkdir -p ~/.gemini/config/skills/
  cp -r .agents/skills/explicador-didatico ~/.gemini/config/skills/
  ```

- **Windows (PowerShell)**:
  ```powershell
  $target = "$HOME\.gemini\config\skills\explicador-didatico"
  New-Item -ItemType Directory -Force -Path $target
  Copy-Item -Path ".\.agents\skills\explicador-didatico\*" -Destination $target -Recurse -Force
  ```

---

## 🤖 Quais Agentes Podem Ser Usados? (Explicação e Exemplos)

O ecossistema do Antigravity opera sob um modelo de orquestração multi-agente e disclosure progressivo. Veja como diferentes agentes tiram proveito desta skill:

### 1. Agente Principal (Pair Programmer / Coding Assistant)
* **Perfil**: O agente primário do chat com ferramentas completas de leitura, escrita e execução.
* **Quando usar**: Durante sessões ativas de desenvolvimento, refatoração pontual de arquivos abertos ou ao pedir para o modelo explicar um trecho de código durante a programação em par.
* **Exemplo de Prompt**:
  > *"Ative a skill explicador-didatico e refatore a função `calculateTax` no arquivo `services/tax.ts` aplicando o contrato inicial e divisórias limpas."*

### 2. Subagente `self` (Trabalho Isolado e Refatorações em Lote)
* **Perfil**: Um clone com o mesmo contexto de ferramentas do agente principal, porém executando em uma thread/sessão isolada.
* **Quando usar**: Refatorar um módulo inteiro ou uma biblioteca inteira de utilitários para gerar material didático sem poluir o histórico ou estourar a janela de contexto da conversa principal.
* **Exemplo de Invocação**:
  ```python
  invoke_subagent(
      TypeName="self",
      Role="Pedagogical Refactorer",
      Prompt="Percorra todos os arquivos em src/algorithms/ e aplique a skill explicador-didatico em cada função exportada."
  )
  ```

### 3. Subagente `research` (Mapeamento e Extração Conceitual)
* **Perfil**: Subagente em sandbox somente leitura, projetado para analisar repositórios grandes e documentações sem modificar arquivos.
* **Quando usar**: Analisar códigos legados complexos ou bibliotecas externas para descobrir quais regras implícitas e fluxos de borda precisam ser explicados pedagogicamente antes de iniciar a refatoração.
* **Exemplo de Invocação**:
  ```python
  invoke_subagent(
      TypeName="research",
      Role="Code Analyst",
      Prompt="Analise a engine de autorização em src/auth/ e elabore um resumo conceitual das regras de validação para orientar a documentação didática."
  )
  ```

### 4. Subagente Customizado (`pedagogical-reviewer`)
* **Perfil**: Agente especializado definido sob demanda via `define_subagent` ou via declaração em `.agents/rules/` ou plugins.
* **Quando usar**: Integração em esteiras de code review ou auditorias de qualidade para garantir que novos commits atendam aos padrões pedagógicos.
* **Exemplo de Definição**:
  ```python
  define_subagent(
      Name="pedagogical-reviewer",
      Description="Audita funções em PRs garantindo contrato inicial e comentários de causa-raiz.",
      SystemPrompt="Você é um auditor pedagógico de código. Verifique se o código possui contrato inicial, divisórias de seções e comentários explicativos conceituais de acordo com a skill explicador-didatico."
  )
  ```

---

## 🔍 Exemplo: Antes x Depois

### Entrada Original (Código Bruto)
```javascript
function checkAge(user) {
  if(user.age >= 18) {
    return true;
  }
  return false;
}
```

### Saída Formatada pela Skill
```javascript
// =================================================================
// FUNÇÃO: Verificação de Maioridade Pedagógica
// Objetivo: Demonstrar o uso de estruturas condicionais (if/else)
// Entrada: Objeto 'user' contendo a propriedade numérica 'age'
// Retorno: Booleano (true para liberado, false para bloqueado)
// =================================================================

function checkAge(user) {
  
  // ---------------------------------------------------------------
  // 1. VALIDAÇÃO DA REGRA DE NEGÓCIO
  // ---------------------------------------------------------------
  // Verificamos a idade comparando com a constante de maioridade (18).
  // Nota didática: O operador `>=` inclui o número 18 na validação.
  if (user.age >= 18) {
    return true; // Retorna imediatamente e interrompe a execução se for verdadeiro
  }
  
  // ---------------------------------------------------------------
  // 2. FLUXO DE RETORNO PADRÃO (FALLBACK)
  // ---------------------------------------------------------------
  // Se o programa chegou até aqui, significa que a condição do 'if' falhou.
  // Portanto, o usuário é menor de idade.
  return false;
}
```

---

## 📄 Licença

Distribuído sob a licença MIT. Consulte `LICENSE` para mais informações.
