---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Query Service
topic: query templates
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# [!DNL Query Service] guida per sviluppatori

Questa guida per gli sviluppatori fornisce i passaggi necessari per eseguire varie operazioni nell&#39; [!DNL Query Service] API  Adobe Experience Platform.

## Introduzione

Questa guida richiede una conoscenza approfondita dei vari servizi  Adobe Experience Platform coinvolti nell&#39;utilizzo [!DNL Query Service].

- [!DNL Query Service](../home.md): Consente di eseguire query sui set di dati e acquisire le query risultanti come nuovi set di dati in [!DNL Experience Platform].
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornisce sandbox virtuali che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrete conoscere per poter utilizzare con successo [!DNL Query Service] l&#39;API.

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate in questa documentazione per le chiamate API di esempio, consultate la sezione relativa alla [lettura delle chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Experience Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Platform] API, come illustrato di seguito:

- Autorizzazione: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sull’utilizzo delle sandbox in [!DNL Experience Platform], consultate la documentazione [sulla panoramica delle](../../sandboxes/home.md)sandbox.

## Chiamate API di esempio

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39; [!DNL Query Service] API. I documenti seguenti descrivono le varie chiamate API che potete effettuare tramite l&#39; [!DNL Query Service] API. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.

- [Query](queries.md)
- [Parametri di connessione](connection-parameters.md)
- [Query pianificate](scheduled-queries.md)
- [Esecuzione per query pianificate](runs-scheduled-queries.md)
- [Modelli di query](query-templates.md)

## Passaggi successivi

Ora che hai imparato a effettuare chiamate utilizzando l&#39; [!DNL Query Service] API, puoi creare query non interattive personalizzate. Per ulteriori informazioni sulla creazione di query, consultate la guida [di riferimento](../sql/overview.md)SQL.