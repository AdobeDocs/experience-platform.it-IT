---
title: Gruppo di campi schema dettagli Advertising
description: Scopri il gruppo di campi dello schema Dettagli di Advertising.
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 27%

---

# [!UICONTROL Dettagli Advertising] gruppo di campi schema

[!UICONTROL Dettagli Advertising] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo oggetto `advertising` a uno schema, che acquisisce informazioni relative a impression pubblicitarie, clickthrough e attribuzione.

![Struttura del gruppo di campi](../../images/field-groups/advertising-details/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `adAssetReference` | Oggetto | Acquisisce informazioni sulla risorsa relative all’annuncio. Per ulteriori informazioni sulla struttura dell&#39;oggetto, vedere la [sottosezione seguente](#adAssetReference). |
| `adAssetViewDetails` | Oggetto | Acquisisce i dettagli di visualizzazione per la riproduzione dell’annuncio. Per ulteriori informazioni sulla struttura dell&#39;oggetto, vedere la [sottosezione seguente](#adAssetViewDetails). |
| `adViewability` | Oggetto | Acquisisce il numero di impression visualizzate dagli utenti finali, ad esempio il volume del lettore, la versione della libreria, lo stato della finestra e le dimensioni del riquadro di visualizzazione degli annunci. Per ulteriori informazioni sulla struttura dell&#39;oggetto, vedere la [sottosezione seguente](#adViewability). |
| `clicks` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di azioni di clic sull’annuncio. |
| `completes` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui una risorsa multimediale a tempo è stata guardata fino al completamento. Ciò non significa necessariamente che l’utente finale abbia guardato l’intero video, poiché potrebbe aver saltato delle parti per andare avanti. |
| `conversions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui una o più azioni predefinite hanno attivato un evento per la valutazione delle prestazioni. |
| `federated` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica se l’evento esperienza è stato creato tramite la federazione di dati, ad esempio la condivisione di dati tra clienti. |
| `firstQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale è stato riprodotto a velocità normale per il 25% della sua durata. |
| `impressions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di ad impression inviate a un utente finale con il potenziale di visualizzazione. |
| `midpoints` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale è stato riprodotto a velocità normale per il 50% della sua durata. |
| `starts` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale ha iniziato la riproduzione. |
| `thirdQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale è stato riprodotto a velocità normale per il 75% della sua durata. |
| `timePlayed` | [[!UICONTROL Misura]](../../data-types/measure.md) | La quantità di tempo trascorso da un utente finale su una specifica risorsa multimediale a tempo. |
| `downloadedPlayback` | Booleano | Se è impostato su `true`, indica che l&#39;hit viene generato a causa della riproduzione di una sessione di annunci scaricata. |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

L&#39;oggetto `adAssetReference` acquisisce le informazioni sulle risorse relative all&#39;annuncio.

![struttura adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc.title` | Stringa | Nome leggibile e intuitivo di una risorsa per annunci. |
| `_xmpDM.duration` | Intero | Lunghezza o durata della risorsa in secondi. |
| `_id` | Stringa | Identificatore univoco della risorsa dell&#39;annuncio, in base allo standard [ID annuncio](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | Stringa | Azienda o marchio il cui prodotto è presentato nell’annuncio. |
| `campaign` | Stringa | ID della campagna pubblicitaria. |
| `creativeID` | Stringa | L’ID della creatività dell’annuncio. |
| `creativeURL` | Stringa | L’URL della creatività dell’annuncio. |
| `placementID` | Stringa | ID di posizionamento dell’annuncio. |
| `siteID` | Stringa | ID del sito dell’annuncio. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

L&#39;oggetto `adAssetViewDetails` acquisisce i dettagli di visualizzazione per la riproduzione dell&#39;annuncio.

![struttura adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Interruzione pubblicitaria]](../../data-types/ad-break.md) | Descrive come un annuncio a tempo viene inserito in un contenuto multimediale a tempo. |
| `index` | Intero | L’indice dell’annuncio all’interno dell’interruzione pubblicitaria principale. Ad esempio, il primo annuncio ha indice `0` e il secondo annuncio ha indice `1`. |
| `playerName` | Stringa | Il nome del lettore responsabile del rendering dell’annuncio. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

L&#39;oggetto `adViewability` acquisisce il numero di impression visualizzate dagli utenti finali, ad esempio il volume del lettore, la versione della libreria, lo stato della finestra e le dimensioni del riquadro di visualizzazione degli annunci.

![struttura adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Dettagli implementazione]](../../data-types/implementation-details.md) | Il nome e la versione della libreria dotata di strumenti per misurare le metriche di visualizzabilità. |
| `measuredAdNotVisible` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che l’annuncio non è visibile come misurato da una libreria di visualizzabilità al momento dell’impression. |
| `measuredMuted` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che l’annuncio è disattivato come misurato da una libreria di visualizzabilità al momento dell’impression. |
| `unmeasurableIframe` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che l’annuncio viene visualizzato in una finestra inattiva come misurato da una libreria di visualizzabilità al momento dell’impression. |
| `unmeasurableOther` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che la libreria di visualizzabilità non è in grado di eseguire correttamente le misurazioni a causa dell’annuncio visualizzato all’interno di un iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Impression di un annuncio pubblicitario rivolto a un utente finale dotato di libreria di visualizzabilità. |
| `viewabilityCompletes` | [[!UICONTROL Misura]](../../data-types/measure.md) | Completamento/i di un annuncio pubblicitario per un utente finale ritenuto visualizzabile al momento del completamento da una libreria di visualizzabilità. |
| `viewableFirstQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Primo/i quartile/i di un annuncio pubblicitario per un utente finale ritenuto visualizzabile al primo quartile di riproduzione da una libreria di visualizzabilità. |
| `viewableImpressions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Impression di un annuncio pubblicitario per un utente finale ritenuto visualizzabile dopo due secondi di riproduzione da una libreria di visualizzabilità. |
| `viewableMidpoints` | [[!UICONTROL Misura]](../../data-types/measure.md) | Punto/i intermedio/i di un annuncio pubblicitario per un utente finale ritenuto visualizzabile nel punto intermedio di riproduzione da una libreria di visualizzabilità. |
| `viewableThirdQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Terzo/i quartile/i di un annuncio pubblicitario per un utente finale ritenuto visualizzabile al terzo quartile di riproduzione da una libreria di visualizzabilità. |
| `activeWindow` | Booleano | Indica se l’annuncio è stato visualizzato nella finestra attiva del dispositivo dell’utente. |
| `adHeight` | Intero | Il numero di pixel verticali del lettore, misurati in fase di runtime. Può essere maggiore della dimensione dell’annuncio, se il lettore ha controlli o miniature extra. |
| `adUnitDepth` | Intero | Gli editori possono incorporare le unità pubblicitarie all’interno dei contenitori (iFrame) in modo da limitare l’accesso all’annuncio unicamente al codice della pagina. Questo valore descrive quanti contenitori viene visualizzata l’unità pubblicitaria all’interno di. |
| `adWidth` | Intero | Il numero di pixel orizzontali del lettore, misurati in fase di runtime. Può essere maggiore della dimensione dell’annuncio se il lettore ha controlli o miniature extra. |
| `measurementEligible` | Booleano | Indica se l’annuncio era idoneo o meno alla misurazione della visualizzabilità. Un annuncio è idoneo se l’unità dispone di un formato di creatività e un tipo di tag supportati. |
| `percentViewable` | Intero | La percentuale di pixel nell’annuncio ritenuta visualizzabile al momento della misurazione. |
| `playerVolume` | Intero | Percentuale del volume del lettore misurata in fase di runtime, dove `0` è disattivato e `100` è il volume massimo. |
| `viewable` | Booleano | Indica se l’annuncio era visualizzabile in fase di runtime. Gli annunci display sono considerati visualizzabili quando almeno il 50% dell’annuncio è visibile per almeno un secondo. Gli annunci video sono considerati visualizzabili quando almeno il 50% dell’annuncio è visibile durante la riproduzione del video per almeno due secondi consecutivi. |
| `viewportHeight` | Intero | La dimensione verticale (in pixel) della finestra in cui è stata visualizzata l’esperienza misurata in fase di runtime. Per un evento di visualizzazione web, questo valore indica l’altezza del riquadro di visualizzazione del browser. |
| `viewportWidth` | Intero | La dimensione orizzontale (in pixel) della finestra in cui è stata visualizzata l’esperienza misurata in fase di runtime. Per un evento di visualizzazione web, questo valore indica la larghezza del riquadro di visualizzazione del browser. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
