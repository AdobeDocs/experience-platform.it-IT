---
title: Panoramica di Braze Currents Source
description: Scopri come inviare dati in streaming da Braze Currents a Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>L&#39;origine [!DNL Braze Currents] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati dalle applicazioni Streaming. Il supporto per i provider di streaming include [!DNL Braze Currents].

[!DNL Braze] potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. [!DNL Braze Currents] è un flusso di dati in tempo reale di eventi di coinvolgimento dalla piattaforma Braze che rappresenta l&#39;esportazione più solida ma granulare della piattaforma [!DNL Braze].

## Prerequisiti

Per completare i passaggi descritti in questa guida, è necessario:

* Accesso a [Adobe Experience Platform](https://platform.adobe.com) e autorizzazione per la creazione di una nuova connessione di origine streaming.
* Accesso a [[!DNL Braze] dashboard](https://dashboard.braze.com/sign_in), licenza [Current Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) non utilizzata e autorizzazioni per la creazione di un connettore. Per ulteriori informazioni, leggere i [requisiti per configurare [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Raccogli le credenziali richieste

Per inviare correttamente i dati di [!DNL Braze Currents] a Experience Platform, è necessario immettere le credenziali di Experience Platform seguenti nel dashboard dell&#39;interfaccia utente di [!DNL Braze].

| Campo | Descrizione |
| --- | --- |
| ID client | L’ID client associato alla sorgente dell’Experience Platform. |
| Segreto client | Il segreto client associato alla tua origine Experience Platform. |
| ID tenant | L’ID tenant associato alla tua origine Experience Platform. |
| Nome sandbox | La sandbox associata alla sorgente di Experience Platform. |
| ID flusso di dati | L’ID del flusso di dati associato alla sorgente di Experience Platform. |
| Endpoint di streaming | L’endpoint di streaming associato alla sorgente di Experience Platform. **Nota**: [!DNL Braze] converte automaticamente questo elemento nell&#39;endpoint di streaming batch. |

Per informazioni su come recuperare questi valori, consulta la guida [guida introduttiva alle API di Platform](../../../landing/api-authentication.md). Per informazioni sull&#39;utilizzo del dashboard [!DNL Braze], leggere la guida di [!DNL Braze] su come [Passare a Correnti](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Passaggi successivi

Dopo aver letto questo documento, hai completato la configurazione dei prerequisiti necessaria per inviare dati dall&#39;account [!DNL Braze Currents] all&#39;Experience Platform. Ora puoi passare alla guida in [connessione [!DNL Braze Currents] all&#39;Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/braze.md).
