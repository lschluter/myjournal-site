---
layout: default
title: Política de Privacidade
---

# Política de Privacidade

- **Data de vigência:** 4 de setembro de 2026
- **Aplica-se a:** MyJournal para Android (`br.com.schluter.myjournal`)
- **Desenvolvedor:** Leonardo Schluter Leite
- **Contato de privacidade:** lschluterleite@gmail.com
- **Versão do aviso no app:** 2 (veja [Mudanças nesta política](#mudancas-nesta-politica))
- **Also available in:** [English](https://lschluter.github.io/myjournal-site/privacy/)

O MyJournal é um diário de voz e texto. Foi feito por uma pessoa só, e não tem servidor, não tem
sistema de contas e não tem analytics. Esta política descreve o que o app realmente faz, como está
implementado — não o que ele pretende fazer.

## Versão curta

- Seu diário fica **no seu celular**, em um banco de dados criptografado.
- A fala é transcrita **no seu dispositivo**. O áudio nunca é gravado em arquivo e nunca é enviado.
- O desenvolvedor não recebe **nenhum dado seu** — não existe servidor para recebê-los.
- O texto do diário só é enviado a um provedor de IA **se você ativar isso explicitamente**, e é
  cobrado na **sua própria** conta, não na do desenvolvedor.

## O que o app armazena, e onde

Tudo abaixo é armazenado apenas no armazenamento privado do app, no seu dispositivo.

| Dado | Finalidade | Retenção |
|---|---|---|
| Entradas do diário (digitadas ou transcritas) | O diário em si | Até você excluí-las |
| TODOs, inclusive os gerados por IA | O recurso de TODOs | Até você excluí-las |
| Sua chave de API do OpenRouter | Autenticar suas próprias requisições de IA | Até você excluí-la ou apagar os dados do app |
| Configurações (tema, idioma, bloqueio do app, modelo escolhido) | Preferências | Até você apagar os dados do app |
| Seu registro de consentimento de nuvem | Comprovar que o consentimento foi concedido, e para qual versão deste aviso | Até você apagar os dados do app |

O banco de dados do diário é criptografado com SQLCipher (AES-256). A chave de criptografia é
gerada aleatoriamente no seu dispositivo, protegida pelo Android Keystore, e nunca sai do
dispositivo. Sua chave de API e o registro de consentimento ficam em preferências criptografadas
apoiadas no mesmo Keystore.

O backup automático em nuvem do Android e a transferência entre dispositivos estão **desativados**
(`allowBackup="false"`), então seu diário não é copiado para a sua conta Google.

## Microfone e fala

O app pede a permissão de **microfone** para transcrever em texto o que você fala.

- A transcrição roda **no seu dispositivo**, usando o reconhecimento de fala on-device do Android.
  É por isso que o app exige Android 13 (API 33) ou superior — a API exclusivamente on-device não
  existe antes disso.
- **O áudio nunca é gravado em arquivo e nunca é transmitido.** Só o texto resultante é guardado,
  como uma entrada do diário que você pode ver e excluir.
- Se o reconhecimento on-device não estiver disponível no seu aparelho, o app **avisa você e
  para**. Ele não recorre silenciosamente a um reconhecedor pela rede.
- Existe uma exceção, e ela é opcional: uma configuração chamada **reconhecimento remoto**,
  desativada por padrão. Se você ativá-la, a fala é enviada ao serviço de reconhecimento do Google,
  sob a política de privacidade do próprio Google. Deixe-a desativada se não quiser isso.

Você pode usar o app inteiro digitando, sem nunca conceder acesso ao microfone.

## Recursos opcionais de IA, e os dados que eles enviam

Dois recursos podem enviar texto do diário para fora do seu dispositivo: **Ask** (fazer perguntas
sobre o seu diário) e a **extração automática de TODOs**. Ambos vêm **desativados por padrão** e
ambos ficam atrás de um interruptor principal — *"Permitir que qualquer dado do diário saia deste
dispositivo"* — que também vem desativado.

Nada é transmitido até você ligar esse interruptor principal *e* habilitar o recurso específico.

**Destinatário:** [OpenRouter](https://openrouter.ai), que encaminha a requisição a um provedor de
modelo de IA (por padrão `google/gemini-2.5-flash-lite`). Você escolhe o modelo nas Configurações.

**O que é enviado:**

- *Ask*: sua pergunta, mais suas entradas mais recentes do diário, na íntegra, como contexto.
  Quantas é uma configuração sua, e o padrão é 20. **Nunca são enviadas mais de 20 entradas,
  qualquer que seja o número mostrado na configuração** — o limite de transmissão é aplicado no
  código independentemente da configuração, então um número maior digitado nas Configurações não
  faz o app enviar mais. O seu idioma de exibição também é enviado (por exemplo
  `Portuguese (Brazil) (pt-BR)`), para que a resposta volte no idioma em que você lê o app — é a
  própria configuração de idioma, não um identificador do dispositivo.
- *Extração de TODOs*: o texto completo da entrada que você acabou de salvar, mais o texto das suas
  TODOs abertas no momento, para que o modelo consiga dizer quais foram concluídas.

**O que não é enviado:** áudio, seu nome, seu e-mail, identificadores do dispositivo, localização,
contatos ou qualquer ID de publicidade. O app não coleta nada disso, para começar.

**Cobrança e contas:** você conecta a sua própria conta do OpenRouter por um login no navegador. A
chave emitida pertence a você e o uso é cobrado de você. O desenvolvedor nunca vê a chave, nunca vê
suas requisições, e não opera nenhum servidor no caminho.

**Controles de privacidade enviados em toda requisição:** cada requisição declara retenção zero de
dados (`zdr`), recusa provedores que coletam dados para treinamento (`data_collection: "deny"`) e
desativa o roteamento alternativo silencioso. Isso é enviado por requisição, em vez de depender das
configurações da sua conta, porque o app não consegue lê-las. As requisições podem ser processadas
fora do seu país. Os termos e a política de privacidade do próprio OpenRouter regem o que eles fazem
com a requisição; veja <https://openrouter.ai/privacy>.

**Você pode retirar o consentimento a qualquer momento.** Desligar o interruptor principal bloqueia
novas requisições e cancela qualquer requisição em andamento.

**Uma limitação honesta:** excluir dados localmente não recupera nada que já foi enviado. Veja
[Retenção e exclusão de dados](#retencao-e-exclusao-de-dados) para o que a exclusão alcança e o que
não alcança.

## O que o desenvolvedor recebe

Nada. Não há servidor, não há conta, não há SDK de analytics, não há SDK de relatório de falhas e
não há publicidade. O desenvolvedor nunca vê suas requisições e não opera nada no caminho delas.

**Os dados do diário vão para exatamente um terceiro, o OpenRouter, e somente sob o consentimento
descrito acima.** Para ser completo, o app faz outros três tipos de requisição de rede. Nenhum
deles carrega conteúdo do diário:

- **Conectar sua conta do OpenRouter** — um login no navegador e a troca de chave que vem depois.
- **Carregar a lista de modelos de IA selecionáveis**, quando você abre o seletor de modelos nas
  Configurações. Isso não envia chave de API nem dados do diário, e é por isso que pode acontecer
  antes de você conceder o consentimento de nuvem — mas só ocorre quando você abre esse seletor,
  nunca na inicialização do app.
- **Áudio de fala para o serviço de fala do Google** — apenas se você ativar a opção *reconhecimento
  remoto* descrita em [Microfone e fala](#microfone-e-fala), que vem desligada por padrão.

Se o app for distribuído pelo Google Play, o Google coleta suas próprias estatísticas de instalação
e de falhas, sob a [política de privacidade do Google](https://policies.google.com/privacy). Essa
coleta é do Google, não do desenvolvedor, e não contém conteúdo do diário.

## Retenção e exclusão de dados {#retencao-e-exclusao-de-dados}

**A regra de retenção é curta, porque só existe um lugar onde seus dados vivem.** Tudo o que o app
guarda fica no seu dispositivo e em nenhum outro lugar. O desenvolvedor não opera servidor nem banco
de dados, então não há cópia para reter, backup para expirar, nem registro de conta que sobreviva ao
app. Os dados são mantidos exatamente enquanto você os mantiver, e excluí-los no app os exclui.

Por isso **não há pedido de exclusão a enviar nem conta a encerrar** — a exclusão é algo que você
faz diretamente, no app, a qualquer momento:

- **Excluir** qualquer entrada ou TODO individual, com uma breve janela para desfazer.
- **Excluir todas** as entradas do diário, ou todas as TODOs.
- **Apagar todos os dados do app** — remove entradas, TODOs, sua chave de API, seu registro de
  consentimento, e redefine as configurações de segurança.
- **Exportar** seu diário, como arquivo de backup criptografado (AES-256-GCM, protegido por uma
  senha escolhida por você) ou como Markdown puro.
- **Importar** um backup criptografado para restaurar.
- **Bloquear o app** com sua digital ou o PIN do dispositivo, com tempo de inatividade
  configurável, e bloquear capturas e gravações de tela.

Como não há conta nem cópia em servidor, desinstalar o app remove seus dados. Faça uma exportação
antes se quiser mantê-los.

**Duas coisas que a exclusão não alcança**, ditas com clareza em vez de escondidas:

- Qualquer coisa já enviada ao OpenRouter pelos recursos opcionais de IA acima. Excluir localmente
  não recupera uma requisição que já foi feita. Toda requisição dessas pede retenção zero ao
  provedor, mas isso é uma declaração contratual a um terceiro, não algo que este app possa impor
  ou verificar.
- Arquivos que você exportou. Depois de gravados no seu dispositivo ou em um drive na nuvem, eles
  ficam fora do controle do app, e a exportação em Markdown não é criptografada.

Se você quiser que a própria chave do OpenRouter seja revogada, faça isso no painel do OpenRouter —
o app consegue excluir a cópia local, mas não consegue revogar uma chave do lado deles.

## Crianças

O MyJournal não é direcionado a crianças e não se destina ao uso por menores de 13 anos.

## Segurança, e seus limites

O app criptografa o diário em repouso, mantém as chaves no Android Keystore, desativa o backup em
nuvem e pode exigir desbloqueio biométrico. Isso protege contra um dispositivo perdido ou roubado e
contra alguém copiar arquivos do aparelho.

Isso **não** protege um dispositivo cujo sistema operacional foi comprometido — um celular com root
rodando software malicioso, com a tela desbloqueada, consegue ler a memória do app enquanto ele está
em execução. Nenhuma criptografia no nível do app impede isso.

Para relatar um problema de segurança, veja a
[página de suporte](https://lschluter.github.io/myjournal-site/support/) ou escreva para
lschluterleite@gmail.com.

## Mudanças nesta política {#mudancas-nesta-politica}

Se o que o app faz com seus dados mudar de forma material, o aviso de consentimento dentro do app é
versionado e você será solicitado a revisar e conceder o consentimento de novo — um consentimento
concedido antes não vale para um aviso novo. A data de vigência acima também muda.

O número no topo desta página é essa versão do aviso, e cada versão mantém uma URL permanente para
que você sempre possa ler o texto com o qual de fato concordou, mesmo depois que uma versão mais
nova o substituir:

- Versão 2 (atual) — <https://lschluter.github.io/myjournal-site/privacy/v2/>

Esta página sempre mostra a versão atual.

## Contato

Leonardo Schluter Leite — lschluterleite@gmail.com
