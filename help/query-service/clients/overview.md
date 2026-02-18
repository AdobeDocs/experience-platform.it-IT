---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;connettere;connettersi al servizio query;aqua data studio;Aqua Data Studio;Looker;Postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Connettere i client a Query Service
description: In questo documento viene illustrato come connettersi a Query Service da diverse applicazioni client desktop e come verificare tali connessioni.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Connettere i client a Query Service

Questa sezione spiega come connettersi a Query Service da diverse applicazioni client desktop e come verificare tali connessioni. Query Service utilizza il protocollo PostgreSQL, pertanto le istruzioni contenute in questa sezione spiegano come utilizzare gli strumenti e i driver PostgreSQL per connettersi e scrivere query.

>[!IMPORTANT]
>
>I certificati TLS/SSL sugli ambienti di produzione per l’API Query Service Interactive Postgres sono stati aggiornati mercoledì 24 gennaio 2024.<br>Anche se si tratta di un requisito annuale, in questa occasione anche il certificato radice nella catena è cambiato in seguito all’aggiornamento della gerarchia dei certificati da parte del provider di certificati TLS/SSL di Adobe. Questo problema può interessare alcuni client Postgres se nell’elenco delle autorità di certificazione manca il certificato radice. Ad esempio, per un client CLI PSQL potrebbe essere necessario aggiungere i certificati radice a un file esplicito `~/postgresql/root.crt`, altrimenti potrebbe verificarsi un errore, ad esempio `psql: error: SSL error: certificate verify failed`. Per ulteriori informazioni su questo problema, consulta la [documentazione ufficiale di PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES).<br>Il certificato radice da aggiungere può essere scaricato da [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Le istruzioni sono fornite per i seguenti clienti:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>In qualità di utente di Power BI e Tableau, puoi collegare Customer Journey Analytics ai tuoi strumenti di business intelligence utilizzando le credenziali fornite nella scheda Credenziali di Query Service. Consulta la documentazione sulle credenziali per istruzioni su come [collegare gli strumenti di business intelligence a Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
