---
seo-title: Principais recursos
title: Principais recursos
uuid: bee91fd7-a335-4881-abad-8972f28630d5
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---


# Principais recursos{#key-features}

O Adobe Primetime DRM fornece os seguintes recursos principais:

* **Suporte para transmissão em sequência HLS (requer Adobe Primetime):** Use o DRM Primetime com conteúdo HLS que pode ser transmitido para qualquer plataforma suportada pelo Flash ou Adobe Primetime (como desktop, iOS e Android).
* **Suporte nativo a aplicativos iOS (requer Adobe Primetime):** Use o Primetime DRM para proteger o vídeo nos aplicativos iOS.
* **Suporte nativo a aplicativos Android (requer Adobe Primetime):** Use o Primetime DRM para proteger vídeos em seus aplicativos Android.
* **Streaming protegido no Xbox (requer Adobe Primetime)**.
* **Delivery de chave do iOS remoto (requer Adobe Primetime):** Suporte para fornecer chaves remotas do iOS por meio de um servidor de chave de vários locatários, chamado Primetime DRM Key Server.
* **Proteção de conteúdo persistente: o** conteúdo permanece protegido em toda a cadeia de distribuição. Depois que o conteúdo é empacotado, ele permanece protegido o tempo todo, e partes dele são descriptografadas somente no momento da reprodução e de acordo com as regras de uso.
* Como o conteúdo é fornecido com regras de uso e informações de licenciamento, a proteção sempre viaja com o conteúdo. Se consumidores não licenciados tentarem reproduzir o conteúdo, a política incorporada no conteúdo os redirecionará para que possam adquirir uma licença válida para o conteúdo.
* **Reprodução segura de conteúdo protegido:esquemas de criptografia** comprovados são usados para proteger conteúdo de reprodução não autorizada.
* **Regras de uso flexíveis:As regras** de uso determinam como os consumidores podem usar conteúdo protegido. As regras de uso suportadas pelo Primetime DRM permitem vários modelos de negócios diferentes, incluindo pagamento por visualização, aluguel de filmes, subscrições ou serviços financiados por anúncios. As regras de uso são especificadas pela política incorporada ao conteúdo durante o empacotamento ou podem ser especificadas pelo License Server durante a aquisição da licença.
* **Proteção de saída: os controles de proteção de** saída podem ser usados para acionar sistemas de proteção como HDCP, CGMS-A ou Rovi (anteriormente Macrovision) ACP. Isso pode ajudar a proteger a saída de conteúdo sobre as saídas digitais (por exemplo, HDMI, DVI e UDI) e analógicas (por exemplo, S-Video e Componente Video).

   É possível especificar opções de proteção de saída na política que você cria para seu conteúdo, permitindo ou impedindo o acesso ao conteúdo com base nos recursos de proteção de saída de um dispositivo. Por exemplo, você pode especificar que a proteção de saída não é necessária para determinado conteúdo, mas requer proteção de saída para conteúdo de vídeo premium, impedindo a saída de conteúdo em sistemas operacionais que não tenham esse recurso.

   Embora essas regras sejam aplicadas de forma consistente em todas as plataformas, atualmente, só é possível ativar a proteção de saída com segurança nas plataformas Windows.

* **Suporte para streaming dinâmico:** use o recurso de streaming dinâmico de Flash Media Server ou HTTP Dynamic Streaming de Adobe para proteger o conteúdo codificado em várias taxas de bits. O streaming dinâmico usa um fluxo de vídeo que ajusta dinamicamente a taxa de bits e a qualidade da reprodução com base na largura de banda disponível, proporcionando uma melhor experiência do usuário. O DRM Primetime permite usar a mesma chave de criptografia de conteúdo e a mesma licença nas diferentes codificações do mesmo ativo.
* **Exibição offline:** o cliente de tempo de execução do Adobe AIR permite que os clientes baixem e armazenem conteúdo para visualização posterior, independentemente de o computador permanecer conectado à Internet.
* **Licenciamento baseado em identidade:** vincula permissões a identidades de usuário, exigindo que os consumidores se autentiquem (fornecendo uma ID de usuário e senha) para obter acesso ao conteúdo. O licenciamento baseado em identidade exige que a parte que desenvolve o aplicativo cliente implemente a autenticação do usuário como parte do fluxo de trabalho de aquisição de licença.
* **Cadeamento de licença:** permite que os consumidores estendam a vida útil de todo o seu conteúdo renovando uma única licença raiz. Um dos principais usos do encadeamento de licenças é para modelos de negócios baseados em subscrições, nos quais, ao final de um período de subscrição, as licenças para um grande número de arquivos de conteúdo podem ser renovadas com a simples renovação da licença raiz.

   As licenças de raiz e de folha estão ligadas ao computador do consumidor. A licença de folha contém o CEK e uma referência à licença raiz. A licença raiz pode estender os direitos concedidos na licença de folha. Por exemplo, um consumidor pode ter licenças de folha para 50 partes de conteúdo que expirarão no final de um determinado período de subscrição. Se o consumidor baixar uma nova licença raiz com uma nova data de expiração, todas as 50 partes do conteúdo poderão ser reproduzidas até que a licença atualizada expire.

   O Primetime DRM 2.0 introduziu o encadeamento de licença no qual as licenças de folha e raiz estão vinculadas a uma máquina específica. O Primetime DRM 3.0 apresenta uma forma aprimorada de encadeamento de licença, na qual uma folha está vinculada a uma licença raiz, e somente a licença raiz está vinculada a uma máquina ou domínio específico. Leia *Encadeamento aprimorado de licença* em *Usando o Adobe Primetime DRM SDK para proteger conteúdo*.

* **Rotação de chave:** durante o empacotamento típico, o conteúdo é criptografado usando a Chave de criptografia de conteúdo (CEK) e o cliente obtém uma licença contendo o CEK para consumir o conteúdo. Quando a rotação de chaves está ativada, a chave usada para criptografar o conteúdo pode ser alterada para que a chave seja usada apenas para criptografar uma parte do conteúdo. Leia *Rotação da chave* em *Usando o Adobe Primetime DRM SDK para proteger conteúdo*.

* **Licenças fora de banda:** com o Primetime DRM, é possível implementar um fluxo de trabalho no qual os clientes obtêm licenças pré-geradas fora de banda, eliminando a necessidade de implantar um License Server.
* **Suporte de domínio:** como alternativa ao vínculo de uma licença a um dispositivo específico, o Primetime DRM oferece suporte ao vínculo de licenças a um domínio. Vários dispositivos podem ingressar em um domínio e receber um token de domínio, permitindo que as licenças sejam movidas entre dispositivos no domínio. Leia *Registro de domínio* em *Usando o Adobe Primetime DRM SDK para proteção de conteúdo*.

* **Criptografia parcial:** especifica se todos os quadros, ou apenas um subconjunto de quadros, devem ser criptografados. Há três níveis de criptografia: baixa, média e alta. A redução do nível de criptografia pode diminuir a sobrecarga da CPU em máquinas de baixa extremidade.
* **Embalagem de conteúdo desconectado:O empacotamento de** conteúdo não exige uma conexão de rede com o License Server. Isso permite operações de back-end seguras limitando a exposição de conteúdo compactado que ainda não foi protegido.
* **Controle da reversão do clock: **O DRM Primetime fornece o cálculo seguro e preciso do tempo para detectar a reversão do clock no computador cliente. Isso aplica direitos relacionados ao acesso ao conteúdo por um período específico e impede que os consumidores subvertam os direitos de acesso alterando o tempo no computador.
* **Individualização**: Permite vincular conteúdo a uma máquina específica.
* **Lista de permissões do aplicativo:** permite que o tempo de execução do cliente garanta que o conteúdo protegido seja reproduzido somente em um aplicativo SWF ou AIR autorizado.
* **Revogação de clientes comprometidos:O software cliente** comprometido pode ser revogado. Se o Flash Player ou o tempo de execução do Adobe AIR for determinado como tendo sido comprometido, o serviço poderá ser recusado a esses clientes até que eles atualizem para uma versão mais nova e mais segura do software cliente.
* **Várias políticas para o mesmo arquivo de vídeo:** um único conteúdo de vídeo pode ter várias políticas incorporadas durante o empacotamento. Ao emitir uma licença, o License Server pode decidir quais políticas usar, permitindo que um distribuidor de conteúdo use o mesmo arquivo protegido para diferentes modelos de negócios (como aluguel e venda eletrônica).