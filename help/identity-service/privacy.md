---
keywords: Experience Platform;home;argomenti popolari
title: Elaborazione della richiesta di privacy nel servizio Identity
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o alla cancellazione dei propri dati personali come delineato da numerose normative sulla privacy. Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di accesso a dati personali per il servizio Identity.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: f0fa8d77e6184314056f8e70205a9b42409d09d5
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---

# Elaborazione della richiesta di privacy in [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti per accedere, rinunciare alla vendita o cancellare i propri dati personali come delineato dalle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per [!DNL Identity Service] in Adobe Experience Platform.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste di accesso a dati personali per l’archivio dati di Identity in Experience Platform. Se prevedi anche di effettuare richieste di privacy per Platform Data Lake o [!DNL Real-time Customer Profile], consulta la guida su [elaborazione delle richieste di privacy in Data Lake](../catalog/privacy.md) e alla guida [elaborazione della richiesta di accesso a dati personali per il profilo](../profile/privacy.md) oltre a questa esercitazione.
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta [Documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introduzione

Si consiglia di avere una comprensione operativa dei seguenti elementi [!DNL Experience Platform] servizi prima di leggere questa guida:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestisce le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o all’eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Real-time Customer Profile]](home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza **spazi dei nomi delle identità** fornire un contesto ai valori d&#39;identità collegandoli al loro sistema d&#39;origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service conserva un archivio di namespace di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; ed &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedi [panoramica dello spazio dei nomi identità](../identity-service/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti illustrano come effettuare richieste di accesso a dati personali per [!DNL Identity Service] utilizzando [!DNL Privacy Service] API o interfaccia utente. Prima di leggere queste sezioni, si consiglia vivamente di rivedere il [API Privacy Service](../privacy-service/api/getting-started.md) o [Interfaccia utente di Privacy Service](../privacy-service/ui/overview.md) documentazione completa sui passaggi per l’invio di un processo relativo alla privacy, inclusa la modalità di formattazione corretta dei dati utente nei payload della richiesta.

### Mediante l’API

Quando crei richieste di lavoro nell&#39;API, qualsiasi ID fornito in `userIDs` deve utilizzare un `namespace` e `type`. Una valida [spazio dei nomi identità](#namespaces) riconosciuti [!DNL Identity Service] devono essere previste `namespace` , mentre `type` deve `standard` o `unregistered` (per namespace standard e personalizzati, rispettivamente).

Inoltre, il `include` la matrice del payload della richiesta deve includere i valori di prodotto per i diversi archivi di dati in cui viene effettuata la richiesta. Durante l’esecuzione di richieste a [!DNL Identity], la matrice deve includere il valore `Identity`.

La seguente richiesta crea un nuovo processo per la privacy in base al RGPD per i dati di un singolo cliente nel [!DNL Identity] archiviare. Per il cliente vengono forniti due valori di identità nel `userIDs` array; uno che utilizza lo standard `Email` spazio dei nomi dell&#39;identità e l&#39;altro tramite un `ECID` Lo spazio dei nomi include anche il valore di prodotto per [!DNL Identity] (`Identity`) nel `include` array:

>[!TIP]
>
>Quando si elimina uno spazio dei nomi personalizzato utilizzando l’API, è necessario specificare il simbolo di identità come spazio dei nomi, anziché come nome visualizzato.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### Utilizzo dell’interfaccia

>[!TIP]
>
>Quando si elimina uno spazio dei nomi personalizzato utilizzando l’interfaccia utente, è necessario specificare il simbolo di identità come spazio dei nomi, anziché come nome visualizzato. Inoltre, non è possibile eliminare i namespace personalizzati nell’interfaccia utente per le sandbox non di produzione.

Quando crei richieste di lavoro nell’interfaccia utente, assicurati di selezionare **[!UICONTROL Identità]** sotto **[!UICONTROL Prodotti]** al fine di elaborare i processi per i dati memorizzati in [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di cancellazione da [!DNL Privacy Service], [!DNL Platform] invia conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. L’eliminazione della singola identità si basa sul namespace e/o sul valore ID fornito. Inoltre, la cancellazione avviene per tutte le sandbox associate a una determinata organizzazione IMS.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all’elaborazione delle richieste di privacy in [!DNL Identity Service]. Per informazioni sull’elaborazione delle richieste di accesso a dati personali per altri [!DNL Experience Cloud] applicazioni, vedere il documento in [[!DNL Privacy Service] and [!DNL Experience Cloud] applicazioni](../privacy-service/experience-cloud-apps.md).
