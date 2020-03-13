---
seo-title: Configurar Tomcat
title: Configurar Tomcat
uuid: 5f23aa33-29d7-4b41-87a4-59dc5b433de4
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Configurar Tomcat{#configure-tomcat}

No servidor de individualização, modifique o arquivo [!DNL conf/server.xml] do Tomcat para incluir informações adicionais no log de acesso. Você pode usar essas informações para fins de relatório.

1. Localize a configuração para o `AccessLogValve` [!DNL server.xml] em e modifique o padrão conforme mostrado aqui:

   ```
   <Valve className="org.apache.catalina.valves.AccessLogValve" 
   directory="logs" prefix="localhost_access_log." suffix=".txt" 
   pattern="%h %{x-forwarded-for}i %l %u %t &quot;%r&quot; %s %b 
   %{request-id}r" resolveHosts="false"/>
   ```

   `%{x-forwarded-for}i` registrará o valor do `x-forwarded-for` cabeçalho. Se você usar um proxy reverso Apache para encaminhar solicitações ao servidor Tomcat, esse cabeçalho conterá o endereço IP do cliente original, enquanto `%h` registrará o endereço IP do servidor Apache. `%{request-id}r` registrará o identificador da solicitação, que corresponde à ID da solicitação contida no log do aplicativo Individualization.

1. Edite [!DNL conf/server.xml] e defina a `unpackwars` propriedade como false.

   Para os servidores de Individualização e Geração de Chave, é uma boa ideia editar [!DNL conf/server.xml] e definir a `unpackwars` propriedade como `false`. Caso contrário, ao atualizar as WARs, talvez seja necessário limpar também as pastas WAR desembaladas.

>[!NOTE]
>
>Clientes futuros de DRM exigirão que você ative e configure o filtro CORS (Cross-Origin Resource Sharing) disponível para Tomcat. Atualmente, nenhum cliente DRM tem esse requisito.

