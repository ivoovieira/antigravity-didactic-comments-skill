---
name: explicador-didatico
description: >-
  Padroniza a formatação e a documentação didática de código-fonte.
  Aplica contratos iniciais de função/módulo, divisão visual por blocos lógicos
  e comentários conceituais focados no 'porquê' e em regras pedagógicas.
---

# Explicador Didático: Padrão Pedagógico de Código e Documentação

Esta skill orienta o modelo a transformar código bruto ou monolítico em código altamente legível, estruturado e autoexplicativo, ideal para materiais didáticos, tutoriais técnicos, onboarding de desenvolvedores e code reviews conceituais.

---

## 1. Diretrizes Fundamentais

Ao formatar, comentar ou gerar código sob esta skill, siga rigorosamente os três pilares:

### Pilar 1: Contrato Inicial Obrigatório
Toda função, classe, método relevante ou módulo deve iniciar com um cabeçalho estruturado delimitado por barras duplas (`// =====` ou `# =====`), contendo:
- **IDENTIFICADOR/TIPO**: Nome da entidade e seu propósito semântico didático.
- **Objetivo**: O que a rotina resolve conceitualmente, evitando tautologias.
- **Entrada / Parâmetros**: Tipos esperados, nomes e restrições de cada argumento.
- **Retorno**: Tipo e significado do valor retornado em cada cenário.
- **Complexidade / Pré-condições** (opcional, quando aplicável): Complexidade assintótica ou premissas exigidas.

### Pilar 2: Divisão Visual por Blocos Lógicos
- Divida o fluxo interno em seções numeradas e nomeadas logicamente.
- Utilize linhas de separação limpas (ex: `// ---------------------------------------------------------------`).
- Agrupe instruções que colaboram para o mesmo objetivo (validação, transformação, execução, fallback).
- Mantenha espaçamento vertical uniforme (1 linha em branco antes e depois de cada divisória).

### Pilar 3: Comentários Conceituais ("O Porquê", não "O Quê")
- **Elimine o óbvio**: Não comente `i++ // incrementa i` ou `return true // retorna verdadeiro`.
- **Foque no fundamento**: Explique por que aquela decisão foi tomada, particularidades de operadores (`>=`, `===`, coalescência nula), armadilhas comuns (edge cases, mutabilidade) e impacto arquitetural.
- **Destaque Pedagógico**: Use marcações claras como `// Nota didática:` para explicitar sutilezas da linguagem ou comportamento de runtime.

---

## 2. Exemplo Canônico de Referência

### Entrada (Código Bruto)
```javascript
function checkAge(user) {
  if(user.age >= 18) {
    return true;
  }
  return false;
}
```

### Saída Obrigatória (Formatado Didaticamente)
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

## 3. Adaptação Multi-Linguagem

Mantenha a coerência de sintaxe da linguagem-alvo mantendo a mesma semântica visual:

- **JavaScript / TypeScript / C / C++ / C# / Java / PHP / Rust / Go / Kotlin**:
  - Delimitador de Contrato: `// =================================================================`
  - Delimitador de Bloco: `// ---------------------------------------------------------------`
- **Python / Shell / Ruby**:
  - Delimitador de Contrato: `# =================================================================`
  - Delimitador de Bloco: `# ---------------------------------------------------------------`
- **SQL**:
  - Delimitador de Contrato: `-- =================================================================`
  - Delimitador de Bloco: `-- ---------------------------------------------------------------`

---

## 4. Checklist de Aplicação

Antes de entregar a refatoração ou explicação ao usuário, valide:
1. [ ] Há um cabeçalho de contrato no topo da rotina?
2. [ ] Cada fase do algoritmo (validações, processamento, retorno) está visualmente separada por divisórias numeradas?
3. [ ] Os comentários explicam a razão e a mecânica das decisões, sem parafrasear a sintaxe?
4. [ ] Foram adicionadas notas didáticas em pontos de atenção técnica (ex: operadores de borda, tratamento de nulos)?
