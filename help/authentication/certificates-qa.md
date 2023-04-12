---
title: Perguntas e respostas sobre certificados
description: Perguntas e respostas sobre certificados
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---



# Perguntas e respostas sobre certificados {#certificates-q}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

**T1:** É possível registrar certificados no iOS e Android?

**A:** O certificado para iOS e Android é o mesmo na configuração atual. O certificado nativo é usado para ambas as plataformas.

</br>

**T2:** Os mesmos certificados iOS podem ser usados como certificados Primários e de Backup nos ambientes de produção e preparo? Se não for recomendado, pode dar uma explicação?

**A:** Não faz sentido configurar o mesmo certificado do certificado Principal e do Certificado de Backup. Temos o conceito de certificados Primários e de Backup para que possamos configurar vários certificados para um Programador caso o certificado Primário expire ou seja revogado. Ter um certificado de backup dará aos programadores tempo para alterar o principal sem afetar o ambiente de lançamento. Mas você pode usar o mesmo conjunto de certificados Primários e de Backup para os perfis Produção e Armazenamento temporário.

</br>

**P3:** É necessário um novo certificado para páginas da Web que usarão o novo TempPass flexível? 

**A:** O certificado (e qualquer certificado de fato) é configurado no nível da Empresa de mídia e do Programador. FlexibleTempPass é um MVPD, você não precisa configurar qualquer certificado para ele, portanto, se estiver integrando um Programador existente com TempPass flexível, o certificado que já está configurado no nível Programador / Empresa de mídia será usado.

