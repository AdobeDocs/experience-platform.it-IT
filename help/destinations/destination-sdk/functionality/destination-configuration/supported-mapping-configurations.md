---
description: Scopri come configurare la destinazione per le configurazioni di mappatura identità e attributi supportate.
title: Configurazioni di mappatura supportate
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Configurazioni di mappatura supportate

Le destinazioni create con Destination SDK supportano specifiche configurazioni di mapping di attributi e spazi dei nomi di identità, in base al tipo di destinazione.

Questo articolo descrive tutte le configurazioni di mappatura supportate che è possibile utilizzare durante la configurazione della destinazione.

>[!WARNING]
>
>Qualsiasi configurazione di mappatura non descritta in questo articolo non è supportata da Destination SDK.

Durante la creazione della destinazione, configura lo schema e gli spazi dei nomi delle identità in base a una delle configurazioni di mappatura descritte in questa pagina.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione maiuscole/minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Mappature supportate per le destinazioni di streaming {#streaming-mappings}

Le destinazioni in tempo reale (streaming) create con Destination SDK supportano le configurazioni di mappatura descritte nella tabella seguente.

| Campo di origine | Campo di destinazione |
| --- | --- |
| attributo XDM | Attributo personalizzato |
| Spazio dei nomi dell’identità | Spazio dei nomi dell’identità |

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

### Mappare gli attributi XDM agli attributi personalizzati {#streaming-xdm-to-custom}

Gli utenti possono mappare gli attributi dal loro profilo XDM di origine agli attributi personalizzati sul lato della destinazione.

Gli utenti devono immettere manualmente il nome dell’attributo personalizzato di destinazione quando selezionano la mappatura del campo di destinazione.

![Schermata dell’interfaccia utente di Platform che mostra la selezione di attributi personalizzati.](../../assets/functionality/destination-configuration/mapping-streaming-select-custom-attribute.png)

L’esperienza dell’interfaccia utente risultante è illustrata nell’immagine seguente.

![Schermata dell’interfaccia utente di Platform che mostra la mappatura degli attributi XDM su attributi personalizzati per le destinazioni di streaming.](../../assets/functionality/destination-configuration/mapping-streaming-xdm-custom.png)

### Mappare gli spazi dei nomi delle identità agli spazi dei nomi delle identità partner {#streaming-identity-to-identity}

Gli utenti possono mappare spazi dei nomi di identità personalizzati o globali da Platform agli spazi dei nomi di identità definiti.

L’esperienza dell’interfaccia utente risultante è illustrata nell’immagine seguente.

![Schermata dell’interfaccia utente di Platform che mostra la mappatura identità per le destinazioni di streaming.](../../assets/functionality/destination-configuration/mapping-streaming-identity-identity.png)

## Mappature supportate per destinazioni basate su file {#batch-mappings}

Le destinazioni basate su file create con Destination SDK supportano le configurazioni di mappatura descritte nella tabella seguente. Per esempi di mappatura dettagliati, consulta le sezioni successive.

| Campo di origine | Campo di destinazione |
| --- | --- |
| attributo XDM | Attributo/Attributo personalizzato |
| Spazio dei nomi dell’identità | Attributo/Attributo personalizzato |
| Spazio dei nomi dell’identità | Spazio dei nomi dell’identità |

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

### Mappare gli attributi XDM agli attributi personalizzati {#batch-xdm-to-custom}

Gli utenti possono mappare gli attributi dal loro profilo XDM di origine agli attributi personalizzati sul lato della destinazione.

Per le destinazioni basate su file, il campo di destinazione viene compilato automaticamente con un attributo predefinito con lo stesso nome del campo di origine.

L’esperienza dell’interfaccia utente risultante è illustrata nell’immagine seguente.

![Schermata dell’interfaccia utente di Platform che mostra la mappatura XDM su attributi personalizzati per destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-xdm-custom.png)

Gli utenti possono lasciare invariato il nome predefinito o immettere un nome di attributo personalizzato nella schermata di selezione del campo di destinazione.

![Schermata dell’interfaccia utente di Platform che mostra la selezione degli attributi di destinazione personalizzati per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

### Mappare gli spazi dei nomi delle identità agli attributi personalizzati {#batch-identity-to-custom}

Gli utenti possono mappare spazi dei nomi di identità personalizzati o globali da Platform agli attributi personalizzati sul lato della destinazione.

Quando selezioni uno spazio dei nomi di identità come campo di origine, il campo di destinazione viene compilato automaticamente con uno spazio dei nomi di identità equivalente. Per sostituire il campo di destinazione con un attributo personalizzato, gli utenti devono immettere un nome di attributo personalizzato nella schermata di selezione del campo di destinazione.

![Schermata dell’interfaccia utente di Platform che mostra la selezione degli attributi di destinazione personalizzati per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-custom-attribute.png)

L’esperienza dell’interfaccia utente risultante è illustrata nell’immagine seguente.

![Schermata dell’interfaccia utente di Platform che mostra il mapping delle identità agli attributi personalizzati per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-identity-custom.png)

### Mappare gli spazi dei nomi delle identità agli spazi dei nomi delle identità partner {#batch-identity-to-identity}

Gli utenti possono mappare spazi dei nomi di identità personalizzati o globali da Platform a spazi dei nomi di identità equivalenti.

Quando selezioni uno spazio dei nomi di identità come campo di origine, il campo di destinazione viene compilato automaticamente con uno spazio dei nomi di identità equivalente.

L’esperienza dell’interfaccia utente risultante è illustrata nell’immagine seguente.

![Schermata dell’interfaccia utente di Platform che mostra il mapping delle identità per le destinazioni basate su file.](../../assets/functionality/destination-configuration/mapping-batch-identity-identity.png)


## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti comprendere meglio quali mappature sono supportate dalle destinazioni create con Destination SDK.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Autenticazione del cliente](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Configurazione batch](batch-configuration.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)