---
title: Procedimentos de escalonamento
description: Procedimentos de escalonamento
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Procedimentos de escalonamento {#escalation-procedures}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

>[!IMPORTANT]
> 
>Chame a linha direta : **+1-205-693-9813** e enviar um email para **tve-support@adobe.com** incluindo **URGENTE - INCIDENTE** na linha de assunto.

## Introdução {#introduction}

Este documento descreve os procedimentos de suporte para incidentes graves (**GRAVIDADE 1** nível) afetando a autenticação da Adobe Primetime, o Monitoramento de simultaneidade do Primetime e seus parceiros.\
 

## Definição de um Incidente de Nível SEVERITY 1 {#definition-of-a-severity-1-level-incident}

A **GRAVIDADE 1** incidente de nível é um **LIVE** situação, **ocorrendo no ambiente de produção**, que não permite a conclusão dos fluxos de autenticação e/ou autorização para um canal e um MVPD, afetando um grande número de assinantes do MVPD que está a executar o fluxo.


## Exemplos de incidentes de SEVERITY 1 {#examples-of-severity-1-incidentcs}

* O Habilitador de acesso de produção hospedado em  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` ou `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`) não está disponível.

* Para um MVPD específico, o Adobe não redireciona / exibe a página de logon depois que o usuário seleciona o MVPD (em qualquer um dos navegadores compatíveis).

* O parceiro recebe um grande número de relatórios que os usuários não podem autenticar/autorizar com um MVPD específico.

* Durante o processo de autenticação, o usuário fica preso em uma página de erro de Adobe sem a possibilidade de reiniciar o fluxo de autenticação/autorização.


| Exemplos do que é **NOT** um incidente de Gravidade 1 |
|---|
| Para questões desse tipo, o Adobe fornecerá apoio para investigações, mas não são incidentes de Gravidade 1:<ul><li>Um ou alguns assinantes não podem executar o fluxo devido a um problema de versão do Flash (Flash ausente, bloqueadores de Flashes, versão incorreta do Flash).</li><li>Um ou alguns assinantes não podem autenticar e permanecer na página de logon do MVPD.</li><li>Um ou alguns assinantes são autenticados, mas não podem reproduzir vídeos.</li><li>Um/poucos/todos os assinantes encontram um erro de JavaScript no site do Programador</li></ul> |

## Fluxos de Escalonamento de Gravidade 1 {#severity-1-escalation-flows}

Os incidentes de gravidade 1 podem ser iniciados pelo Adobe ou por um parceiro de autenticação da Adobe Primetime. As etapas para cada um são apresentadas abaixo.

### Fluxo iniciado pelo parceiro {#partner-initiated-flow}

1. O parceiro identifica um incidente de Gravidade 1 (conforme descrito acima)exigindo atenção imediata do Adobe.
1. O parceiro envia um email para **tve-support@adobe.com** incluindo **URGENTE - INCIDENTE** na linha de assunto e adicionando as seguintes informações:
   * Título
   * Descrição e etapas para reproduzir
   * SO / Navegador
   * SDK e versão
   * Dispositivos afetados
   * % de usuários afetados
   * Logs do Rastreamento HTTP ou do Dispositivo que demonstram o problema
   * (opcional) Quaisquer capturas de tela ou vídeo disponíveis que demonstrem o problema
1. Se o Adobe não responder ao tíquete em 30 minutos, o parceiro chama o seguinte número:
   **1-205-693-9813**

   >[!IMPORTANT]
   >Se você não incluir &quot;URGENT-INCIDENT&quot; no título do ticket, ele não será coletado pelo nosso sistema de notificação**.

### Fluxo iniciado pelo Adobe {#adobe-initiated-flow}

#### ...para um problema de autenticação da Adobe Primetime {#adobe-initiated-flow-authn-issue}

1. O Adobe identifica um problema interno e abre um tíquete com nosso sistema de rastreamento.

1. O Adobe notifica o gerente de programa do parceiro e o contato técnico, especificando o número do ticket e o impacto estimado do problema.

1. O Adobe trabalha para a resolução do incidente e mantém todos os parceiros afetados informados.

#### ...para um problema de parceiro (Programador/MVPD) {#adobe-initiated-flow-partner-issue}

1. O Adobe identifica um problema relacionado à integração com um MVPD ou em um dos sites do Programador.

1. Adobe notifica o parceiro afetado <u>seguindo os procedimentos de apoio em vigor com esse parceiro</u> e abre um tíquete com a organização de suporte do parceiro.

1. Se, durante a análise de impacto, o Adobe identificar que o problema pertence a uma das decisões pré-acordadas sobre cenários de incidentes, consulte **Decisões pré-acordadas sobre cenários de incidente**, atuará de acordo sem esperar a entrada do parceiro.

1. O Adobe aguardará as atualizações do parceiro e uma notificação do parceiro quando o serviço for restaurado.

## Decisões pré-acordadas sobre cenários de incidente {#pre-agreed-descn}

Há algumas situações em que uma ação padrão será executada no caso da ocorrência desse cenário:

|  | Cenário | Descrição | Ações |
|---|---|---|---|
| S1 | O Adobe identifica um problema com a integração de um MVPD durante as operações normais de produção. | Durante as operações normais de produção, o Adobe identifica um problema com um dos MVPDs que torna impossível a execução dos fluxos de autenticação/autorização (por exemplo, certificados expirados, respostas SAML expiradas, portas fechadas, parâmetros alterados, etc.) | - O Adobe notificará o MVPD e os programadores afetados.  </br> </br> - O Adobe desativará este MVPD para todos os Programadores afetados. </br> </br> - O Adobe abrirá um bilhete no MVPD seguindo o procedimento de apoio acordado com esse MVPD |
| S2 | O Adobe ativa um novo MVPD para um Programador e o Programador permite o MVPD antes da data de lançamento. | O Adobe está ativando um novo MVPD para o site de um Programador, e o site já está exibindo o novo MVPD no selecionador, mesmo que não fosse suposto. | - O Adobe notificará o Programador sobre o novo MVPD que aparece no selecionador antes da data agendada. </br> </br>  - O programador tomará medidas para removê-lo do seletor, se necessário. |
| S3 | O Adobe ativa um novo MVPD para um Programador mesmo que o MVPD não esteja pronto para entrar na produção | O Adobe está ativando um novo MVPD para um Programador, mas o MVPD ainda não implantou o suporte para a integração, portanto, os fluxos de autenticação/autorização não podem ser executados | - O Adobe só fará a implantação se solicitado pelo programador </br> </br> - O programador será responsável por assegurar a autorização do MVPD depois de todos os ensaios terem sido efetuados. |

## Expectativas De Resposta Para Incidentes De Gravidade 1 {#response-expectations-for-severity-one-incidents}

* Resposta inicial: 30 minutos (24/7)
* Plano de ação: 1 hora (24/7)
* Resolução: ASAP (24/7)
