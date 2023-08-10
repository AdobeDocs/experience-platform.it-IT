---
description: Scopri come configurare le identità di destinazione supportate per le destinazioni create con Destination SDK.
title: Configurazione dello spazio dei nomi dell’identità
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---


# Configurazione dello spazio dei nomi dell’identità

In questo Experience Platform vengono utilizzati gli spazi dei nomi delle identità per descrivere il tipo di identità specifiche. Ad esempio, uno spazio dei nomi delle identità denominato `Email` identifica un valore come `name@email.com` come indirizzo e-mail.

Durante la creazione di una destinazione tramite Destination SDK, oltre a [configurazione di uno schema partner](schema-configuration.md) Affinché gli utenti possano mappare gli attributi e le identità del profilo su, puoi anche definire gli spazi dei nomi delle identità supportati dalla piattaforma di destinazione.

Dopo una tale azione, gli utenti potranno scegliere anche di selezionare le identità di destinazione, oltre agli attributi del profilo di destinazione.

Per ulteriori informazioni sugli spazi dei nomi delle identità in Experienci Platform, consulta [documentazione sugli spazi dei nomi di identità](../../../../identity-service/namespaces.md).

Quando configuri gli spazi dei nomi di identità per la destinazione, puoi ottimizzare la mappatura identità di destinazione supportata dalla destinazione, ad esempio:

* Consente agli utenti di mappare gli attributi XDM agli spazi dei nomi delle identità.
* Consentire agli utenti di mappare [spazi dei nomi di identità standard](../../../../identity-service/namespaces.md#standard) nei tuoi spazi dei nomi di identità.
* Consentire agli utenti di mappare [spazi dei nomi di identità personalizzati](../../../../identity-service/namespaces.md#manage-namespaces) nei tuoi spazi dei nomi di identità.

Per capire dove questo componente si inserisce in un’integrazione creata con Destination SDK, consulta il diagramma riportato di seguito. [opzioni di configurazione](../configuration-options.md) o consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puoi configurare gli spazi dei nomi di identità supportati tramite `/authoring/destinations` endpoint. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione degli spazi dei nomi delle identità supportate che puoi utilizzare per la tua destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

Quando definisci le identità di destinazione supportate dalla destinazione, puoi utilizzare i parametri descritti nella tabella seguente per configurarne il comportamento.

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Facoltativo | Indica se i clienti possono mappare gli attributi di profilo standard all’identità che stai configurando. |
| `acceptsCustomNamespaces` | Booleano | Facoltativo | Indica se i clienti possono mappare gli spazi dei nomi di identità personalizzati allo spazio dei nomi di identità che stai configurando. |
| `acceptedGlobalNamespaces` | - | Facoltativo | Indica quale [spazi dei nomi di identità standard](../../../../identity-service/namespaces.md#standard) (ad esempio, [!UICONTROL IDFA]) i clienti possono eseguire il mapping all&#39;identità che stai configurando. |
| `transformation` | Stringa | Facoltativo | Visualizza la [[!UICONTROL Applica trasformazione]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) nell’interfaccia utente di Platform, quando il campo di origine è un attributo XDM o uno spazio dei nomi di identità personalizzato. Utilizza questa opzione per consentire agli utenti di aggiungere hash agli attributi sorgente durante l’esportazione. Per abilitare questa opzione, imposta il valore su `sha256(lower($))`. |
| `requiredTransformation` | Stringa | Facoltativo | Quando i clienti selezionano questo spazio dei nomi dell’identità di origine, il [[!UICONTROL Applica trasformazione]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) La casella di controllo viene applicata automaticamente alla mappatura e i clienti non possono disattivarla. Per abilitare questa opzione, imposta il valore su `sha256(lower($))`. |

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

Indicare quale [!DNL Platform] identità che i clienti possono esportare nella tua destinazione. Alcuni esempi sono [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono [!DNL Platform] spazi dei nomi di identità che i clienti possono mappare su spazi dei nomi di identità dalla tua destinazione.

Gli spazi dei nomi delle identità non richiedono una corrispondenza da 1 a 1 tra [!DNL Platform] e la tua destinazione.
Ad esempio, i clienti possono mappare una [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL IDFA] dalla destinazione, oppure possono mappare lo stesso [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL Customer ID] dello spazio dei nomi nella destinazione.

Ulteriori informazioni sulle identità in [panoramica dello spazio dei nomi delle identità](../../../../identity-service/namespaces.md).

## Considerazioni sulla mappatura

Se i clienti selezionano uno spazio dei nomi dell’identità di origine e non una mappatura di destinazione, Platform inserisce automaticamente nella mappatura di destinazione un attributo con lo stesso nome.

## Configurare l’hashing facoltativo del campo sorgente

I clienti di Experienci Platform possono scegliere di acquisire i dati in Platform in formato hash o in testo normale. Se la piattaforma di destinazione accetta sia dati con hash che dati senza hash, puoi dare ai clienti la possibilità di scegliere se Platform deve eseguire l’hashing dei valori dei campi sorgente quando vengono esportati nella destinazione.

La configurazione seguente abilita il [Applica trasformazione](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) nell’interfaccia utente di Platform, nel passaggio Mappatura.

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

Quando mappi gli attributi di origine senza hash agli attributi di destinazione per i quali la destinazione prevede l&#39;hashing (ad esempio: `email_lc_sha256` o `phone_sha256`), controlla **Applica trasformazione** opzione per fare in modo che Adobe Experience Platform esegua automaticamente l’hash degli attributi sorgente all’attivazione.

## Configurare l’hashing obbligatorio del campo sorgente

Se la destinazione accetta solo dati con hash, puoi configurare gli attributi esportati in modo che ricevano automaticamente l’hash da Platform. La configurazione seguente controlla automaticamente **Applica trasformazione** opzione quando `Email` e `Phone` le identità sono mappate.

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
* [Autenticazione OAuth2](oauth2-authentication.md)
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
