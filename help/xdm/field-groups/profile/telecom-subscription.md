---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;profilo individuale;campi;schemi;schemi;telecom;abbonamento;telecomunicazioni;schema di schema;gruppo di campi;gruppo di campi;
solution: Experience Platform
title: Gruppo di campi schema sottoscrizione Telecom
topic-legacy: overview
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema di sottoscrizione di Telecom.
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 5%

---

# [!UICONTROL Gruppo di campi ] Sottoscrizione Telecom

>[!NOTE]
>
>Sono stati modificati i nomi di diversi gruppi di campi dello schema. Per ulteriori informazioni, consulta il documento sugli [aggiornamenti dei nomi dei gruppi di campi](../name-updates.md) .

[!UICONTROL Telecom ] Subscriptionè un gruppo di campi di schema standard per la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe che descrive il piano di abbonamento a un cliente per le telecomunicazioni, tra cui prezzi, pacchetti e abbonamenti a singoli prodotti.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `telecomSubscription`, le cui proprietà sono descritte di seguito.

![Struttura di abbonamento a telecomunicazioni](../../images/field-groups/telecom-subscription/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `internetSubscription` | Array di oggetti | Descrive i dettagli del piano di sottoscrizione Internet quali il limite dati, il tipo di connessione e i dettagli della velocità. Per ulteriori informazioni, consulta la sezione [sotto](#internetSubscription) . |
| `landlineSubscription` | Array di oggetti | Descrive i dettagli del piano di abbonamento in linea, incluse le funzioni selezionate, i minuti e i piani di composizione. Per ulteriori informazioni, consulta la sezione [sotto](#landlineSubscription) . |
| `mediaSubscription` | Array di oggetti | Descrive i dettagli del piano di abbonamento multimediale, compreso il numero di canali e i servizi di streaming inclusi. Per ulteriori informazioni, consulta la sezione [sotto](#mediaSubscription) . |
| `mobileSubscription` | Array di oggetti | Descrive i dettagli del piano di abbonamento mobile, tra cui il numero di righe, le tariffe dei dati, i costi e altro ancora. Per ulteriori informazioni, consulta la sezione [sotto](#mobileSubscription) . |
| `primarySubscriber` | [[!UICONTROL Persona]](../../data-types/person.md) | Descrive il proprietario della sottoscrizione. |
| `bundleName` | Stringa | Acquisisce il nome di qualsiasi tipo di bundle di abbonamento in cui il cliente è iscritto, ad esempio `Internet + Media`. |
| `primaryPartyID` | Stringa | Identificatore della persona principale responsabile dell&#39;abbonamento, che in genere potrebbe essere il numero di telefono del dispositivo. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` viene fornito un array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `connectionType` | Stringa | Tipo di connessione per la sottoscrizione. |
| `dataCap` | Intero | Limite massimo dati per l’account, in megabyte (MB). |
| `downloadSpeed` | Intero | Velocità massima di download disponibile per l’abbonamento, in megabyte (MB). |
| `selfSetup` | Booleano | Indica se un cliente è idoneo per la configurazione di Internet senza la visita di un tecnico. |
| `uploadSpeed` | Intero | La velocità massima di caricamento disponibile per l’abbonamento, in megabyte (MB). |

{style=&quot;table-layout:auto&quot;}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` viene fornito un array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Numero di telefono]](../../data-types/telecom-subscription.md) | Numero di telefono assegnato a questa sottoscrizione. |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `callBlocking` | Booleano | Indica se le funzioni di abbonamento a linee fisse includono il blocco delle chiamate. |
| `callForwarding` | Booleano | Indica se le funzionalità di abbonamento in linea fissa includono l&#39;inoltro delle chiamate. |
| `callWaiting` | Booleano | Indica se le funzionalità di abbonamento in linea fissa includono l&#39;attesa di chiamata. |
| `callerID` | Booleano | Indica se le funzionalità di sottoscrizione offline includono l&#39;id chiamante. |
| `internationalCalling` | Booleano | Indica se le funzionalità di abbonamento a linee fisse includono la chiamata internazionale. |
| `minutes` | Intero | Il numero di minuti mensili disponibili nell’abbonamento. |
| `threeWayCalling` | Booleano | Indica se le funzioni di abbonamento a linee fisse includono la chiamata a tre vie. |
| `unlimitedDomesticLongDistance` | Booleano | Indica se le caratteristiche di abbonamento a linea fissa includono chiamate a lunga distanza nazionali illimitate. |
| `unlimitedLocalCalling` | Booleano | Indica se le funzionalità di abbonamento a linee fisse includono una chiamata locale illimitata. |
| `voicemail` | Booleano | Indica se le funzionalità di abbonamento in linea fissa includono voicemail. |

{style=&quot;table-layout:auto&quot;}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` viene fornito un array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `streamingServices` | Array di oggetti | Elenco di tutti i servizi di streaming inclusi nell’abbonamento. Ogni elemento array include le seguenti proprietà: <ul><li>`promotionLength`: La durata della promozione, in mesi, se il servizio di streaming è stato aggiunto come parte di una promozione.</li><li>`promotionalAddition`: Indica se il servizio di streaming è stato aggiunto come parte di una promozione.</li><li>`serviceName`: Nome del servizio di streaming.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `channels` | Intero | Il numero di canali inclusi con l’abbonamento a contenuti multimediali. |

{style=&quot;table-layout:auto&quot;}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` viene fornito un array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Numero di telefono]](../../data-types/telecom-subscription.md) | Numero di telefono assegnato a questa sottoscrizione. |
| `subscriptionDetails` | [[!UICONTROL Abbonamento a domicilio]](../../data-types/telecom-subscription.md) | Descrive i dettagli generali dell’abbonamento, inclusi la lunghezza dell’abbonamento, le tariffe, lo stato e altro ancora. |
| `earlyUpgradeEnrollment` | Booleano | Indica se il cliente effettua il consenso per gli aggiornamenti anticipati. |
| `planLevel` | Stringa | Nome del piano mobile assegnato a questo abbonamento. |
| `portedNumber` | Booleano | Indica se il cliente porta il proprio numero da un altro vettore. |

{style=&quot;table-layout:auto&quot;}

