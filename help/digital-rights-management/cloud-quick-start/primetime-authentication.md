---
seo-title: Autenticação do Adobe Primetime (opcional)
title: Autenticação do Adobe Primetime (opcional)
uuid: fa6225d6-e0e5-4fcc-ac26-4ff54f9f334a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Autenticação do Adobe Primetime (opcional) {#adobe-primetime-authentication-optional}

Se a política de DRM usada para disponibilizar o conteúdo for uma política anônima, uma licença será emitida para todas as solicitações de licença. Como opção, o DRM da Primetime Cloud também oferece suporte à autenticação por meio da autenticação do Adobe Primetime. Se esse recurso estiver ativado, uma licença não será emitida, a menos que o dispositivo cliente tenha adquirido primeiro um Token de autenticação Primetime e o defina localmente por meio da API do cliente apropriada ( `setAuthenticationToken`) para configurar tokens de autenticação personalizados. Para obter mais informações sobre a integração da autenticação Primetime ao fluxo de trabalho de autenticação, consulte: Autenticação [do Adobe Primetime.](https://tve.helpdocsonline.com/home)

Durante a aquisição da licença, se a Política de DRM informar que a autenticação de tempo de impressão é obrigatória, o servidor de licença analisará e validará o token de mídia curta de autenticação Primetime. Se a política DRM especificar um `ResourceID` ou `RequestorID`, o servidor de licenças também validará o token em relação a essas propriedades. Se não estiverem definidas, o servidor de licenças especificará as propriedades como &quot;null&quot; durante a validação do token. Só será emitida uma licença se a validação do token for bem sucedida; caso contrário, um DRMErrorEvent 3328 com um código de suberro 305 (Usuário não autorizado) será despachado pelo cliente.

Os parâmetros de autenticação Primetime devem ser especificados na política usada para disponibilizar o conteúdo destinado à autenticação Primetime.

As propriedades relevantes são:

```
#policy.customProp.1=adobePass.required=<TRUE or FALSE> 
#policy.customProp.1=adobePass.requestorID=<Requestor ID String> 
#policy.customProp.1=adobePass.resourceID=<Resource ID String>
```

>[!NOTE]
>
>Ao usar a autenticação Primetime em conjunto com o recurso Rotação de licença (DRM), lembre-se de que o SMT (Short Media Token) de autenticação Primetime tem uma data de validade curta. Se seu aplicativo planeja usar a Rotação de licença (por exemplo, para suportar o caso de uso de *Blecautes* ), o aplicativo deve estar ciente disso e atualizar seu Token de mídia curta de autenticação Primetime antes de girar sua licença.