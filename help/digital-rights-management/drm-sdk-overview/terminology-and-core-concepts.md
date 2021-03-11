---
title: Terminologia e conceitos principais
description: Terminologia e conceitos principais
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Terminologia e conceitos principais{#terminology-and-core-concepts}

Os termos e conceitos a seguir são usados neste documento:

**Consumidor**

O *consumidor* é o usuário final que baixa ou envia conteúdo.

**Conteúdo**

** O conteúdo consiste em arquivos digitais de áudio ou vídeo.

**Chave de criptografia de conteúdo**

A *Chave de criptografia de conteúdo* (CEK) é uma chave criptográfica usada para criptografar o conteúdo.

**Proprietários do conteúdo**

*Os* proprietários do conteúdo são as entidades comerciais proprietárias dos direitos autorais do conteúdo. Podem ser grandes estúdios de fotografia em movimento ou pequenos produtores independentes de filmes ou outros conteúdos audiovisuais.

**Pacotes de conteúdo**

*Os pacotes* de conteúdo são organizações que empacotam conteúdo para uso com o Adobe Primetime DRM. Os proprietários ou distribuidores de conteúdo podem optar por empacotar seu próprio conteúdo ou podem inscrever os serviços de terceiros para empacotar seu conteúdo e distribuí-lo eletronicamente pela Internet.

**Certificado digital**

*Certificados digitais*  (também conhecidos como  *certificados*) vinculam uma entidade, como um indivíduo, organização ou sistema, a um par de chaves públicas e privadas específico. Certificados digitais podem ser considerados credenciais eletrônicas que verificam a identidade de um indivíduo, sistema ou organização.

**Assinatura digital**

Uma *assinatura digital* vincula a identidade do editor ao conteúdo que eles publicaram e fornece um mecanismo para detectar adulterações. Os algoritmos de assinatura digital usam funções de hash criptográfico e algoritmos de criptografia assimétricos (ou pares de chave pública/privada). Algumas assinaturas digitais também aproveitam os certificados digitais e a infraestrutura de chave pública (PKI) para vincular chaves públicas às identidades dos proprietários ou distribuidores de conteúdo.

**Distribuidor**

*Distribuidores*  (também conhecidos como  *distribuidores de* conteúdo ou varejistas*) são entidades comerciais que protegem direitos de distribuição de proprietários de conteúdo para publicar e divulgar conteúdo aos consumidores. Em alguns casos, a mesma entidade é proprietária de conteúdo e distribuidora de conteúdo.

**Metadados DRM**

Informações que o cliente (ou seja, o Flash® Player, o tempo de execução do Adobe® AIR® e o cliente Primetime do Adobe®) envia para identificar o conteúdo solicitado.

**Licença**

Uma *licença *é uma estrutura de dados que contém uma chave criptografada usada para descriptografar conteúdo associado a uma política. A licença é gerada pelo DRM do Primetime quando o consumidor solicita conteúdo e está vinculado ao computador do consumidor. Usando uma política como referência, a licença define os direitos disponíveis para o consumidor que baixa conteúdo. Para visualizar o conteúdo, o consumidor deve obter uma licença.

**Aquisição de licença**

*A* aquisição de licença é o processo de aquisição de uma licença que permite ao consumidor descriptografar e visualizar conteúdo protegido de acordo com um conjunto de regras de uso. A aquisição de licença ocorre quando um cliente envia informações que identificam o conteúdo solicitado (os *metadados de DRM*) e o certificado da máquina (identificando o computador do consumidor) para o License Server (veja abaixo).

**Servidor de licenças**

O* License Server *pode ser integrado aos sistemas de faturamento e autenticação do distribuidor ou do provedor de serviços e pode conter lógica comercial para verificar se o consumidor que solicita conteúdo protegido está autorizado a visualizar o conteúdo. Se o usuário estiver autorizado a acessar o conteúdo, o License Server emitirá uma licença que permitirá que o cliente do tempo de execução descriptografe e reproduza o conteúdo com base na política e nos direitos associados à conta do consumidor.

Você deve criar e implantar um Servidor de licenças usando o SDK de DRM do Primetime.

**Política**

Uma *policy* é um contêiner das regras de uso que determinam como os consumidores podem usar conteúdo protegido. As políticas são definidas independentemente do conteúdo que está sendo protegido. Uma política não impõe direitos até que seja vinculada ao conteúdo por meio da licença. Uma política lista o conjunto de regras de uso, ou seja, as permissões ou os &quot;direitos&quot; que os consumidores têm ao conteúdo que adquirem. Por exemplo, os proprietários de conteúdo podem criar uma política que garanta que o conteúdo protegido seja acessível apenas aos consumidores por um período específico. Essa política é aplicada a todo o conteúdo para o qual o proprietário do conteúdo deseja aplicar essa restrição.

As políticas são criadas usando o SDK de DRM do Primetime.

**Conteúdo protegido**

*O conteúdo protegido*  (também conhecido como conteúdo  *empacotado*) refere-se ao conteúdo de vídeo que foi criptografado usando o SDK DRM do Primetime ou outras ferramentas compatíveis.

**Varejistas**

Consulte a entrada para *distribuidores* anteriormente nesta seção.
