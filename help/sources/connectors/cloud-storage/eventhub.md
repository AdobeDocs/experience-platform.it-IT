---
title: Panoramica del connettore di origine degli hub eventi di Azure
description: Scopri come collegare gli hub eventi di Azure a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 7240f96cb30e79add500a1957d93062eecd79ee2
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] sorgente

>[!IMPORTANT]
>
>Il [!DNL Azure Event Hubs] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform], e [!DNL Azure]. Puoi inserire in Platform i dati provenienti da questi sistemi.

Le origini di archiviazione cloud possono inserire i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini. Platform consente di inserire dati da [!DNL Event Hubs] in tempo reale.

## Ridimensionamento con [!DNL Event Hubs]

Il fattore di scala del [!DNL Event Hubs] L’istanza di deve essere aumentata se devi acquisire dati di volume elevato, aumentare il parallelismo o aumentare la velocità della piattaforma di acquisizione.

### Dati di volume superiori in ingresso

Attualmente, il volume massimo di dati che puoi importare dal tuo [!DNL Event Hubs] l’account per Platform è di 2000 record al secondo. Per aumentare e acquisire dati con volumi più elevati, contatta il rappresentante del tuo Adobe.

### Aumenta parallelismo su [!DNL Event Hubs] e Platform

Il parallelismo si riferisce all&#39;esecuzione simultanea delle stesse attività su più unità di elaborazione al fine di aumentare la velocità e le prestazioni. Puoi aumentare il parallelismo sulla [!DNL Event Hubs] aumentando la partizione o acquisendo più unità di elaborazione per il [!DNL Event Hubs] account. Vedi questo [[!DNL Event Hubs] documento in scala](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) per ulteriori informazioni.

Per aumentare la velocità di acquisizione sul lato Platform, Platform deve aumentare il numero di attività nel connettore di origine da leggere dal [!DNL Event Hubs] partizioni. Una volta che hai aumentato il parallelismo sulla [!DNL Event Hubs] contatta il tuo rappresentante di Adobe per ridimensionare le attività di Platform in base alla nuova partizione. Attualmente, questo processo non è automatizzato.

## Utilizzare una rete virtuale a cui connettersi [!DNL Event Hubs] alla piattaforma

È possibile configurare una rete virtuale per la connessione [!DNL Event Hubs] su Platform mentre le misure firewall sono abilitate. Per configurare una rete virtuale, passare a questo [[!DNL Event Hubs] documento set di regole di rete](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) e segui i passaggi elencati di seguito:

* Seleziona **Prova** dal pannello API REST;
* Autentica il tuo [!DNL Azure] utilizzando le credenziali nello stesso browser;
* Seleziona la [!DNL Event Hubs] spazio dei nomi, gruppo di risorse e sottoscrizione che desideri portare in Platform e quindi selezionare **ESEGUI**;
* Nel corpo del codice JSON visualizzato, aggiungi la seguente subnet Platform in `virtualNetworkRules` interno `properties`:


>[!IMPORTANT]
>
>Prima di eseguire l’aggiornamento, devi effettuare un backup del corpo JSON ricevuto `virtualNetworkRules` con la subnet Platform, in quanto contiene le regole di filtro IP esistenti. In caso contrario, le regole verranno eliminate dopo la chiamata.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Per le diverse aree delle subnet Platform, consulta l’elenco seguente:

### VA7: Nord America

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: Europa

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: Australia

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5_network_10_21_116_0_22/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Vedi quanto segue [[!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) per ulteriori informazioni sui set di regole di rete.

## Connetti [!DNL Event Hubs] alla piattaforma

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Event Hubs] in Platform tramite API o l’interfaccia utente:

### Utilizzo delle API

* [Creare una connessione sorgente degli hub eventi utilizzando l’API del servizio Flusso](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Raccogliere dati in streaming utilizzando l’API del servizio Flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia utente

* [Creare una connessione sorgente agli hub eventi nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configurare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
