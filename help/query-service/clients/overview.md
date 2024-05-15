---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;connettere;connettersi al servizio query;aqua data studio;Aqua Data Studio;Looker;looker;Postico;postico;postico;Power BI;power bi;psql;rstudio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Connettere i client a Query Service
description: In questo documento viene illustrato come connettersi a Query Service da diverse applicazioni client desktop e come verificare tali connessioni.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Connetti client a [!DNL Query Service]

Questa sezione spiega come connettersi a [!DNL Query Service] da diverse applicazioni client desktop e come verificare tali connessioni. [!DNL Query Service] utilizza [!DNL PostgreSQL] , quindi le istruzioni in questa sezione spiegano come utilizzare [!DNL PostgreSQL] strumenti e driver per la connessione e la scrittura di query.

>[!IMPORTANT]
>
>I certificati TLS/SSL sugli ambienti di produzione per l’API Query Service Interactive Postgres sono stati aggiornati mercoledì 24 gennaio 2024.<br>Anche se si tratta di un requisito annuale, in questa occasione il certificato principale nella catena è cambiato anche in seguito all’aggiornamento della gerarchia dei certificati da parte del provider di certificati TLS/SSL di Adobe. Questo problema può interessare alcuni client Postgres se nell’elenco delle autorità di certificazione manca il certificato radice. Ad esempio, un client CLI PSQL potrebbe dover aggiungere i certificati radice a un file esplicito `~/postgresql/root.crt`, altrimenti può causare un errore. Ad esempio, `psql: error: SSL error: certificate verify failed`. Consulta la [documentazione ufficiale PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) per ulteriori informazioni su questo problema.<br>Il certificato principale da aggiungere può essere scaricato da [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

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
>In qualità di utente Power BI e Tableau, puoi collegare il Customer Journey Analytics agli strumenti di business intelligence dalla scheda Credenziali di Query Service. Per istruzioni su come utilizzare, consulta la documentazione sulle credenziali. [collegare gli strumenti BI al Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
