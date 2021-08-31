---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;visualizzazione e video
title: Connessione Google Display e Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento utilizzato per eseguire il retargeting e le campagne digitali mirate al pubblico tra le origini di inventario Display, Video e Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] connection

## Panoramica {#overview}

[!DNL Display & Video 360], precedentemente noto come  [!DNL DoubleClick Bid Manager], è uno strumento utilizzato per eseguire campagne di retargeting e campagne digitali mirate per il pubblico tra le sorgenti di inventario Display, Video e Mobile.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici delle destinazioni [!DNL Google Display & Video 360]:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Display &amp; Video 360 e non hai abilitato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud in passato (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l&#39;Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza hai configurato le integrazioni Google in Audience Manager, le sincronizzazioni ID che avevi configurato per il passaggio a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come  [!DNL Device ID]. Un ID dispositivo numerico a 38 cifre associato a ciascun dispositivo con cui interagisce. | Google utilizza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e l&#39;ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| MAID | ID pubblicità Microsoft. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| Amazon Fire TV ID | Questo ID identifica in modo univoco i Amazon Fire TV. |  |

## Tipo di esportazione {#export-type}

**Esportazione segmento** : stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google.

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti

>[!NOTE]
>
>L’inserimento nell’elenco Consentiti è obbligatorio prima di configurare la prima destinazione [!DNL Google Display & Video 360] in Platform. Prima di creare una destinazione, assicurati che Google abbia completato il processo di inserimento nell’elenco Consentiti descritto di seguito.

Prima di creare la destinazione [!DNL Google Display & Video 360] in Platform, è necessario contattare Google chiedendo di inserire l’Adobe nell’elenco dei provider di dati consentiti e di aggiungere l’account all’elenco consentiti. Contatta Google e fornisci le seguenti informazioni:

* **ID** account: ID account di Adobe con Google. ID account: 87933855.
* **ID** cliente: ID account cliente di Adobe con Google. ID cliente: 89690775.
* **Tipo** di account: utilizza  **[!DNL Invite advertiser]** per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel tuo account Display &amp; Video 360 o  **[!DNL Invite partner]** per consentire al pubblico di essere condiviso con tutti i marchi del tuo account Display &amp; Video 360.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Tipo]** account: Seleziona un’opzione, a seconda del tuo account con Google:
   * Utilizza `Invite Advertiser` per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel tuo account Display &amp; Video 360 .
   * Utilizza `Invite Partner` per consentire ai tipi di pubblico di essere condivisi con tutti i marchi del tuo account Display &amp; Video 360.
* **[!UICONTROL ID]** account: Compila il tuo ID  **[!DNL Invite partner]** o  **[!DNL Invite advertiser]** account con Google. In genere si tratta di un ID a sei o sette cifre.

>[!NOTE]
>
>Quando imposti una destinazione [!DNL Google Display & Video 360], collabora con il tuo [!DNL Google Account Manager] o rappresentante di Adobe per capire quale tipo di account hai.

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Display & Video 360], controlla il tuo account [!DNL Google Display & Video 360]. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potresti ricevere il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi ai [prerequisiti](#prerequisites). Per risolvere questo problema, contatta Google e assicurati che il tuo account sia inserito nell’elenco Consentiti.