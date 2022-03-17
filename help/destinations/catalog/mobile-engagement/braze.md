---
keywords: mobile; branco; messaggistica;
title: Collegamento del freno
description: Braze è una piattaforma completa di coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---

# [!DNL Braze] connection

## Panoramica {#overview}

La [!DNL Braze] La destinazione consente di inviare i dati del profilo a [!DNL Braze].

[!DNL Braze] è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze rilevanti e memorabili tra i clienti e i marchi che amano.

Per inviare i dati del profilo a [!DNL Braze], è innanzitutto necessario connettersi alla destinazione.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici della [!DNL Braze] destinazione:

* [!DNL Adobe Experience Platform] i segmenti vengono esportati in [!DNL Braze] in `AdobeExperiencePlatformSegments` attributo.

>[!NOTE]
>
>Tieni presente che l’invio di attributi personalizzati aggiuntivi a [!DNL Braze] può causare aumenti [!DNL Braze] consumo dei punti dati. Consulta la [!DNL Braze] account manager prima di inviare attributi personalizzati aggiuntivi.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio indirizzare gli utenti verso una destinazione di coinvolgimento mobile, con i segmenti incorporati [!DNL Adobe Experience Platform]. Inoltre, voglio offrire loro esperienze personalizzate, basate sugli attributi dei rispettivi [!DNL Adobe Experience Platform] non appena i segmenti e i profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Identità supportate {#supported-identities}

[!DNL Braze] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| external_id | Personalizzato [!DNL Braze] identificatore che supporta la mappatura di qualsiasi identità. | Puoi inviare qualsiasi [identità](../../../identity-service/namespaces.md) al [!DNL Braze] a condizione che sia mappata sulla destinazione [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura del campo.[!DNL Adobe Experience Platform] i segmenti vengono esportati in [!DNL Braze] in `AdobeExperiencePlatformSegments` attributo. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Token account di frenatura]**: Questo è il tuo [!DNL Braze] [!DNL API] chiave. Puoi trovare istruzioni dettagliate su come ottenere il tuo [!DNL API] qui: [Panoramica della chiave API REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nome]**: immetti un nome in base al quale riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: inserisci una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Istanza endpoint]**: chiedi [!DNL Braze] rappresenta l&#39;istanza dell&#39;endpoint da utilizzare.

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Considerazioni sulla mappatura {#mapping-considerations}

Per inviare correttamente i dati sul pubblico da [!DNL Adobe Experience Platform] al [!DNL Braze] destinazione, devi passare attraverso il passaggio di mappatura dei campi .

La mappatura consiste nella creazione di un collegamento tra [!DNL Experience Data Model] Campi dello schema (XDM) nel [!DNL Platform] e loro equivalenti corrispondenti dalla destinazione target.

Per mappare correttamente i campi XDM su [!DNL Braze] campi di destinazione, segui questi passaggi:

In [!UICONTROL Mappatura] passo, fai clic su **[!UICONTROL Aggiungi nuova mappatura]**.

![Mappatura aggiunta destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping.png)

In [!UICONTROL Campo di origine] fare clic sul pulsante freccia accanto al campo vuoto.

![Mappatura della sorgente del freno](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

In [!UICONTROL Selezionare il campo di origine] È possibile scegliere tra due categorie di campi XDM:
* [!UICONTROL Seleziona attributi]: utilizza questa opzione per mappare un campo specifico dallo schema XDM a un [!DNL Braze] attributo.

![Attributo origine mappatura destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Seleziona spazio dei nomi identità]: Utilizza questa opzione per mappare un [!DNL Platform] spazio dei nomi identità in un [!DNL Braze] spazio dei nomi.

![Spazio dei nomi dell&#39;origine della mappatura della destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Scegli il campo di origine, quindi fai clic su **[!UICONTROL Seleziona]**.

In [!UICONTROL Campo di destinazione] fai clic sull’icona di mappatura a destra del campo .

![Mappatura del target di destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

In [!UICONTROL Selezionare il campo di destinazione] è possibile scegliere tra due categorie di campi target:
* [!UICONTROL Seleziona spazio dei nomi identità]: Usa questa opzione per eseguire la mappatura [!DNL Platform] spazi dei nomi delle identità in [!DNL Braze] spazi dei nomi delle identità.
* [!UICONTROL Seleziona attributi personalizzati]: Usa questa opzione per mappare gli attributi XDM su personalizzati [!DNL Braze] attributi definiti nella [!DNL Braze] conto. <br> Puoi inoltre utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Braze]. Ad esempio, la mappatura di un `lastName` Attributo XDM a personalizzato `Last_Name` attributo in [!DNL Braze], crea `Last_Name` attributo in [!DNL Braze], se non esiste già, e mappa il `lastName` Attributo XDM.

![Campi di mappatura destinazione di branding](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Scegli il campo di destinazione, quindi fai clic su **[!UICONTROL Seleziona]**.

Ora dovresti vedere la mappatura dei campi nell’elenco.

![Mappatura destinazione del freno completata](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Per aggiungere altre mappature, ripeti i passaggi precedenti.

## Esempio di mappatura {#mapping-example}

Supponiamo lo schema del profilo XDM e il [!DNL Braze] L&#39;istanza contiene i seguenti attributi ed identità:

|  | Schema del profilo XDM | [!DNL Braze] Istanza |
|---|---|---|
| Attributi | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>Nome</code></li><li>LastName</code></li><li>NumeroTelefono</code></li></ul> |
| Identità | <ul><li>E-mail</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID per gli inserzionisti (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

La mappatura corretta sarà simile alla seguente:

![Esempio di mappatura della destinazione del freno](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL Braze] destinazione, controlla il tuo [!DNL Braze] conto. [!DNL Adobe Experience Platform] i segmenti vengono esportati in [!DNL Braze] in `AdobeExperiencePlatformSegments` attributo.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
