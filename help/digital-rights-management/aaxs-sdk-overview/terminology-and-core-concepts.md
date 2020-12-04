---
seo-title: Terminologia e conceitos fundamentais
title: Terminologia e conceitos fundamentais
uuid: 89a9e4b0-f5e1-4dc2-9cf8-0c8d7e9b7d62
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Terminologia e conceitos fundamentais {#terminology-and-core-concepts}

Os seguintes termos e conceitos são usados em todo o documento:

**Consumidor**

O *consumidor* é o usuário final que baixa ou transmite conteúdo.

**Conteúdo**

*O* conteúdo consiste em arquivos de áudio ou vídeo digitais.

**Chave de criptografia de conteúdo**

A *Chave de criptografia de conteúdo* (CEK) é uma chave criptográfica usada para criptografar o conteúdo.

**Proprietários de conteúdo**

*Os* proprietários de conteúdo são as entidades comerciais que possuem os direitos autorais do conteúdo. Podem ser grandes estúdios cinematográficos ou pequenos produtores independentes de filmes ou outros conteúdos audiovisuais.

**Empacotadores de conteúdo**

*Os* pacotes de conteúdo são organizações que empacotam conteúdo para uso com o Adobe Access. Os proprietários ou distribuidores de conteúdo podem optar por disponibilizar seus próprios conteúdos ou podem inscrever os serviços de terceiros para disponibilizar seus conteúdos e distribuí-los eletronicamente pela Internet.

**Certificado digital**

*Certificados*  digitais (também conhecidos como  *certificados*) vinculam uma entidade, como um indivíduo, organização ou sistema, a um par de chaves público e privado específico. Certificados digitais podem ser considerados como credenciais eletrônicas que verificam a identidade de um indivíduo, sistema ou organização.

**Assinatura digital**

Uma *assinatura digital* vincula a identidade do editor ao conteúdo publicado e fornece um mecanismo para detectar adulterações. Os algoritmos de assinatura digital usam funções de hash criptográfico e algoritmos de criptografia assimétricos (ou par de chaves públicas/privadas). Algumas assinaturas digitais também aproveitam os certificados digitais e a infraestrutura de chave pública (PKI) para vincular chaves públicas à identidade dos proprietários ou distribuidores de conteúdo.

**Distribuidor**

*Distribuidores*  (também conhecidos como  *distribuidores de* conteúdo ou varejistas*) são entidades comerciais que protegem os direitos de distribuição dos proprietários de conteúdo para publicar e divulgar conteúdo aos consumidores. Em alguns casos, a mesma entidade é proprietária de conteúdo e distribuidora de conteúdo.

**Metadados DRM**

Informações que o cliente (ou seja, o Adobe® Flash® Player, o tempo de execução do Adobe® AIR® e o cliente Primetime) envia para identificar o conteúdo solicitado.

**Licença**

Uma *licença *é uma estrutura de dados que contém uma chave criptografada usada para descriptografar o conteúdo associado a uma política. A licença é gerada pelo Adobe Access quando o consumidor solicita conteúdo e é vinculada ao computador do consumidor. Usando uma política como referência, a licença define os direitos disponíveis para o consumidor que baixa conteúdo. Para que o conteúdo seja visualização, o consumidor deve obter uma licença.

**Aquisição de licença**

*A* aquisição de licença é o processo de aquisição de uma licença que permite ao consumidor descriptografar e visualização conteúdo protegido de acordo com um conjunto de regras de uso. A aquisição de licença ocorre quando um cliente envia informações identificando o conteúdo solicitado (os *metadados DRM*) e o certificado da máquina (identificando o computador do consumidor) para o License Server (veja abaixo).

**Servidor de licença**

O* License Server *pode ser integrado aos sistemas de cobrança e autenticação do distribuidor ou do provedor de serviço e pode conter uma lógica comercial para verificar se o consumidor que solicita o conteúdo protegido está autorizado a visualização do conteúdo. Se o usuário estiver autorizado a acessar o conteúdo, o License Server emite uma licença que permite que o cliente do tempo de execução descriptografe e reproduza o conteúdo com base na política e nos direitos associados à conta do consumidor.

Você deve criar e implantar um License Server usando o SDK de acesso ao Adobe.

**Política**

Uma *política* é um container para as regras de uso que determinam como os consumidores podem usar conteúdo protegido. As políticas são definidas independentemente do conteúdo que está sendo protegido. Uma política não aplica direitos até que seja vinculada ao conteúdo por meio da licença. Uma política lista o conjunto de regras de uso, o que significa as permissões ou &quot;direitos&quot; que os consumidores têm ao conteúdo que adquirem. Por exemplo, os proprietários de conteúdo podem criar uma política que garanta que o conteúdo protegido só seja acessível pelos consumidores por um período específico. Essa política é aplicada a todo o conteúdo para o qual o proprietário do conteúdo deseja aplicar essa restrição.

As políticas são criadas usando o SDK de acesso ao Adobe.

**Conteúdo protegido**

*O conteúdo*  protegido (também conhecido como conteúdo ** empacotado) refere-se ao conteúdo de vídeo FLV e F4V que foi criptografado usando o SDK de acesso ao Adobe ou outras ferramentas suportadas.

**Varejistas**

Consulte a entrada para *distribuidores* mais cedo nesta seção.
