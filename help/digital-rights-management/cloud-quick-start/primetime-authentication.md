---
title: Autenticação Adobe Primetime (opcional)
description: Autenticação Adobe Primetime (opcional)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Autenticação Adobe Primetime (opcional) {#adobe-primetime-authentication-optional}

Se a política de DRM usada para empacotar o conteúdo for uma política anônima, uma licença será emitida para todas as solicitações de licença. Como opção, o DRM da Primetime Cloud também é compatível com autenticação por meio da autenticação da Adobe Primetime. Se esse recurso estiver ativado, uma licença não será emitida, a menos que o dispositivo cliente tenha adquirido primeiro um Token de autenticação Primetime e o defina localmente por meio da API do cliente apropriada ( `setAuthenticationToken`) para configurar tokens de autenticação personalizados. Para obter mais informações sobre a integração da autenticação do Primetime ao workflow de autenticação, consulte: [Autenticação Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante a aquisição de licença, se a Política de DRM informar que a autenticação de tempo de memória principal é necessária, o servidor de licenças analisará e validará o token de mídia curta da autenticação Primetime. Se a política de DRM especificar um `ResourceID` ou `RequestorID`, o servidor de licenças também validará o token em relação a essas propriedades. Se não forem definidas, o servidor de licenças especificará as propriedades como &quot;null&quot; durante a validação do token. Só se a validação do token for bem sucedida é que será emitida uma licença; caso contrário, um DRMErrorEvent 3328 com um subcódigo de erro 305 (Usuário não autorizado) será despachado pelo cliente.

Os parâmetros de autenticação do Primetime devem ser especificados na política usada para empacotar o conteúdo destinado à autenticação do Primetime.

As propriedades relevantes são:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Ao usar a autenticação do Primetime em conjunto com o recurso Rotação de licença (DRM), lembre-se de que o SMT (Short Media Token) de autenticação do Primetime tem uma data de validade curta. Se seu aplicativo planeja usar a Rotação de licença (por exemplo, para suportar o *Blackouts* caso de uso), o aplicativo deve estar ciente disso e atualizar seu Token de mídia curta de autenticação do Primetime antes de rodar sua licença.