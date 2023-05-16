---
description: Scopri come configurare le identità di destinazione supportate per le destinazioni create con Destination SDK.
title: Configurazione dello spazio dei nomi identità
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---


# Configurazione dello spazio dei nomi identità

Experience Platform utilizza i namespace di identità per descrivere il tipo di identità specifica. Ad esempio, uno spazio dei nomi di identità denominato `Email` identifica un valore come `name@email.com` come indirizzo e-mail.

Durante la creazione di una destinazione tramite Destination SDK, oltre a [configurazione di uno schema partner](schema-configuration.md) che gli utenti possano mappare attributi e identità di profilo, puoi anche definire spazi dei nomi di identità supportati dalla piattaforma di destinazione.

In questo modo, gli utenti possono scegliere di selezionare le identità di destinazione, oltre agli attributi di profilo di destinazione.

Per ulteriori informazioni sugli spazi dei nomi delle identità, consulta l’ [documentazione dei namespace di identità](../../../../identity-service/namespaces.md).

Quando configuri i namespace di identità per la destinazione, puoi perfezionare la mappatura dell’identità di destinazione supportata dalla destinazione, ad esempio:

* Consentire agli utenti di mappare gli attributi XDM sui namespace di identità.
* Consentire agli utenti di eseguire la mappatura [spazi dei nomi delle identità standard](../../../../identity-service/namespaces.md#standard) ai namespace della tua identità.
* Consentire agli utenti di eseguire la mappatura [spazi dei nomi delle identità personalizzati](../../../../identity-service/namespaces.md#manage-namespaces) ai namespace della tua identità.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puoi configurare i namespace di identità supportati tramite `/authoring/destinations` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione dei namespace di identità supportati che puoi utilizzare per la tua destinazione e mostra ciò che i clienti vedranno nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

Quando definisci le identità di destinazione supportate dalla tua destinazione, puoi utilizzare i parametri descritti nella tabella seguente per configurarne il comportamento.

| Parametro | Tipo | Obbligatorio/facoltativo | Descrizione |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Facoltativo | Indica se i clienti possono mappare gli attributi di profilo standard all’identità che stai configurando. |
| `acceptsCustomNamespaces` | Booleano | Facoltativo | Indica se i clienti possono mappare spazi dei nomi di identità personalizzati allo spazio dei nomi di identità configurato. |
| `acceptedGlobalNamespaces` | - | Facoltativo | Indica quale [spazi dei nomi delle identità standard](../../../../identity-service/namespaces.md#standard) (ad esempio, [!UICONTROL IDFA]) i clienti possono eseguire la mappatura dell’identità che stai configurando. |
| `transformation` | Stringa | Facoltativo | Visualizza la [[!UICONTROL Applica trasformazione]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) nell’interfaccia utente di Platform, quando il campo di origine è un attributo XDM o uno spazio dei nomi di identità personalizzato. Utilizza questa opzione per consentire agli utenti di aggiungere attributi di origine hash all’esportazione. Per abilitare questa opzione, imposta il valore su `sha256(lower($))`. |
| `requiredTransformation` | Stringa | Facoltativo | Quando i clienti selezionano questo spazio dei nomi dell&#39;identità di origine, la [[!UICONTROL Applica trasformazione]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) la casella di controllo viene applicata automaticamente alla mappatura e i clienti non possono disattivarla. Per abilitare questa opzione, imposta il valore su `sha256(lower($))`. |

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

Indica quale [!DNL Platform] i clienti di identità possono esportare nella tua destinazione. Alcuni esempi [!DNL Experience Cloud ID], e-mail con hash, ID dispositivo ([!DNL IDFA], [!DNL GAID]). Questi valori sono [!DNL Platform] spazi dei nomi delle identità che i clienti possono mappare a spazi dei nomi delle identità dalla destinazione.

Gli spazi dei nomi di identità non richiedono una corrispondenza 1-to-1 tra [!DNL Platform] e la destinazione.
Ad esempio, i clienti possono mappare un [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL IDFA] spazio dei nomi dalla destinazione, oppure possono mappare lo stesso [!DNL Platform] [!DNL IDFA] spazio dei nomi in un [!DNL Customer ID] spazio dei nomi nella destinazione.

Ulteriori informazioni sulle identità in [panoramica dello spazio dei nomi identità](../../../../identity-service/namespaces.md).

## Considerazioni sulla mappatura

Se i clienti selezionano uno spazio dei nomi dell’identità sorgente e non selezionano una mappatura di destinazione, Platform compila automaticamente la mappatura di destinazione con un attributo con lo stesso nome.

## Configurare l’hashing del campo di origine facoltativo

Ad Experience Platform, i clienti possono scegliere di acquisire dati in Platform in formato con hash o in testo normale. Se la piattaforma di destinazione accetta sia dati con hash che dati con hash, puoi offrire ai clienti la possibilità di scegliere se eseguire l’hash dei valori dei campi di origine quando vengono esportati nella destinazione.

La configurazione seguente abilita il [Applica trasformazione](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) nell’interfaccia utente di Platform, nel passaggio Mappatura .

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

Quando mappi attributi di origine con hash non crittografati su attributi di destinazione per cui si prevede di eseguire l’hashing della destinazione (ad esempio: `email_lc_sha256` o `phone_sha256`), controlla il **Applica trasformazione** per fare in modo che Adobe Experience Platform esegua automaticamente l’hash degli attributi di origine all’attivazione.

## Configurare l’hashing del campo di origine obbligatorio

Se la destinazione accetta solo dati con hash, puoi configurare gli attributi esportati in modo che vengano impostati automaticamente con hash da Platform. La configurazione seguente controlla automaticamente il **Applica trasformazione** quando `Email` e `Phone` le identità sono mappate.

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

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di come configurare i namespace di identità per le destinazioni create con Destination SDK.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione dei clienti](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)
