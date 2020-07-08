---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connetti con Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Connetti con Aqua Data Studio

Questo documento descrive i passaggi necessari per collegare Aqua Data Studio a  Adobe Experience Platform Query Service.

Dopo aver installato Aqua Data Studio, è prima necessario registrare il server. Dal menu principale, fate clic su **Server**, quindi su **Register Server**.

![](../images/clients/aqua-data-studio/register-server.png)

Viene visualizzata la finestra di dialogo *Registra server* . Nella scheda *Generale* , selezionare **PostgreSQL** dall&#39;elenco a sinistra. Nella finestra di dialogo visualizzata, fornite i seguenti dettagli per le impostazioni del server.

- **Nome**: Nome della connessione.
- **Nome di login e password**: Le credenziali di accesso che verranno utilizzate. Il nome utente assume la forma di `ORG_ID@AdobeOrg`.
- **Host e porta**: L&#39;endpoint host e la relativa porta per il servizio query.
- **Database:** Il database che verrà utilizzato.

>[!NOTE]
>
>Per ulteriori informazioni su come trovare le credenziali di accesso, l&#39;host, la porta e il nome del database, visitare la pagina delle [credenziali su Platform](https://platform.adobe.com/query/configuration). Per trovare le credenziali, accedere ad Platform, fare clic su **Query**, quindi su **Credenziali**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selezionare la scheda **Driver** . In *Parametri*, imposta il valore come `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Dopo aver inserito i dettagli di connessione, fate clic su **Verifica connessione** per verificare il corretto funzionamento delle credenziali. Se la connessione ha esito positivo, fate clic su **Salva** per registrare il server. La connessione viene visualizzata sul *dashboard* dopo la registrazione, confermando che è ora possibile connettersi al server e visualizzare i relativi oggetti schema.

## Passaggi successivi

Ora che si è connessi a Query Service, è possibile utilizzare *Query Analyzer* in Aqua Data Studio per eseguire e modificare le istruzioni SQL. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida [alle query](../creating-queries/creating-queries.md)in esecuzione.