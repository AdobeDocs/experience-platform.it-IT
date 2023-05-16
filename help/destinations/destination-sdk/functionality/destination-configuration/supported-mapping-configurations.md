---
description: Scopri come configurare la destinazione per le configurazioni di mappatura identità e attributi supportate.
title: Configurazioni di mappatura supportate
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Configurazioni di mappatura supportate

Le destinazioni create con Destination SDK supportano configurazioni specifiche per lo spazio dei nomi delle identità e la mappatura degli attributi, in base al tipo di destinazione.

Questo articolo descrive tutte le configurazioni di mappatura supportate che puoi utilizzare per configurare la destinazione.

>[!WARNING]
>
>Qualsiasi configurazione di mappatura non descritta in questo articolo non è supportata da Destination SDK.

Quando crei la destinazione, configura lo schema e i namespace di identità in base a una delle configurazioni di mappatura descritte in questa pagina.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Mappature supportate per le destinazioni di streaming {#streaming-mappings}

Le destinazioni in tempo reale (streaming) create con Destination SDK supportano le configurazioni di mappatura descritte nella tabella seguente.

| Campo di origine | Campo di destinazione |
| --- | --- |
| Attributo XDM | Attributo personalizzato |
| Spazio dei nomi identità | Spazio dei nomi identità |

L’esempio di configurazione seguente consente ai clienti di utilizzare entrambe le mappature nella tabella precedente.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
            
         },
         "Phone":{
            
         }
      }
   }
},
```

### Mappatura di attributi XDM su attributi personalizzati {#streaming-xdm-to-custom}

Gli utenti possono mappare gli attributi dal profilo XDM di origine agli attributi personalizzati sul lato della destinazione.

Gli utenti devono immettere manualmente il nome dell’attributo personalizzato di destinazione quando selezionano la mappatura del campo di destinazione.

![Schermata dell’interfaccia utente della piattaforma che mostra la selezione di attributi personalizzati.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

L’esperienza di interfaccia utente risultante viene mostrata nell’immagine seguente.

![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura degli attributi XDM su attributi personalizzati per le destinazioni di streaming.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Mappare i namespace di identità negli spazi dei nomi dei partner {#streaming-identity-to-identity}

Gli utenti possono mappare i namespace di identità personalizzati o globali da Platform a quelli definiti dall’utente.

L’esperienza di interfaccia utente risultante viene mostrata nell’immagine seguente.

![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura dell’identità sull’identità per le destinazioni di streaming.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Mappature supportate per destinazioni basate su file {#batch-mappings}

Le destinazioni basate su file create con Destination SDK supportano le configurazioni di mappatura descritte nella tabella seguente. Consulta le sezioni successive per esempi di mappatura dettagliati.

| Campo di origine | Campo di destinazione |
| --- | --- |
| Attributo XDM | Attributo / Attributo personalizzato |
| Spazio dei nomi identità | Attributo / Attributo personalizzato |
| Spazio dei nomi identità | Spazio dei nomi identità |

L’esempio di configurazione seguente consente ai clienti di utilizzare tutte le mappature della tabella precedente.

```json
"schemaConfig":{
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
},
"identityNamespaces":{
   "Customer_contact":{
      "acceptsAttributes":false,
      "acceptsCustomNamespaces":true,
      "acceptedGlobalNamespaces":{
         "Email":{
         },
         "Phone":{
         }
      }
   }
},
```

### Mappatura di attributi XDM su attributi personalizzati {#batch-xdm-to-custom}

Gli utenti possono mappare gli attributi dal profilo XDM di origine agli attributi personalizzati sul lato della destinazione.

Per le destinazioni basate su file, il campo di destinazione viene compilato automaticamente con un attributo predefinito con lo stesso nome del campo di origine.

L’esperienza di interfaccia utente risultante viene mostrata nell’immagine seguente.

![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura XDM su attributi personalizzati per destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Gli utenti possono lasciare attivo il nome predefinito oppure immettere un nome di attributo personalizzato nella schermata di selezione del campo di destinazione.

![Schermata dell’interfaccia utente di Platform che mostra la selezione di attributi di destinazione personalizzati per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Mappatura di spazi dei nomi di identità su attributi personalizzati {#batch-identity-to-custom}

Gli utenti possono mappare i namespace di identità personalizzati o globali da Platform agli attributi personalizzati sul lato della destinazione.

Quando si seleziona uno spazio dei nomi di identità come campo di origine, il campo di destinazione viene compilato automaticamente con uno spazio dei nomi di identità equivalente. Per sostituire il campo di destinazione con un attributo personalizzato, gli utenti devono immettere un nome di attributo personalizzato nella schermata di selezione del campo di destinazione.

![Schermata dell’interfaccia utente di Platform che mostra la selezione di attributi di destinazione personalizzati per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

L’esperienza di interfaccia utente risultante viene mostrata nell’immagine seguente.

![Schermata dell’interfaccia utente di Platform che mostra la mappatura delle identità agli attributi personalizzati per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Mappare i namespace di identità negli spazi dei nomi dei partner {#batch-identity-to-identity}

Gli utenti possono mappare spazi dei nomi di identità personalizzati o globali da Platform a spazi dei nomi di identità equivalenti.

Quando si seleziona uno spazio dei nomi di identità come campo di origine, il campo di destinazione viene compilato automaticamente con uno spazio dei nomi di identità equivalente.

L’esperienza di interfaccia utente risultante viene mostrata nell’immagine seguente.

![Schermata dell’interfaccia utente della piattaforma che mostra la mappatura dell’identità per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di quali mappature sono supportate dalle destinazioni create con Destination SDK.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione dei clienti](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)