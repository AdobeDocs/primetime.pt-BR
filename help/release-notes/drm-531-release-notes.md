---
title: Notas de versão do DRM 5.3.1
description: As Notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# Notas de versão do DRM 5.3.1 {#drm-release-notes}

As Notas de versão do DRM 5.3.1 descrevem os novos recursos e os problemas conhecidos no DRM 5.3.1.

## Novos recursos na versão 5.3 {#new-features}

* **Parada segura -** Você pode especificar se a reprodução é interrompida ou continua no final de uma janela de reprodução.
* **Proteção de saída baseada em resolução (RBOP) -** Você pode especificar as restrições de saída com base nas resoluções de pixel.
* **Gating do CDM -** para oferecer suporte a HTML5, o Adobe atualizou o servidor de licença da Implementação de referência incluído no SDK Java do Adobe Primetime DRM (antigo DRM de acesso de Adobe) para poder consumir todas as mensagens de protocolo DRM em um único ponto de extremidade de URL. Essa consolidação de métodos de URL HTTP é necessária para estar em conformidade com a especificação EME HTML5 (Encrypted Media Extension), que, por sua vez, é necessária para ser implementada por fornecedores DRM CDM (Content Decryption Module). Anteriormente, esses eram os únicos pontos de extremidade de URL expostos pelo servidor de licença de Implementação de Referência:

   * /flashaccess/i15n/v3 (individualização)
   * /flashaccess/license/v5 (Solicitação de licença)
   * /flashaccess/licenseRet/v5 (Retorno de Licença)
   * /flashaccess/getServerVersion/v5 (Obter Versão do Servidor)

Agora, todas as solicitações (originadas de um CDM HTML5) podem ser direcionadas a um único terminal: /req

Essa alteração é compatível com versões anteriores de plataformas não-CDM, como Flash Player, Android, iOS.

* **Descarregamento de RBOP -** Específico do espaço HTML5, a RBOP contém o recurso de download automático, onde, se uma taxa de bits exceder a taxa de bits permitida especificada na política de DRM, o conteúdo será reduzido para a resolução máxima permitida. Por exemplo, se um fluxo de 1080p for transmitido a um cliente que está exibindo o conteúdo em um monitor não compatível com HDCP, a política de DRM pode indicar que a resolução máxima deve ser de 720p. O DRM do Primetime decodificará o fluxo de 1080p e, em seguida, baixará para 720p antes de renderizá-lo na tela. Se o navegador reproduzindo o vídeo for arrastado para um monitor que suporta HDCP, o DRM do Primetime interromperá o download do conteúdo e permitirá que ele seja reproduzido em 1080.

## Problemas conhecidos na versão 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` Gera mensagens de log para  `flashaccess-global.log.`Você deve garantir que o  `flashaccess-global.log` arquivo esteja no mesmo diretório com Hasher.bat.

* A saída de algumas das chamadas `toJSON()`retorna `Strings` que não são totalmente compatíveis com JSON ou totalmente compatíveis de maneira independente (ou seja, sem composição de estruturas JSON).

* O servidor de chave Xbox aceita solicitações de chave que têm o valor de versão não igual a 1.

O servidor de chaves Xbox só deve oferecer suporte a solicitações de chaves com a versão igual a 1, mas, no momento, o servidor aceita solicitações de chaves, onde a versão não é 1.

* O servidor de chaves Xbox não valida uma política corretamente.

O servidor de chaves Xbox não deve aceitar políticas que estejam fora da data de validade, mas atualmente, o servidor as aceita independentemente.

* O servidor de chaves Xbox deve rejeitar uma solicitação de chave que contenha um metadados que foi criado com um certificado de empacotador incorreto.
* O valor retornado de algumas estruturas JSON não está formatado corretamente para classes relacionadas à Proteção de Saída com base em Resolução.

Várias classes implementam um método toJSON() que deve retornar uma representação compatível com JSON desse objeto como uma String, mas atualmente o valor retornado não é totalmente compatível com JSON.

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
