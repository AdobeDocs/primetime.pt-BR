---
title: Configurar Tomcat
description: Configurar Tomcat
copied-description: true
exl-id: 766b66dd-6070-4b0d-a860-a426fca05e56
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Configurar Tomcat{#configure-tomcat}

No servidor de individualização, modifique o do Tomcat [!DNL conf/server.xml] arquivo para incluir informações adicionais no log de acesso. É possível usar essas informações para fins de relatório.

1. Localize a configuração para o `AccessLogValve` in [!DNL server.xml] e modifique o padrão como mostrado aqui:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrará o valor de `x-forwarded-for` cabeçalho. Se você usar um proxy reverso do Apache para encaminhar solicitações ao servidor Tomcat, esse cabeçalho conterá o endereço IP do cliente original, enquanto `%h` O registra o endereço IP do servidor Apache. `%{request-id}r` registrará o identificador da solicitação, que corresponde à ID da solicitação contida no log de aplicativo de individualização.

1. Editar [!DNL conf/server.xml] e defina o `unpackwars` para falso.

   Para os servidores de Individualização e Geração de Chaves, é uma boa ideia editar [!DNL conf/server.xml] e defina o `unpackwars` propriedade para `false`. Caso contrário, ao atualizar as WARs, talvez você também precise limpar as pastas WAR desempacotadas.

>[!NOTE]
>
>Futuros clientes DRM exigirão que você ative e configure o filtro CORS (Cross-Origin Resource Sharing) que está disponível para Tomcat. No momento, nenhum cliente DRM tem esse requisito.
