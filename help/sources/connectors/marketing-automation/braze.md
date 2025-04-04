---
title: Panoramica di Braze Currents Source
description: Scopri come inviare dati in streaming da Braze Currents ad Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 4%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>L&#39;origine [!DNL Braze Currents] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione dei dati dalle applicazioni Streaming. Il supporto per i provider di streaming include [!DNL Braze Currents].

[!DNL Braze] potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. [!DNL Braze Currents] è un flusso di dati in tempo reale di eventi di coinvolgimento dalla piattaforma Braze che rappresenta l&#39;esportazione più solida ma granulare della piattaforma [!DNL Braze].

## Prerequisiti

Per completare i passaggi descritti in questa guida, è necessario:

* Accesso a [Adobe Experience Platform](https://platform.adobe.com) e autorizzazione per la creazione di una nuova connessione di origine streaming.
* Accesso a [[!DNL Braze] dashboard](https://dashboard.braze.com/sign_in), licenza [Current Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) non utilizzata e autorizzazioni per la creazione di un connettore. Per ulteriori informazioni, leggere i [requisiti per configurare [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Raccogli le credenziali richieste

Per inviare correttamente i dati di [!DNL Braze Currents] ad Experience Platform, è necessario immettere le seguenti credenziali Experience Platform nel dashboard dell&#39;interfaccia utente di [!DNL Braze].

| Campo | Descrizione |
| --- | --- |
| ID client | L’ID client associato alla tua sorgente Experience Platform. |
| Segreto client | Il segreto client associato alla tua origine Experience Platform. |
| ID tenant | L’ID tenant associato alla tua sorgente Experience Platform. |
| Nome sandbox | La sandbox associata alla tua origine Experience Platform. |
| ID flusso di dati | L’ID del flusso di dati associato alla sorgente di Experience Platform. |
| Endpoint di streaming | L’endpoint di streaming associato alla tua origine Experience Platform. **Nota**: [!DNL Braze] converte automaticamente questo elemento nell&#39;endpoint di streaming batch. |

Per informazioni su come recuperare questi valori, consulta la guida [guida introduttiva alle API di Experience Platform](../../../landing/api-authentication.md). Per informazioni sull&#39;utilizzo del dashboard [!DNL Braze], leggere la guida di [!DNL Braze] su come [Passare a Correnti](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Passaggi successivi

Dopo aver letto questo documento, hai completato la configurazione dei prerequisiti necessaria per inviare dati dal tuo account [!DNL Braze Currents] ad Experience Platform. Ora puoi passare alla guida su [connessione [!DNL Braze Currents] ad Experience Platform tramite l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/braze.md).
