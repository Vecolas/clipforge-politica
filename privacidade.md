---
layout: default
title: Política de Privacidade
---

# Política de Privacidade — ClipForge

**Última atualização:** 6 de outubro de 2026

O ClipForge é uma ferramenta de edição que roda **inteiramente no computador
do próprio usuário**. Não há servidor, não há conta de serviço e não há
transmissão de dados para a operadora desta ferramenta — porque não existe
operadora com infraestrutura: o programa é executado localmente por quem o
instalou.

Este documento existe para cumprir a exigência dos [Termos de Serviço dos
Serviços de API do YouTube][tos] e descreve exatamente o que o programa faz
com dados.

## 1. Quem trata os dados

O próprio usuário, no computador dele. Quem instala e executa o ClipForge é o
controlador dos dados que o programa manipula. O autor do software não recebe,
não armazena e não tem acesso a nenhum desses dados.

## 2. Que dados o programa acessa

**Do YouTube, por meio da API:**

| Dado | Para quê | Onde fica |
|---|---|---|
| Token de acesso e de renovação (OAuth) | Autorizar o envio de vídeo e capa | Arquivo local, em `data/contas/<id>.json` |
| Nome e identificador do canal | Mostrar na interface de qual canal se trata | Banco local SQLite |
| Identificador do vídeo enviado | Ligar o clipe publicado às métricas | Banco local SQLite |
| Métricas do próprio canal (visualizações, retenção, CTR) | Relatório de desempenho e recalibração dos pesos | Banco local SQLite |

**Do computador do usuário:** arquivos de vídeo que ele mesmo indica,
transcrições geradas localmente e os clipes produzidos.

O programa **não** acessa dados de canais de terceiros, não lê comentários,
não gerencia assinaturas e não altera configurações do canal além de enviar o
vídeo que o usuário mandou enviar.

## 3. Escopos de autorização solicitados

| Escopo | Por que é necessário |
|---|---|
| `youtube.upload` | Enviar o arquivo de vídeo e a capa |
| `youtube.readonly` | Ler o nome do canal autorizado, para identificá-lo na interface |
| `yt-analytics.readonly` | Ler métricas dos vídeos do próprio usuário (opcional; só se ele usar o relatório) |

Escopos mais amplos como `youtube` e `youtube.force-ssl` **não** são pedidos:
eles dariam permissão de leitura e escrita sobre todo o canal, e a ferramenta
não precisa disso.

## 4. Onde os dados ficam e por quanto tempo

Tudo em disco local, nos diretórios configurados em `config.toml`:

- tokens de autorização: `data/contas/`
- banco de dados: o caminho de `[paths].db_file`
- mídia e artefatos: o caminho de `[paths].data_dir`

Os dados permanecem até o usuário apagá-los. Não há cópia remota, backup em
nuvem nem telemetria.

## 5. Com quem os dados são compartilhados

Com ninguém. As únicas requisições de rede que o programa faz são:

- para a **API do YouTube**, com o token do próprio usuário, para enviar vídeo
  e ler métricas dele mesmo;
- para o **Wayback Machine** (`archive.org`), para arquivar a página pública
  que documenta a permissão de uso de conteúdo de terceiros — enviando apenas
  o endereço dessa página pública;
- para baixar, uma única vez, os modelos de detecção facial usados no
  recorte vertical.

Nenhuma dessas requisições carrega dado pessoal do usuário além do necessário
para a própria operação.

## 6. Como revogar o acesso

Pelo programa: aba **Uploads** → **Revogar**, ou `clipforge contas revogar <id>`.
A revogação apaga o arquivo de token do disco.

Pela conta Google, de forma independente do programa:
[myaccount.google.com/permissions](https://myaccount.google.com/permissions).

## 7. Dados de API do YouTube

Esta ferramenta usa os Serviços de API do YouTube. Ao usá-la, o usuário
concorda com os [Termos de Serviço dos Serviços de API do YouTube][tos] e fica
sujeito à [Política de Privacidade do Google][privacidade-google].

Dados obtidos da API do YouTube são usados apenas para as funções descritas
acima, ficam somente no computador do usuário e são removidos quando ele apaga
os arquivos do programa ou revoga a autorização.

## 8. Contato

Este é um projeto pessoal. Dúvidas e pedidos relacionados a dados: abra uma
issue em
[github.com/Vecolas/clipforge-politica](https://github.com/Vecolas/clipforge-politica/issues).

[tos]: https://developers.google.com/youtube/terms/api-services-terms-of-service
[privacidade-google]: https://policies.google.com/privacy
