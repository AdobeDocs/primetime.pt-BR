---
title: Arquivo de propriedades do servidor de licenças
description: Arquivo de propriedades do servidor de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Arquivo de propriedades do servidor de licenças{#license-server-properties-file}

O servidor de licenças faz referência às propriedades definidas no arquivo [!DNL flashaccess-refimpl.properties]. Você pode consultar esse arquivo diretamente para obter detalhes sobre valores específicos e informações de uso sobre cada propriedade. Uma amostra totalmente funcional é fornecida no diretório [!DNL resources] da implementação de referência ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenciais**  - O arquivo de propriedades inclui configurações para o local das credenciais que o Adobe emite para você. Você pode especificar essas credenciais em um arquivo [!DNL .pfx] com uma senha ou fornecer um alias e senha para uma credencial armazenada em um HSM. Você precisa pelo menos configurar as propriedades que estão relacionadas à Credencial de Transporte e à Credencial do Servidor de Licenças. Especifique os locais dos arquivos de credenciais em relação ao diretório especificado na propriedade `config.resourcesDirectory`.

**Servidor Flash do Rights Management Media**  - O  `flashaccess-refimpl.properties` arquivo também inclui várias propriedades relacionadas ao conteúdo do empacotamento. Essas propriedades são usadas somente para a conversão de metadados do Flash Media Rights Management Server 1.x. Depois de modificar os valores neste arquivo de propriedade, para que as alterações entrem em vigor, reinicie o servidor de licenças.
