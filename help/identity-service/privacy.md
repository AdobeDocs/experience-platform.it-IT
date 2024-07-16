---
keywords: Experience Platform;home;argomenti popolari
title: Elaborazione delle richieste di privacy nel servizio Identity
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere ai propri dati personali, rinunciarvi o cancellarli, come indicato da numerose normative sulla privacy. Questo documento descrive i concetti essenziali relativi all’elaborazione delle richieste di accesso a dati personali per il servizio Identity.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 1%

---

# Elaborazione della richiesta di accesso a dati personali in [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere ai propri dati personali, di rifiutarne la vendita o di eliminarli, in conformità alle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento descrive i concetti essenziali relativi all&#39;elaborazione delle richieste di accesso a dati personali per [!DNL Identity Service] in Adobe Experience Platform.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste di accesso ai dati personali per l’archivio dati di identità in Experience Platform. Se prevedi anche di effettuare richieste di privacy per il data lake di Platform o [!DNL Real-Time Customer Profile], consulta la guida sull&#39;elaborazione delle richieste di privacy [nel data lake](../catalog/privacy.md) e la guida sull&#39;elaborazione delle richieste di privacy [per il profilo](../profile/privacy.md) oltre a questa esercitazione.
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta la [documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introduzione

Prima di leggere questa guida, è consigliabile avere una buona conoscenza dei seguenti servizi [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../privacy-service/home.md): gestisce le richieste dei clienti di accedere, rinunciare alle vendite o eliminare i propri dati personali nelle applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati sull&#39;esperienza del cliente collegando le identità tra dispositivi e sistemi.
* [[!DNL Real-Time Customer Profile]](home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Comprendere gli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] esegue il bridging dei dati di identità del cliente tra sistemi e dispositivi. [!DNL Identity Service] utilizza **spazi dei nomi di identità** per fornire contesto ai valori di identità tramite la relazione con il proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, come un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service gestisce un archivio di spazi dei nomi di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle sue esigenze specifiche.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere [panoramica dello spazio dei nomi delle identità](../identity-service/features/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti descrivono come effettuare richieste di accesso a dati personali per [!DNL Identity Service] utilizzando l&#39;API o l&#39;interfaccia utente di [!DNL Privacy Service]. Prima di leggere queste sezioni, ti consigliamo vivamente di rivedere la documentazione dell&#39;[API Privacy Service](../privacy-service/api/getting-started.md) o dell&#39;[interfaccia utente Privacy Service](../privacy-service/ui/overview.md) per i passaggi completi su come inviare un processo per la privacy, incluso come formattare correttamente i dati utente nei payload delle richieste.

### Mediante l’API

Durante la creazione di richieste di processi nell&#39;API, qualsiasi ID fornito in `userIDs` deve utilizzare un `namespace` e un `type` specifici. È necessario fornire uno spazio dei nomi [identity](#namespaces) valido riconosciuto da [!DNL Identity Service] per il valore `namespace`, mentre `type` deve essere `standard` o `unregistered` (rispettivamente per gli spazi dei nomi standard e personalizzati).

Inoltre, l&#39;array `include` del payload della richiesta deve includere i valori del prodotto per i diversi archivi di dati a cui viene effettuata la richiesta. Quando si eseguono richieste a [!DNL Identity], l&#39;array deve includere il valore `Identity`.

La richiesta seguente crea un nuovo processo di privacy in base al RGPD per i dati di un singolo cliente nell&#39;archivio [!DNL Identity]. Nell&#39;array `userIDs` sono forniti due valori di identità per il cliente, uno che utilizza lo spazio dei nomi di identità standard `Email` e l&#39;altro che utilizza uno spazio dei nomi `ECID`. Include inoltre il valore del prodotto per [!DNL Identity] (`Identity`) nell&#39;array `include`:

>[!TIP]
>
>Quando elimini uno spazio dei nomi personalizzato utilizzando l’API, devi specificare il simbolo di identità come spazio dei nomi, invece del nome visualizzato.

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

### Utilizzo dell’interfaccia utente

>[!TIP]
>
>Quando elimini uno spazio dei nomi personalizzato tramite l’interfaccia utente, è necessario specificare il simbolo di identità come spazio dei nomi, anziché il nome visualizzato. Inoltre, non è possibile eliminare spazi dei nomi personalizzati nell’interfaccia utente per le sandbox non di produzione.

Durante la creazione di richieste di processi nell&#39;interfaccia utente, assicurarsi di selezionare **[!UICONTROL Identità]** in **[!UICONTROL Prodotti]** per elaborare i processi per i dati archiviati in [!DNL Identity Service].

![identity-gdpr](./images/identity-gdpr.png)

## Elaborazione richiesta di eliminazione

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l&#39;eliminazione. L’eliminazione della singola identità si basa sullo spazio dei nomi e/o sul valore ID fornito. Inoltre, l’eliminazione avviene per tutte le sandbox associate a una determinata organizzazione.

A seconda che siano stati inclusi anche Real-Time Customer Profile (`ProfileService`) e il data lake (`aepDataLake`) come prodotti nella richiesta di accesso a dati personali per Identity Service (`identity`), diversi set di dati relativi all&#39;identità vengono rimossi dal sistema in momenti potenzialmente diversi:

| Prodotti inclusi | Effetti |
| --- | --- |
| Solo `identity` | L’identità fornita viene eliminata non appena Platform invia la conferma di ricezione della richiesta di eliminazione. Il profilo costruito da tale grafo di identità rimane ancora, ma non verrà aggiornato quando vengono acquisiti nuovi dati, in quanto le associazioni di identità vengono ora rimosse. Anche i dati associati al profilo rimangono nel data lake. |
| `identity` e `ProfileService` | L’identità fornita viene eliminata non appena Platform invia la conferma di ricezione della richiesta di eliminazione. I dati associati al profilo rimangono nel data lake. |
| `identity` e `aepDataLake` | L’identità fornita viene eliminata non appena Platform invia la conferma di ricezione della richiesta di eliminazione. Il profilo costruito da tale grafo di identità rimane ancora, ma non verrà aggiornato quando vengono acquisiti nuovi dati, in quanto le associazioni di identità vengono ora rimosse.<br><br>Quando il prodotto del data lake risponde che la richiesta è stata ricevuta ed è in fase di elaborazione, i dati associati al profilo vengono eliminati in modo non permanente e pertanto non sono accessibili da alcun servizio [!DNL Platform]. Una volta completato il processo, i dati vengono rimossi completamente dal data lake. |
| `identity`, `ProfileService` e `aepDataLake` | L’identità fornita viene eliminata non appena Platform invia la conferma di ricezione della richiesta di eliminazione.<br><br>Quando il prodotto del data lake risponde che la richiesta è stata ricevuta ed è in fase di elaborazione, i dati associati al profilo vengono eliminati in modo non permanente e pertanto non sono accessibili da alcun servizio [!DNL Platform]. Una volta completato il processo, i dati vengono rimossi completamente dal data lake. |

Per ulteriori informazioni sugli stati dei processi di tracciamento, consulta la [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor).

## Passaggi successivi

Dopo aver letto questo documento, ti verranno presentati i concetti importanti relativi all&#39;elaborazione delle richieste di accesso a dati personali in [!DNL Identity Service]. Per informazioni sull&#39;elaborazione delle richieste di accesso a dati personali per altre applicazioni [!DNL Experience Cloud], vedere il documento in [[!DNL Privacy Service] e [!DNL Experience Cloud] applicazioni](../privacy-service/experience-cloud-apps.md).
