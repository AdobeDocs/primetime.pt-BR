---
title: Lista de permissões para SWF do Adobe® Flash® Player com permissão para reproduzir conteúdo protegido
description: Lista de permissões para SWF do Adobe® Flash® Player com permissão para reproduzir conteúdo protegido
copied-description: true
exl-id: e6adf548-c5d5-45d0-bcd3-ef5185092291
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Lista de permissões para SWF do Adobe® Flash® Player com permissão para reproduzir conteúdo protegido {#allowlist-for-adobe-flash-player-swfs-allowed-to-play-protected-content}

Especifica os arquivos SWF que podem reproduzir conteúdo. Especifique o arquivo de SWF por um URL de SWF ou um resumo SHA-256 calculado usando o conteúdo do SWF. Se você usar o resumo SHA-256, essa regra de uso também especifica a quantidade máxima de tempo para permitir que o cliente baixe e verifique o SWF.

Exemplo de caso de uso: equivalente conceitualmente à Verificação de SWF no caso do Flash Media Server, mas aplicado no lado do cliente para limitar quais players de vídeo podem reproduzir o conteúdo. Observe que o comportamento de Acesso ao Adobe é diferente no que diz respeito à imposição do SWF filho em comparação ao SWF pai.
