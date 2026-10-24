---
name: proposta-comercial
description: Gera proposta comercial (orçamento) em HTML de página única, simples, no padrão visual da marca do usuário, a partir de uma conversa sobre o serviço. Vai salvando o escopo descrito como catálogo reutilizável pras próximas propostas. Use quando o usuário pedir pra montar proposta, orçamento, proposta comercial, "monta a proposta pro cliente X", "faz o orçamento desse projeto", ou quiser editar uma proposta já gerada.
---

# Proposta Comercial

Gera uma proposta comercial (orçamento) em HTML de página única, simples, no mesmo padrão
visual dos documentos do usuário. O cliente abre e lê, do jeito que já é de praxe mandar
proposta por link ou PDF. Não é deck de apresentação nem página de vendas, é documento.

## Fase 0 — Marca (só na primeira vez, ou se mudar)

- Procurar a pasta de marca (`Marca/`, `marca/`, `brand/`, `identidade/`) e o
  `design-guide.md` dentro dela
- Ler `_contexto/empresa.md` (ou `AGENTS.md`/`CLAUDE.md`) pra puxar nome do responsável
  técnico, registro profissional e nome do negócio
- Achar o arquivo de logo e abrir pra conferir se é a versão clara, que funciona em fundo
  branco (documento é sempre fundo branco, logo pensado pra fundo escuro some)
- Mostrar o que encontrou e perguntar só o que faltou. Nunca escrever nada antes de
  confirmar

## Fase 1 — Escopo do serviço

- Perguntar o escopo do serviço pro usuário descrever com as próprias palavras: o que entra
  nesse tipo de proposta, pra qual tipo de projeto ou cliente
- Checar se já existe `orcamentos/catalogo-escopo.md` na pasta do projeto
  - Existe: mostrar os itens já salvos que combinam com o que o usuário descreveu agora,
    perguntar se quer reaproveitar algum e complementar com o que for novo
  - Não existe: criar o arquivo com o que o usuário descreveu, organizado por tipo de
    serviço
- Toda vez que aparecer um item de escopo novo numa proposta, ele entra no catálogo
  também. O catálogo cresce sozinho com o uso, nunca precisa ser montado na mão antes de
  começar a usar a skill
- Perguntar também o que NÃO está incluso (itens não considerados) e se existe alguma
  disposição geral que costuma entrar nesse tipo de proposta (prazo de resposta do cliente,
  forma de revisão, validade padrão). Mesma lógica: se for novo, também vai pro catálogo

## Fase 2 — Dados da proposta

Perguntar numa mensagem só:

1. Cliente (nome, projeto, cidade se fizer diferença)
2. Valor: único, direto, ou calculado por m² (nesse caso, pedir a metragem)
3. Prazo de execução: data fixa, ou "X dias a partir da assinatura do contrato" (quando for
   esse caso, avisar que a data final só fecha quando o contrato for assinado de verdade)
4. Validade da proposta (sugestão padrão: 7 dias)
5. Forma de pagamento

Regra dura: nunca inventar valor, prazo ou condição. O que não for informado entra no
documento como `[a confirmar]`, visível, em vez de ser preenchido por dedução.

## Fase 3 — Esqueleto antes de gerar

Mostrar em bullets a estrutura da proposta (seção por seção, com a frase central de cada
uma) e esperar aprovação do usuário antes de montar o HTML. Corrigir o esqueleto é rápido,
corrigir o documento pronto não é.

## Fase 4 — Gerar o documento

- Layout de documento, não de página de vendas: logo centralizado no topo, título, corpo
  de texto organizado por seção (Objeto, Escopo, Itens não considerados, Valor, Prazo,
  Forma de pagamento, Disposições gerais, Validade), assinatura no fim
- Cor e fonte vêm do `design-guide.md` (ou um fallback neutro, se a marca ainda não tiver
  sido preenchida)
- Logo puxado direto do arquivo encontrado na Fase 0
- Arquivo único, HTML autocontido (CSS inline), salvo em
  `orcamentos/proposta-{cliente}-{AAAA-MM-DD}.html` (criar a pasta `orcamentos/` se não
  existir)

## Fase 5 — Entregar

- Abrir o arquivo no navegador pro usuário conferir
- Lembrar que Ctrl+P (ou Cmd+P no Mac) salva como PDF direto do navegador, pra mandar por
  WhatsApp ou e-mail sem precisar de mais nenhuma ferramenta

## Regras

1. Nunca inventar valor, prazo ou escopo. O que faltar fica `[a confirmar]`
2. O catálogo de escopo é vivo: pergunta, salva, reaproveita. Nunca pede pro usuário montar
   um catálogo do zero antes de poder usar a skill
3. Uma proposta por cliente. Nada de reaproveitar proposta antiga só trocando o nome sem
   revisar escopo e valor
4. Documento simples: sem seção grande de "quem somos", sem linguagem de página de vendas.
   É proposta de prestação de serviço, não material de marketing
5. Abrir no navegador e olhar antes de entregar: logo claro em fundo claro não dá erro, só
   some. Se sumiu, usar a versão escura do logo ou o nome em texto
