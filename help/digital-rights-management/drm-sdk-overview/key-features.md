---
title: Principais recursos
description: Principais recursos
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Principais recursos{#key-features}

O Adobe Primetime DRM oferece estes recursos principais:

* **Suporte a streaming HLS (requer Adobe Primetime):** Use o Primetime DRM com conteúdo HLS que pode ser transmitido para qualquer plataforma compatível com o Flash ou Adobe Primetime (como desktop, iOS e Android).
* **Suporte a aplicativos nativos do iOS (exige o Adobe Primetime):** Use o Primetime DRM para proteger vídeos nos aplicativos do iOS.
* **Suporte para aplicativo Android nativo (requer Adobe Primetime):** Use o Primetime DRM para proteger vídeos em seus aplicativos Android.
* **Streaming Protegido no Xbox (requer Adobe Primetime)**.
* **Entrega remota de chaves do iOS (requer Adobe Primetime):** Suporte para fornecer chaves remotas do iOS por meio de um servidor de chaves de vários locatários, chamado de Servidor de chaves DRM Primetime.
* **Proteção de conteúdo persistente:** O conteúdo permanece protegido em toda a cadeia de distribuição. Depois que o conteúdo é empacotado, ele permanece protegido o tempo todo e partes dele são descriptografadas somente no momento da reprodução e de acordo com as regras de uso.
* Como o conteúdo é fornecido com regras de uso e informações de licenciamento, a proteção sempre é transferida com o conteúdo. Se consumidores não licenciados tentarem reproduzir o conteúdo, a política incorporada no conteúdo os redirecionará para que eles possam adquirir uma licença válida para o conteúdo.
* **Reprodução segura de conteúdo protegido:** Esquemas de criptografia comprovados são usados para proteger o conteúdo contra reprodução não autorizada.
* **Regras de uso flexíveis:** As regras de uso determinam como os consumidores podem usar conteúdo protegido. As regras de uso compatíveis com o Primetime DRM permitem vários modelos de negócios diferentes, incluindo pay-per-view, aluguel de filmes, subscrições ou serviços financiados por anúncios. As regras de uso são especificadas pela política que você incorpora ao conteúdo durante o empacotamento ou podem ser especificadas pelo License Server durante a aquisição da licença.
* **Proteção de saída:** Os controles de proteção de saída podem ser usados para envolver esquemas de proteção como HDCP, CGMS-A ou Rovi (anteriormente Macrovision) ACP. Isso pode ajudar a proteger a saída de conteúdo em saídas digitais (por exemplo, HDMI, DVI e UDI) e analógicas (por exemplo, S-Video e Component Video).

  Você pode especificar opções de proteção de saída na política criada para o seu conteúdo, permitindo ou não o acesso ao conteúdo com base nos recursos de proteção de saída de um dispositivo. Por exemplo, você pode especificar que a proteção de saída não é necessária para determinado conteúdo, mas exige a proteção de saída para conteúdo de vídeo premium, impedindo a saída de conteúdo em sistemas operacionais que não têm esse recurso.

  Embora essas regras sejam aplicadas consistentemente em todas as plataformas, atualmente só é possível ativar com segurança a proteção de saída nas plataformas Windows.

* **Suporte para transmissão dinâmica:** Use o recurso de transmissão dinâmica de Flash Media Server ou Adobe HTTP Dynamic Streaming para proteger o conteúdo codificado em várias taxas de bits. A transmissão dinâmica usa um fluxo de vídeo que ajusta dinamicamente a taxa de bits e a qualidade de reprodução, com base na largura de banda disponível, proporcionando uma melhor experiência ao usuário. O Primetime DRM permite usar a mesma Chave de criptografia de conteúdo e licença em diferentes codificações do mesmo ativo.
* **Exibição offline:** O cliente de tempo de execução do Adobe AIR permite que os consumidores baixem e armazenem conteúdo para visualização posterior, independentemente de o computador permanecer ou não conectado à Internet.
* **Licenciamento baseado em identidade:** Vincula permissões a identidades de usuário, exigindo que os consumidores se autentiquem (fornecendo uma ID de usuário e senha) para obter acesso ao conteúdo. O licenciamento baseado em identidade exige que a parte que desenvolve o aplicativo cliente implemente a autenticação de usuário como parte do fluxo de trabalho de aquisição de licença.
* **Encadeamento de licenças:** Permite que os consumidores estendam a vida útil de todo o seu conteúdo renovando uma única licença raiz. Um dos principais usos da cadeia de licenças é para modelos de negócios baseados em assinatura, em que, no final de um período de assinatura, as licenças para um grande número de arquivos de conteúdo podem ser renovadas simplesmente renovando a licença raiz.

  As licenças raiz e folha estão vinculadas ao computador do consumidor. A licença folha contém o CEK e uma referência à licença raiz. A licença raiz pode estender os direitos concedidos na licença folha. Por exemplo, um consumidor pode ter licenças folha para 50 conteúdos que expirarão no final de um determinado período de assinatura. Se o consumidor baixar uma nova licença raiz com uma nova data de expiração, todos os 50 conteúdos poderão ser reproduzidos até que a licença atualizada expire.

  O Primetime DRM 2.0 introduziu o encadeamento de licenças, no qual as licenças folha e raiz estão vinculadas a uma máquina específica. O Primetime DRM 3.0 apresenta uma forma aprimorada de encadeamento de licenças, na qual uma folha é vinculada a uma licença raiz e somente a licença raiz é vinculada a uma máquina ou domínio específico. Ler *Encadeamento de licenças aprimorado* in *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo*.

* **Rotação de chaves:** Durante o empacotamento típico, o conteúdo é criptografado usando a Chave de criptografia de conteúdo (CEK), e o cliente obtém uma licença contendo a CEK para consumir o conteúdo. Quando a rotação de chaves estiver ativada, a chave usada para criptografar o conteúdo poderá ser alterada para que a chave seja usada apenas para criptografar uma parte do conteúdo. Ler *Rotação de chaves* in *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo*.

* **Licenças fora da banda:** Com o Primetime DRM, é possível implementar um fluxo de trabalho no qual os clientes obtêm licenças pré-geradas fora da banda, eliminando a necessidade de implantar um License Server.
* **Suporte de domínio:** Como alternativa à vinculação de uma licença a um dispositivo específico, o Primetime DRM oferece suporte à vinculação de licenças a um domínio. Vários dispositivos podem ingressar em um domínio e receber um token de domínio, permitindo que as licenças sejam movidas entre dispositivos no domínio. Ler *Registro de domínio* in *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo*.

* **Criptografia parcial:** Especifica se todos os quadros ou somente um subconjunto de quadros devem ser criptografados. Há três níveis de criptografia: baixo, médio e alto. A redução do nível de criptografia pode diminuir a sobrecarga da CPU em máquinas com poucos recursos.
* **Empacotamento de conteúdo desconectado:** O empacotamento de conteúdo não requer uma conexão de rede com o License Server. Isso permite operações de back-end seguras, limitando a exposição de conteúdo compactado que ainda não foi protegido.
* **Controle da reversão do relógio: **o Primetime DRM fornece o cálculo seguro e preciso do tempo para detectar a reversão do relógio no computador cliente. Isso aplica os direitos relacionados ao acesso ao conteúdo por um período específico e impede que os consumidores subvertam os direitos de acesso alterando o tempo em seus computadores.
* **Individualização**: permite a vinculação de conteúdo a uma máquina específica.
* **Lista de permissões de aplicativo:** Permite que o tempo de execução do cliente garanta que o conteúdo protegido seja reproduzido apenas em um SWF ou aplicativo AIR autorizado.
* **Revogação de clientes comprometidos:** O software cliente comprometido pode ser revogado. Se for determinado que o Flash Player ou o tempo de execução do Adobe AIR foi comprometido, o serviço poderá ser recusado a esses clientes até que eles atualizem para uma versão mais recente e segura do software cliente.
* **Várias políticas para o mesmo arquivo de vídeo:** Um único conteúdo de vídeo pode ter várias políticas incorporadas durante o empacotamento. Ao emitir uma licença, o License Server pode decidir quais das políticas usar, permitindo que um distribuidor de conteúdo use o mesmo arquivo protegido para diferentes modelos de negócios (como aluguel e venda automática eletrônica).
