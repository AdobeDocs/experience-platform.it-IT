---
title: Panoramica dell’origine delle correnti di brasatura
description: Scopri come inviare dati in streaming da Braze Currents a Experienci Platform.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>Il [!DNL Braze Currents] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experienci Platform fornisce supporto per l’acquisizione di dati dalle applicazioni Streaming. Il supporto per i provider di streaming include [!DNL Braze Currents].

[!DNL Braze] potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. [!DNL Braze Currents] è un flusso di dati in tempo reale di eventi di coinvolgimento dalla piattaforma Braze che rappresenta l’esportazione più solida ma granulare dal [!DNL Braze] piattaforma.

## Prerequisiti

Per completare i passaggi descritti in questa guida, è necessario:

* Accesso a [Adobe Experience Platform](https://platform.adobe.com) e l’autorizzazione per creare una nuova connessione sorgente di streaming.
* Accesso al [[!DNL Braze] dashboard](https://dashboard.braze.com/sign_in), non utilizzato [Licenza del connettore corrente](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents), e le autorizzazioni per creare un connettore. Per ulteriori informazioni, leggere [requisiti per l&#39;impostazione [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Raccogli le credenziali richieste

Per inviare correttamente il [!DNL Braze Currents] dati di Experience Platform, è necessario immettere le seguenti credenziali di Experience Platform nel [!DNL Braze] Dashboard dell’interfaccia utente.

| Campo | Descrizione |
| --- | --- |
| ID client | L’ID client associato alla sorgente dell’Experience Platform. |
| Segreto client | Il segreto client associato alla tua origine Experience Platform. |
| ID tenant | L’ID tenant associato alla tua origine Experience Platform. |
| Nome sandbox | La sandbox associata alla sorgente di Experience Platform. |
| ID flusso di dati | L’ID del flusso di dati associato alla sorgente di Experience Platform. |
| Endpoint di streaming | L’endpoint di streaming associato alla sorgente di Experience Platform. **Nota**: [!DNL Braze] converte automaticamente questo valore nell&#39;endpoint di streaming batch. |

Per informazioni su come recuperare questi valori, consulta la guida su [introduzione alle API di Platform](../../../landing/api-authentication.md). Per informazioni sull&#39;utilizzo di [!DNL Braze] , leggi la [!DNL Braze] guida su come [Passa a correnti](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Passaggi successivi

Una volta letto questo documento, avrai completato la configurazione dei prerequisiti necessaria per inviare in streaming i dati dal tuo [!DNL Braze Currents] da Experience Platform. Ora puoi passare alla guida su [connessione [!DNL Braze Currents] per Experienci Platform utilizzando l’interfaccia utente di](../../tutorials/ui/create/marketing-automation/braze.md).