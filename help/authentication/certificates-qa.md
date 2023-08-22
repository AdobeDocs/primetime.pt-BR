---
title: Perguntas e respostas sobre certificados
description: Perguntas e respostas sobre certificados
exl-id: d4e493b0-4467-42b1-9758-16c5941d8051
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Perguntas e respostas sobre certificados {#certificates-q}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

</br>

**P1:** É possível registrar certificados no iOS e no Android?

**R:** O certificado para iOS e Android é o mesmo na configuração atual. O certificado nativo é usado para ambas as plataformas.

</br>

**P2:** Os mesmos certificados iOS podem ser usados como certificados Primários e de Backup nos ambientes de produção e de preparo? Se isso não for recomendado, você pode oferecer uma explicação?

**R:** Não há razão para configurar o mesmo certificado como certificado Principal e de Backup. Temos o conceito de certificados primários e de backup para que possamos configurar vários certificados para um programador caso o certificado primário expire ou seja revogado. Ter um certificado de backup dará aos programadores tempo para alterar o principal sem afetar o ambiente da versão. Mas você pode usar o mesmo conjunto de certificados primários e de backup para os perfis de produção e de preparo.

</br>

**P3:** É necessário um novo certificado para páginas da Web que usarão o novo TempPass flexível?

**R:** O certificado (e qualquer certificado) é configurado no nível da Empresa de mídia e do Programador. FlexibleTempPass é um MVPD, você não precisa configurar nenhum certificado para ele, portanto, se você estiver integrando um Programador existente com TempPass flexível, o certificado que já está configurado no nível Programador/Empresa de Mídia será usado.
