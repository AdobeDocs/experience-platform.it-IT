---
title: Panoramica del Snowflake
description: Scopri il Snowflake per l’inoltro degli eventi in Adobe Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: abddf0c4-3d4c-4f66-a6e0-c10b54ea3430
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# Panoramica di [!DNL Snowflake]

[[!DNL Snowflake]](https://www.snowflake.com/en/) è un data warehouse cloud in grado di archiviare e analizzare tutti i record di dati in un’unica posizione. Può essere utilizzato per l’immagazzinamento dei dati, i laghi di dati, l’ingegneria dei dati, la scienza dei dati, lo sviluppo di applicazioni di dati e la condivisione e l’utilizzo sicuri di dati condivisi o in tempo reale.

[!DNL Snowflake] è basato su Amazon Web Services (AWS), Microsoft Azure (Azure) e Google Cloud Platform (GCP).

![Un diagramma che mostra [!DNL Snowflake] architettura dei dati.](../../../images/extensions/server/snowflake/snowflake.png)

## Integrazione del Snowflake

Un account di Snowflake può essere ospitato su una qualsiasi delle seguenti piattaforme cloud:

- [AMAZON WEB SERVICES ([!DNL AWS])](https://aws.amazon.com/) - [!DNL AWS] è una piattaforma di cloud computing che offre un’ampia gamma di servizi, tra cui elaborazione distribuita, archiviazione di database, distribuzione di contenuti e servizi di integrazione software-as-a-service (SaaS) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

Consulta la sezione [[!DNL AWS] panoramica](../aws/overview.md) per ulteriori informazioni sull&#39;installazione dell&#39;estensione e sulla configurazione delle regole di inoltro degli eventi.

- [Microsoft Azure ([!DNL Azure])](https://azure.microsoft.com/en-us/products/event-hubs/#overview) - [!DNL Azure] è una piattaforma di cloud computing e un portale online che consente di accedere e gestire i servizi cloud e le risorse forniti da Microsoft.

Consulta la sezione [[!DNL Azure] panoramica](../azure/overview.md) per ulteriori informazioni sull&#39;installazione dell&#39;estensione e sulla configurazione delle regole di inoltro degli eventi.

- [[!DNL Google Cloud Platform]](https://cloud.google.com/) - [!DNL Google Cloud Platform] è una piattaforma di cloud computing che offre un’ampia gamma di servizi, tra cui elaborazione distribuita, archiviazione di database, distribuzione di contenuti e servizi di integrazione software-as-a-service (SaaS) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

Consulta la sezione [[!DNL Google Cloud Platform] panoramica](../google-cloud-platform/overview.md) per ulteriori informazioni sull&#39;installazione dell&#39;estensione e sulla configurazione delle regole di inoltro degli eventi.

Nostro nativo [[!DNL AWS]](../aws/overview.md), [[!DNL Azure]](../azure/overview.md), e [[!DNL Google Cloud Platform]](../google-cloud-platform/overview.md) le estensioni di inoltro eventi consentono ai clienti di raccogliere, arricchire e inoltrare i dati evento lato server in tempo reale ai servizi cloud da utilizzare da [!DNL Snowflake]. Vedi sotto:

![Il [!DNL Snowflake] diagramma di reporting che mostra il collegamento tra [!DNL AWS] e [!DNL Azure].](../../../images/extensions/server/snowflake/snowflake-workflow.png)

## Passaggi successivi

Questa guida fornisce una panoramica di [!DNL Snowflake] e l&#39;uso di [!DNL AWS] e [!DNL Azure] estensioni di inoltro eventi.

Per ulteriori informazioni su [!DNL AWS] e [!DNL Azure] funzionalità di inoltro degli eventi in Experienci Platform, consulta [[!DNL AWS] panoramica dell’estensione](../aws/overview.md) e [[!DNL Azure] panoramica dell’estensione](../azure/overview.md).
