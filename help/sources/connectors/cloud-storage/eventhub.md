---
keywords: Experience Platform;home;argomenti popolari;hub eventi di Azure;hub eventi di Azure;hub eventi di Azure;hub eventi;hub eventi;hub eventi
solution: Experience Platform
title: Panoramica del connettore di origine per gli hub eventi di Azure
topic-legacy: overview
description: Scopri come collegare gli hub eventi di Azure a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: b64054859cbd88687dd05b0c65e51d0b2ef2a7b3
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] connettore

Adobe Experience Platform fornisce connettività nativa per fornitori di cloud come AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. Puoi importare i dati da questi sistemi in Platform.

Le origini di archiviazione cloud possono importare i tuoi dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . Platform consente di importare i dati da [!DNL Event Hubs] in tempo reale.

## Ridimensionamento con [!DNL Event Hubs]

Il fattore di scala del tuo [!DNL Event Hubs] L’istanza deve essere aumentata se è necessario inserire dati con volume elevato, aumentare il parallelismo o aumentare la velocità della piattaforma di acquisizione.

### Ingresso di dati di volume più elevati

Attualmente, il volume massimo di dati che puoi ottenere dal tuo [!DNL Event Hubs] L’account a Platform è di 2000 record al secondo. Per ingrandire e acquisire dati di volume più elevati, contattare il rappresentante di Adobe.

### Aumenta il parallelismo su [!DNL Event Hubs] e piattaforma

Parallelismo si riferisce all&#39;esecuzione simultanea degli stessi compiti su più unità di elaborazione al fine di aumentare la velocità e le prestazioni. È possibile aumentare il parallelismo sul [!DNL Event Hubs] affiancare aumentando la partizione o acquisendo più unità di elaborazione per il tuo [!DNL Event Hubs] conto. Vedi questo [[!DNL Event Hubs] documento su scala](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) per ulteriori informazioni.

Per aumentare la velocità di acquisizione sul lato Platform, Platform deve aumentare il numero di attività nel connettore sorgente da leggere dal [!DNL Event Hubs] partizioni. Una volta aumentato il parallelismo sul [!DNL Event Hubs] contatta il tuo rappresentante Adobe per ridimensionare le attività di Platform in base alla nuova partizione. Attualmente, questo processo non è automatizzato.

## Utilizzare una rete virtuale a cui connettersi [!DNL Event Hubs] su Platform

È possibile impostare una rete virtuale per la connessione [!DNL Event Hubs] su Platform durante l’abilitazione delle misure del firewall. Per impostare una rete virtuale, eseguire l&#39;operazione [[!DNL Event Hubs] documento set di regole di rete](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) e segui i passaggi elencati di seguito:

* Seleziona **Prova** dal pannello REST API;
* Autentica il tuo [!DNL Azure] account che utilizza le credenziali nello stesso browser;
* Seleziona la [!DNL Event Hubs] namespace, gruppo di risorse e sottoscrizione che desideri portare a Platform, quindi seleziona **ESECUZIONE**;
* Nel corpo JSON visualizzato, aggiungi la seguente subnet Platform in `virtualNetworkRules` interno `properties`:


>[!IMPORTANT]
>
>È necessario eseguire un backup del corpo JSON ricevuto prima di aggiornare `virtualNetworkRules` con la subnet Platform in quanto contiene le regole di filtro IP esistenti. In caso contrario, le regole verranno eliminate dopo la chiamata .


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Consulta l’elenco seguente per diverse aree di subnet della piattaforma:

### VA7: America del Nord

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
          "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2_network_10_20_40_0_23/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
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

## Connetti [!DNL Event Hubs] su Platform

La documentazione seguente fornisce informazioni su come connettersi [!DNL Event Hubs] su Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

* [Creare una connessione sorgente Event Hubs utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Raccogliere dati in streaming utilizzando l’API del servizio di flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia

* [Creare una connessione sorgente Event Hubs nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Configurare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
