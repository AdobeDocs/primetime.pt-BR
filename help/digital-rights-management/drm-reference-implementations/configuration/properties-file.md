---
description: nulo
seo-description: nulo
seo-title: Arquivo de propriedades do servidor de licenças
title: Arquivo de propriedades do servidor de licenças
uuid: 5e94ed1f-1dbf-4506-a097-183fcd5d25ef
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Arquivo de propriedades do servidor de licenças{#license-server-properties-file}

O servidor de licenças faz referência às propriedades definidas no arquivo [!DNL flashaccess-refimpl.properties]. Você pode consultar esse arquivo diretamente para obter detalhes sobre valores específicos e informações de uso sobre cada propriedade. Uma amostra totalmente funcional é fornecida no diretório [!DNL resources] da implementação de referência ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources/).`).

**Credenciais**  - O arquivo de propriedades inclui configurações para o local das credenciais que o Adobe emite para você. Você pode especificar essas credenciais em um arquivo [!DNL .pfx] com uma senha ou fornecer um alias e uma senha para uma credencial armazenada em um HSM. É necessário configurar pelo menos as propriedades relacionadas à Credencial de Transporte e à Credencial do License Server. Especifique os locais dos arquivos de credenciais em relação ao diretório especificado na propriedade `config.resourcesDirectory`.

**Flash Media Rights Management Server**  - O  `flashaccess-refimpl.properties` arquivo também inclui várias propriedades relacionadas ao conteúdo do empacotamento. Essas propriedades são usadas apenas para a conversão de metadados 1.x do Flash Media Rights Management Server. Depois de modificar os valores neste arquivo de propriedade, para que as alterações entrem em vigor, reinicie o servidor de licenças.
