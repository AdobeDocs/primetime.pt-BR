---
title: Autenticação do Adobe Primetime (opcional)
description: Autenticação do Adobe Primetime (opcional)
copied-description: true
exl-id: 59fbbefa-0c84-474a-ace9-141b50ad5f5f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Autenticação do Adobe Primetime (opcional) {#adobe-primetime-authentication-optional}

Se a política DRM usada para empacotar o conteúdo for uma política anônima, uma licença será emitida para todas as solicitações de licença. Como opção, o DRM do Primetime Cloud também oferece suporte à autenticação por meio da autenticação da Adobe Primetime. Se esse recurso estiver ativado, uma licença não será emitida a menos que o dispositivo cliente tenha adquirido primeiro um token de autenticação do Primetime e o definido localmente por meio da API do cliente apropriada ( `setAuthenticationToken`) para definir tokens de autenticação personalizados. Para obter mais informações sobre como integrar a autenticação do Primetime ao seu fluxo de trabalho de autenticação, consulte: [Autenticação Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante a aquisição da licença, se a Política DRM indicar que a autenticação Pri metime é necessária, o servidor de licença analisará e validará o token Short Media de autenticação Primetime. Se a política de DRM especificar uma `ResourceID` ou `RequestorID`, o servidor de licenças também validará o token em relação a essas propriedades. Se não forem definidas, o servidor de licença especificará as propriedades como &quot;null&quot; durante a validação do token. Uma licença será emitida somente se a validação do token for bem-sucedida; caso contrário, um DRMErrorEvent 3328 com um código de suberro 305 (Usuário não autorizado) será despachado pelo cliente.

Os parâmetros de autenticação do Primetime devem ser especificados na política usada para empacotar o conteúdo destinado a exigir a autenticação do Primetime.

As propriedades relevantes são:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Ao usar a autenticação do Primetime em conjunto com o recurso Rotação de licenças (DRM), lembre-se de que o token de mídia curta (SMT) de autenticação do Primetime tem uma data de validade curta. Se seu aplicativo planeja usar a Rotação de licenças (por exemplo, para dar suporte ao *Blecouts* caso de uso), o aplicativo deve estar ciente disso e atualizar seu Token de mídia curta de autenticação do Primetime antes de girar sua licença.
