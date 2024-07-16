---
description: Scopri come configurare le identità di destinazione supportate per le destinazioni create con Destination SDK.
title: Configurazione dello spazio dei nomi dell’identità
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: 606685c1f0b607ca586e477cb9825ec551d537cc
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 3%

---

# Configurazione dello spazio dei nomi dell’identità

In questo Experience Platform vengono utilizzati gli spazi dei nomi delle identità per descrivere il tipo di identità specifiche. Ad esempio, uno spazio dei nomi di identità denominato `Email` identifica un valore come `name@email.com` come indirizzo e-mail.

A seconda del tipo di destinazione creato (in streaming o basata su file), tieni presente i seguenti requisiti di spazio dei nomi delle identità:

* Durante la creazione di destinazioni in tempo reale (streaming) tramite Destination SDK, oltre a [configurare uno schema partner](schema-configuration.md) in cui gli utenti possono mappare gli attributi e le identità del profilo, devi anche definire *almeno uno* spazi dei nomi di identità supportati dalla piattaforma di destinazione. Ad esempio, se la piattaforma di destinazione accetta e-mail con hash e [!DNL IDFA], è necessario definire queste due identità come [descritte più avanti in questo documento](#supported-parameters).

  >[!IMPORTANT]
  >
  >Quando si attivano tipi di pubblico su destinazioni di streaming, gli utenti devono mappare anche _almeno un&#39;identità di destinazione_, oltre agli attributi del profilo di destinazione. In caso contrario, i tipi di pubblico non verranno attivati nella piattaforma di destinazione.

* Durante la creazione di destinazioni basate su file tramite Destination SDK, la configurazione degli spazi dei nomi di identità è _facoltativa_.

Per ulteriori informazioni sugli spazi dei nomi delle identità in Experience Platform, consulta la [documentazione sugli spazi dei nomi delle identità](../../../../identity-service/features/namespaces.md).

Quando configuri gli spazi dei nomi di identità per la destinazione, puoi ottimizzare la mappatura identità di destinazione supportata dalla destinazione, ad esempio:

* Consente agli utenti di mappare gli attributi XDM agli spazi dei nomi delle identità.
* Consente agli utenti di mappare [spazi dei nomi di identità standard](../../../../identity-service/features/namespaces.md#standard) agli spazi dei nomi di identità personalizzati.
* Consente agli utenti di mappare [spazi dei nomi di identità personalizzati](../../../../identity-service/features/namespaces.md#manage-namespaces) agli spazi dei nomi di identità personalizzati.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

È possibile configurare gli spazi dei nomi di identità supportati tramite l&#39;endpoint `/authoring/destinations`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione degli spazi dei nomi delle identità supportate che puoi utilizzare per la tua destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì (obbligatorio) |
| Integrazioni basate su file (batch) | Sì (facoltativo) |

## Parametri supportati {#supported-parameters}

Quando definisci le identità di destinazione supportate dalla destinazione, puoi utilizzare i parametri descritti nella tabella seguente per configurarne il comportamento.

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Facoltativo | Indica se i clienti possono mappare gli attributi di profilo standard all’identità che stai configurando. |
| `acceptsCustomNamespaces` | Booleano | Facoltativo | Indica se i clienti possono mappare gli spazi dei nomi di identità personalizzati allo spazio dei nomi di identità che stai configurando. |
| `acceptedGlobalNamespaces` | - | Facoltativo | Indica quali [spazi dei nomi di identità standard](../../../../identity-service/features/namespaces.md#standard) (ad esempio, [!UICONTROL IDFA]) i clienti possono mappare all&#39;identità che stai configurando. |
| `transformation` | Stringa | Facoltativo | Visualizza la casella di controllo [[!UICONTROL Applica trasformazione]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) nell&#39;interfaccia utente di Platform quando il campo di origine è un attributo XDM o uno spazio dei nomi di identità personalizzato. Utilizza questa opzione per consentire agli utenti di aggiungere hash agli attributi sorgente durante l’esportazione. Per abilitare questa opzione, impostare il valore su `sha256(lower($))`. |
| `requiredTransformation` | Stringa | Facoltativo | Quando i clienti selezionano questo spazio dei nomi dell&#39;identità di origine, la casella di controllo [[!UICONTROL Applica trasformazione]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) viene applicata automaticamente alla mappatura e i clienti non possono disattivarla. Per abilitare questa opzione, impostare il valore su `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

È necessario indicare le identità [!DNL Platform] che i clienti possono esportare nella destinazione. Alcuni esempi sono [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono [!DNL Platform] spazi dei nomi di identità che i clienti possono mappare su spazi dei nomi di identità dalla destinazione.

Gli spazi dei nomi di identità non richiedono una corrispondenza 1-a-1 tra [!DNL Platform] e la destinazione.
Ad esempio, i clienti possono mappare uno spazio dei nomi [!DNL Platform] [!DNL IDFA] a uno spazio dei nomi [!DNL IDFA] dalla tua destinazione, oppure possono mappare lo stesso spazio dei nomi [!DNL Platform] [!DNL IDFA] a uno spazio dei nomi [!DNL Customer ID] nella tua destinazione.

Ulteriori informazioni sulle identità nella [panoramica dello spazio dei nomi delle identità](../../../../identity-service/features/namespaces.md).

## Considerazioni sulla mappatura

Se i clienti selezionano uno spazio dei nomi dell’identità di origine e non una mappatura di destinazione, Platform inserisce automaticamente nella mappatura di destinazione un attributo con lo stesso nome.

## Configurare l’hashing facoltativo del campo sorgente

I clienti di Experience Platform possono scegliere di acquisire i dati in Platform in formato hash o in testo normale. Se la piattaforma di destinazione accetta sia dati con hash che dati senza hash, puoi dare ai clienti la possibilità di scegliere se Platform deve eseguire l’hashing dei valori dei campi sorgente quando vengono esportati nella destinazione.

La configurazione seguente abilita l&#39;opzione opzionale [Applica trasformazione](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) nell&#39;interfaccia utente di Platform, nel passaggio Mappatura.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Seleziona questa opzione quando utilizzi campi di origine senza hash per fare in modo che Adobe Experience Platform ne esegua automaticamente l’hashing all’attivazione.

Quando si esegue il mapping degli attributi di origine senza hash agli attributi di destinazione per i quali la destinazione prevede l&#39;hash (ad esempio: `email_lc_sha256` o `phone_sha256`), selezionare l&#39;opzione **Applica trasformazione** per fare in modo che Adobe Experience Platform esegua automaticamente l&#39;hash degli attributi di origine all&#39;attivazione.

## Configurare l’hashing obbligatorio del campo sorgente

Se la destinazione accetta solo dati con hash, puoi configurare gli attributi esportati in modo che ricevano automaticamente l’hash da Platform. La configurazione seguente controlla automaticamente l&#39;opzione **Applica trasformazione** quando le identità `Email` e `Phone` sono mappate.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti sapere meglio come configurare gli spazi dei nomi delle identità per le destinazioni create con Destination SDK.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione del cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
