---
name: proposta-comercial
description: Gera proposta comercial (orçamento) em HTML pronto pra virar PDF, no formato de documento técnico numerado (objeto, escopo, itens não considerados, disposições gerais, prazo, honorários, validade), com a marca do usuário. Vai salvando o escopo descrito como catálogo reutilizável pras próximas propostas. Use quando o usuário pedir pra montar proposta, orçamento, proposta comercial, "monta a proposta pro cliente X", "faz o orçamento desse projeto", ou quiser editar uma proposta já gerada.
---

# Proposta Comercial

Gera uma proposta comercial (orçamento) em HTML, pronta pra virar PDF (Ctrl+P), no formato
de documento técnico numerado, igual ao que um escritório de projeto ou consultoria manda
pro cliente assinar. Não é deck de apresentação nem página de vendas, é documento formal.

## Fase 0 — Logo e dados do responsável (só na primeira vez, ou se mudar)

O documento é sempre texto preto em fundo branco, igual qualquer proposta técnica formal.
A identidade do usuário entra só pela logo no topo, nada de cor nem fonte de marca.

- Procurar a pasta de marca (`Marca/`, `marca/`, `brand/`, `identidade/`) e achar o arquivo
  de logo. Abrir pra conferir se é a versão clara, que funciona em fundo branco (logo
  pensado pra fundo escuro some)
- Conferir se o arquivo tem fundo transparente (PNG com alpha). Se tiver fundo sólido (um
  retângulo branco, cinza ou de cor por trás da marca), isso aparece como uma caixa no topo
  do documento, que é branco. Nesse caso, avisar o usuário e oferecer:
  1. Se existir alguma skill de edição de imagem instalada (ex. remoção de fundo), usar pra
     gerar uma versão transparente e perguntar se pode salvar essa versão na pasta de marca
  2. Se o fundo do arquivo já for branco puro (ou bem próximo), pode seguir assim mesmo, o
     contraste contra o fundo do documento é mínimo
  3. Sem nenhuma das duas opções, avisar que vai aparecer uma caixa ao redor da logo e
     perguntar se o usuário quer seguir assim ou mandar outro arquivo
- Ler `_contexto/empresa.md` (ou `AGENTS.md`/`CLAUDE.md`) pra puxar nome do responsável
  técnico, registro profissional (CREA, CAU, CFT ou equivalente) e nome do negócio
- Mostrar o que encontrou e perguntar só o que faltou. Nunca escrever nada antes de
  confirmar

## Fase 1 — Escopo do serviço

- Perguntar o escopo do serviço pro usuário descrever com as próprias palavras: o que entra
  nesse tipo de proposta, pra qual tipo de projeto ou cliente, separado por disciplina ou
  frente de trabalho quando fizer sentido (ex. concreto armado, estrutura metálica,
  elétrico, arquitetura, consultoria)
- Checar se já existe `orcamentos/catalogo-escopo.md` na pasta do projeto
  - Existe: mostrar os itens já salvos que combinam com o que o usuário descreveu agora,
    perguntar se quer reaproveitar algum e complementar com o que for novo
  - Não existe: criar o arquivo com o que o usuário descreveu, organizado por disciplina ou
    frente de trabalho
- Toda vez que aparecer um item de escopo novo numa proposta, ele entra no catálogo
  também. O catálogo cresce sozinho com o uso, nunca precisa ser montado na mão antes de
  começar a usar a skill
- Perguntar também o que NÃO está incluso (itens não considerados). Mesma lógica: se for
  novo, também vai pro catálogo

## Fase 2 — Dados da proposta

Perguntar numa mensagem só:

1. Número da proposta (olhar o maior número já usado em `orcamentos/`, se houver, e sugerir
   o próximo; se for a primeira, perguntar de onde começar a numerar)
2. Cliente, projeto e endereço ou localização, se fizer diferença pro objeto
3. Disciplina(s) envolvida(s) (usadas no Objeto e pra agrupar o Escopo, se houver mais de
   uma)
4. Valor: único, direto, ou calculado por m² (nesse caso, pedir a metragem)
5. Forma de pagamento (parcelas, percentual de cada uma, gatilho de cada parcela: aceite da
   proposta, entrega, assinatura etc.)
6. Prazo de execução: data fixa, ou "X dias [úteis ou corridos] a partir da assinatura do
   contrato" (quando for esse caso, avisar que a data final só fecha quando o contrato for
   assinado de verdade)
7. Disposições gerais que sempre entram nesse tipo de proposta (ex. emissão de ART/RRT,
   formato de entrega dos arquivos) — reaproveitar do catálogo se já tiver, perguntar se for
   novo
8. Validade da proposta (sugestão padrão: 10 dias corridos)

Regra dura: nunca inventar valor, prazo ou condição. O que não for informado entra no
documento como `[a confirmar]`, visível, em vez de ser preenchido por dedução.

## Fase 3 — Esqueleto antes de gerar

Mostrar em bullets a estrutura da proposta, seção por seção (mesma ordem da Fase 4) com a
frase central de cada uma, e esperar aprovação do usuário antes de montar o HTML. Corrigir
o esqueleto é rápido, corrigir o documento pronto não é.

## Fase 4 — Gerar o documento

Estrutura fixa, igual a uma proposta técnica formal. Seguir essa ordem e essa numeração:

```
PROPOSTA TÉCNICA Nº {número}/{ano com 2 dígitos}        ← título, centralizado, negrito

1.) OBJETO DA PROPOSTA
Projeto referente a {disciplina(s)}, para {nome do projeto/cliente}, conforme descrição:
• Endereço: {endereço, se houver}
• Proprietário/Cliente: {nome}
• Área [estruturada/do projeto]: {metragem, se houver}

2.) ESCOPO DA PROPOSTA
Os projetos e serviços que estamos propondo são os seguintes:

[Se houver mais de uma disciplina, um subtítulo em negrito por disciplina, ex.
"Concreto armado:", seguido da lista de itens daquela disciplina. Se for só uma
disciplina, lista direta sem subtítulo.]
• {item};
• {item};

3.) ITENS NÃO CONSIDERADOS NA PROPOSTA
• {item};

4.) DISPOSIÇÕES GERAIS
{parágrafos curtos, um por disposição}

5.) PRAZO PARA EXECUÇÃO DOS SERVIÇOS
O prazo para a execução dos serviços descritos no ESCOPO DA PROPOSTA é de {prazo}.

6.) HONORÁRIOS
• O honorário para execução dos trabalhos aqui propostos é de {valor}.
• Forma de pagamento:
{parcela 1, valor, percentual, gatilho};
{parcela 2, valor, percentual, gatilho};

7.) VALIDADE DA PROPOSTA
A presente proposta tem validade de {prazo}, a partir da data de recebimento.

Sem mais, ficamos no aguardo, nos colocando à disposição para maiores esclarecimentos.

Atenciosamente,

{Nome do responsável técnico}        ← centralizado
{Registro profissional}              ← centralizado
{Nome do negócio}                    ← centralizado

{Cidade/UF}, {data por extenso ou DD/MM/AAAA}.   ← alinhado à direita
```

Regras de formatação do HTML:

- Logo centralizado no topo de cada página
- Título da proposta centralizado, negrito, logo abaixo do logo
- Cada cabeçalho numerado (`1.) OBJETO DA PROPOSTA`, `2.) ESCOPO DA PROPOSTA` etc.) em
  negrito
- Subtítulo de disciplina (quando houver mais de uma no Escopo) em negrito, sozinho na
  linha, terminado em dois pontos
- Itens de lista com `•`, cada um terminado em ponto e vírgula
- Bloco de assinatura (nome, registro, negócio) centralizado
- Linha de cidade e data alinhada à direita, por último
- Texto sempre preto sobre fundo branco, fonte neutra (ex. Helvetica/Arial), igual a
  qualquer documento técnico formal. A identidade visual do usuário não entra na cor nem na
  fonte do texto, só na logo
- Arquivo único, HTML autocontido (CSS inline), nomeado
  `orcamentos/Orçamento nº {número}_{ano} - {Cliente}.html` (criar a pasta `orcamentos/`
  se não existir)

## Fase 5 — Entregar

- Abrir o arquivo HTML pro usuário conferir antes de gerar o PDF
- Depois que o usuário aprovar o HTML, gerar o PDF automaticamente, sem pedir pra ele
  apertar Ctrl+P na mão. Usar um navegador headless (ex. Playwright/Chromium, formato A4,
  margens padrão) pra imprimir o próprio HTML direto em
  `orcamentos/Orçamento nº {número}_{ano} - {Cliente}.pdf`, no mesmo lugar e com o mesmo
  nome do HTML, só trocando a extensão
- Se não houver navegador headless disponível no ambiente (ex. Playwright/Chromium não
  instalado), avisar o usuário e perguntar se ele quer que a skill instale o que falta
  agora (ex. `npm install -D playwright` seguido de `npx playwright install chromium`,
  ajustando ao gerenciador de pacote e ao sistema operacional dele). Só instalar depois do
  "sim" explícito. Se ele preferir não instalar, seguir com Ctrl+P (ou Cmd+P no Mac) como
  alternativa manual
- Confirmar no fim que o PDF foi gerado e onde ele está salvo

## Regras

1. Nunca inventar valor, prazo ou escopo. O que faltar fica `[a confirmar]`
2. O catálogo de escopo é vivo: pergunta, salva, reaproveita. Nunca pede pro usuário montar
   um catálogo do zero antes de poder usar a skill
3. Uma proposta por cliente. Nada de reaproveitar proposta antiga só trocando o nome sem
   revisar escopo e valor
4. Seguir à risca a estrutura numerada da Fase 4. É isso que dá cara de documento formal,
   não de texto corrido
5. Abrir no navegador e olhar antes de entregar: logo claro em fundo claro não dá erro, só
   some. Se sumiu, usar a versão escura do logo ou o nome em texto
