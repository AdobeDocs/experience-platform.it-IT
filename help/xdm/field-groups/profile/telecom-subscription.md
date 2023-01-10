---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;telecom;abbonamento;telecomunicazioni;schema di schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo di campi schema sottoscrizione Telecom
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema di sottoscrizione di Telecom.
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 8%

---

# [!UICONTROL Abbonamento a domicilio] gruppo di campi schema

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Visualizza il documento in [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) per ulteriori informazioni.

[!UICONTROL Abbonamento a domicilio] è un gruppo di campi di schema standard per [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) che descrive il piano di abbonamento a servizi di telecomunicazione di un cliente, inclusi prezzi, pacchetti e abbonamenti a singoli prodotti.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `telecomSubscription`, le cui proprietà sono descritte di seguito.

![Struttura di abbonamento a telecomunicazioni](../../images/field-groups/telecom-subscription/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `internetSubscription` | Array di oggetti | Descrive i dettagli del piano di sottoscrizione Internet quali il limite dati, il tipo di connessione e i dettagli della velocità. Consulta la sezione [sezione sottostante](#internetSubscription) per ulteriori informazioni. |
| `landlineSubscription` | Array di oggetti | Descrive i dettagli del piano di abbonamento in linea, incluse le funzioni selezionate, i minuti e i piani di composizione. Consulta la sezione [sezione sottostante](#landlineSubscription) per ulteriori informazioni. |
| `mediaSubscription` | Array di oggetti | Descrive i dettagli del piano di abbonamento multimediale, compreso il numero di canali e i servizi di streaming inclusi. Consulta la sezione [sezione sottostante](#mediaSubscription) per ulteriori informazioni. |
| `mobileSubscription` | Array di oggetti | Descrive i dettagli del piano di abbonamento mobile, tra cui il numero di righe, le tariffe dei dati, i costi e altro ancora. Consulta la sezione [sezione sottostante](#mobileSubscription) per ulteriori informazioni. |
| `primarySubscriber` | [[!UICONTROL Persona]](../../data-types/person.md) | Descrive il proprietario della sottoscrizione. |
| `bundleName` | Stringa | Acquisisce il nome di qualsiasi tipo di bundle di abbonamento in cui il cliente è iscritto, come `Internet + Media`. |
| `primaryPartyID` | Stringa | Identificatore della persona principale responsabile dell&#39;abbonamento, che in genere potrebbe essere il numero di telefono del dispositivo. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `connectionType` | Stringa | Tipo di connessione per la sottoscrizione. |
| `dataCap` | Intero | Limite massimo dati per l’account, in megabyte (MB). |
| `downloadSpeed` | Intero | La velocità massima di download disponibile per l’abbonamento, in megabyte (MB). |
| `selfSetup` | Booleano | Indica se un cliente è idoneo per la configurazione di Internet senza la visita di un tecnico. |
| `uploadSpeed` | Intero | La velocità massima di caricamento disponibile per l’abbonamento, in megabyte (MB). |

{style=&quot;table-layout:auto&quot;}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Numero di telefono]](../../data-types/telecom-subscription.md) | Numero di telefono assegnato a questa sottoscrizione. |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `callBlocking` | Booleano | Indica se le funzioni di abbonamento a linee fisse includono il blocco delle chiamate. |
| `callForwarding` | Booleano | Indica se le funzionalità di abbonamento in linea fissa includono l&#39;inoltro delle chiamate. |
| `callWaiting` | Booleano | Indica se le funzionalità di abbonamento in linea fissa includono l&#39;attesa di chiamata. |
| `callerID` | Booleano | Indica se le funzionalità di sottoscrizione offline includono l&#39;ID chiamante. |
| `internationalCalling` | Booleano | Indica se le funzionalità di abbonamento a linee fisse includono la chiamata internazionale. |
| `minutes` | Intero | Il numero di minuti mensili disponibili nell’abbonamento. |
| `threeWayCalling` | Booleano | Indica se le funzioni di abbonamento a linee fisse includono la chiamata a tre vie. |
| `unlimitedDomesticLongDistance` | Booleano | Indica se le caratteristiche di abbonamento a linea fissa includono chiamate a lunga distanza nazionali illimitate. |
| `unlimitedLocalCalling` | Booleano | Indica se le funzionalità di abbonamento a linee fisse includono una chiamata locale illimitata. |
| `voicemail` | Booleano | Indica se le funzionalità di abbonamento in linea fissa includono voicemail. |

{style=&quot;table-layout:auto&quot;}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `streamingServices` | Array di oggetti | Elenco di tutti i servizi di streaming inclusi nell’abbonamento. Ogni elemento array include le seguenti proprietà: <ul><li>`promotionLength`: La durata della promozione, in mesi, se il servizio di streaming è stato aggiunto come parte di una promozione.</li><li>`promotionalAddition`: Indica se il servizio di streaming è stato aggiunto come parte di una promozione.</li><li>`serviceName`: Nome del servizio di streaming.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `channels` | Intero | Il numero di canali inclusi con l’abbonamento a contenuti multimediali. |

{style=&quot;table-layout:auto&quot;}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Numero di telefono]](../../data-types/telecom-subscription.md) | Numero di telefono assegnato a questa sottoscrizione. |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `earlyUpgradeEnrollment` | Booleano | Indica se il cliente effettua il consenso per gli aggiornamenti anticipati. |
| `planLevel` | Stringa | Nome del piano mobile assegnato a questo abbonamento. |
| `portedNumber` | Booleano | Indica se il cliente porta il proprio numero da un altro vettore. |

{style=&quot;table-layout:auto&quot;}
