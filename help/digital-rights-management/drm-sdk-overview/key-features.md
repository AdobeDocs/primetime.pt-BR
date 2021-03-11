---
title: Principais recursos
description: Principais recursos
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---


# Principais recursos{#key-features}

O Adobe Primetime DRM fornece estes recursos principais:

* **Suporte para transmissão de HLS (requer Adobe Primetime):** use o DRM do Primetime com conteúdo HLS que pode ser transmitido para qualquer plataforma compatível com Flash ou Adobe Primetime (como desktop, iOS e Android).
* **Suporte a aplicativo iOS nativo (requer Adobe Primetime):** use o DRM do Primetime para proteger vídeo em seus aplicativos iOS.
* **Suporte a aplicativo nativo Android (requer Adobe Primetime):** use o DRM do Primetime para proteger o vídeo nos aplicativos Android.
* **Fluxo protegido no Xbox (requer Adobe Primetime)**.
* **Entrega remota de chaves iOS (requer Adobe Primetime):** suporte para entrega de chaves iOS remotas por meio de um servidor de chaves de vários locatários, chamado de Servidor de chaves DRM do Primetime.
* **Proteção de conteúdo persistente:** o conteúdo permanece protegido por toda a cadeia de distribuição. Depois que o conteúdo é empacotado, ele permanece protegido o tempo todo e partes dele são descriptografadas somente no momento da reprodução e de acordo com as regras de uso.
* Como o conteúdo é fornecido com regras de uso e informações de licenciamento, a proteção sempre viaja com o conteúdo. Se consumidores não licenciados tentarem reproduzir o conteúdo, a política incorporada no conteúdo os redirecionará para que possam adquirir uma licença válida para o conteúdo.
* **Reprodução segura de conteúdo protegido:** os esquemas de criptografia comprovados são usados para proteger o conteúdo de reprodução não autorizada.
* **Regras de uso flexíveis:** as regras de uso determinam como os consumidores podem usar conteúdo protegido. As regras de uso compatíveis com o Primetime DRM permitem vários modelos de negócios diferentes, incluindo pagamento por exibição, aluguel de filmes, assinaturas ou serviços financiados por anúncios. As regras de uso são especificadas pela política incorporada ao conteúdo durante o empacotamento ou podem ser especificadas pelo License Server durante a aquisição da licença.
* **Proteção de saída:** os controles de proteção de saída podem ser usados para envolver esquemas de proteção como HDCP, CGMS-A ou Rovi (anteriormente Macrovision) ACP. Isso pode ajudar a proteger a saída de conteúdo sobre as saídas digitais (por exemplo, HDMI, DVI e UDI) e analógicas (por exemplo, S-Video e Component Video).

   Você pode especificar opções de proteção de saída na política criada para o seu conteúdo, permitindo ou não permitindo o acesso ao conteúdo com base nos recursos de proteção de saída de um dispositivo. Por exemplo, você pode especificar que a proteção de saída não é necessária para determinado conteúdo, mas requer proteção de saída para conteúdo de vídeo premium, evitando a saída do conteúdo em sistemas operacionais que não têm esse recurso.

   Embora essas regras sejam aplicadas de forma consistente em todas as plataformas, atualmente é possível ativar com segurança a proteção de saída em plataformas Windows.

* **Suporte para transmissão dinâmica:** use o recurso de transmissão dinâmica do Flash Media Server ou do Adobe HTTP Dynamic Streaming para proteger o conteúdo codificado em várias taxas de bits. O streaming dinâmico usa um fluxo de vídeo que ajusta dinamicamente a taxa de bits e a qualidade da reprodução com base na largura de banda disponível, fornecendo uma melhor experiência ao usuário. O DRM do Primetime possibilita o uso da mesma Chave de criptografia de conteúdo e licença em diferentes codificações do mesmo ativo.
* **Visualização offline:** o cliente de tempo de execução do Adobe AIR permite que os consumidores baixem e armazenem conteúdo para visualização posterior, independentemente de o computador permanecer conectado à Internet.
* **Licenciamento baseado em identidade:** vincula permissões às identidades de usuário, exigindo que os consumidores se autentiquem (fornecendo uma ID de usuário e senha) para obter acesso ao conteúdo. O licenciamento baseado em identidade exige que a parte que desenvolve o aplicativo cliente implemente a autenticação de usuário como parte do fluxo de trabalho de aquisição de licença.
* **Cadeamento de licença:** permite que os consumidores estendam a vida de todo o conteúdo renovando uma única licença raiz. Um dos usos principais do encadeamento de licenças é para modelos de negócios com base em assinatura, onde, no final de um período de assinatura, as licenças para um grande número de arquivos de conteúdo podem ser renovadas com a simples renovação da licença raiz.

   As licenças de raiz e de folha estão vinculadas ao computador do consumidor. A licença de folha contém o CEK e uma referência à licença raiz. A licença raiz pode estender os direitos concedidos na licença de folha. Por exemplo, um consumidor pode ter licenças de folha para 50 partes de conteúdo que expirarão no final de um determinado período de assinatura. Se o consumidor baixar uma nova licença raiz com uma nova data de expiração, todos os 50 conteúdos poderão ser reproduzidos até que a licença atualizada expire.

   O Primetime DRM 2.0 introduziu o encadeamento de licenças, no qual as licenças de folha e raiz estão vinculadas a uma máquina específica. O Primetime DRM 3.0 apresenta uma forma aprimorada de cadeia de licença, na qual uma folha é vinculada a uma licença raiz e somente a licença raiz é vinculada a uma máquina ou domínio específico. Leia *Encadeamento de licença aprimorado* em *Uso do Adobe Primetime DRM SDK para proteção de conteúdo*.

* **Rotação de chave:** durante a embalagem típica, o conteúdo é criptografado usando a Chave de criptografia de conteúdo (CEK) e o cliente obtém uma licença contendo o CEK para consumir o conteúdo. Quando a rotação de chave estiver ativada, a chave usada para criptografar o conteúdo poderá ser alterada para que a chave seja usada apenas para criptografar uma parte do conteúdo. Leia *Rotação de chave* em *Usando o SDK de DRM do Adobe Primetime para proteger o conteúdo*.

* **Licenças fora de banda:** com o Primetime DRM, é possível implementar um fluxo de trabalho no qual os clientes obtêm licenças pré-geradas fora de banda, eliminando a necessidade de implantar um License Server.
* **Suporte de domínio:** como alternativa para vincular uma licença a um dispositivo específico, o DRM do Primetime suporta a vinculação de licenças a um domínio. Vários dispositivos podem ingressar em um domínio e receber um token de domínio que permite que as licenças sejam movidas entre dispositivos no domínio. Leia *Domain Registration* em *Using the Adobe Primetime DRM SDK for Protecting Content*.

* **Criptografia parcial:** especifica se todos os quadros, ou apenas um subconjunto de quadros, devem ser criptografados. Há três níveis de criptografia: baixa, média e alta. A redução do nível de criptografia pode diminuir a sobrecarga da CPU em máquinas de ponta.
* **Embalagem de conteúdo desconectado:** o empacotamento de conteúdo não requer uma conexão de rede com o License Server. Isso permite operações de back-end seguras limitando a exposição de conteúdo compactado que ainda não foi protegido.
* **Controle sobre a reversão do relógio: **O DRM do Primetime fornece o cálculo seguro e preciso de tempo para detectar a reversão do relógio no computador cliente. Isso aplica direitos relacionados ao acesso a conteúdo por um período específico e impede que os consumidores subvertam os direitos de acesso alterando o tempo em seu computador.
* **Individualização**: Permite vincular conteúdo a uma máquina específica.
* **Lista de permissões do aplicativo:** permite que o tempo de execução do cliente garanta que o conteúdo protegido seja reproduzido somente em um aplicativo SWF ou AIR autorizado.
* **Revogação de clientes comprometidos:** o software cliente comprometido pode ser revogado. Se o Flash Player ou o tempo de execução do Adobe AIR for determinado como comprometido, o serviço poderá ser recusado a esses clientes até que eles atualizem para uma versão mais recente e mais segura do software cliente.
* **Várias políticas para o mesmo arquivo de vídeo:** um único conteúdo de vídeo pode ter várias políticas incorporadas durante o empacotamento. Ao emitir uma licença, o License Server pode decidir qual das políticas usar, permitindo que um distribuidor de conteúdo use o mesmo arquivo protegido para diferentes modelos de negócios (como aluguel e venda eletrônica).