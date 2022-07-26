---
title: Gruppo di campi schema dettagli pubblicità
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli annuncio .
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 10%

---

# [!UICONTROL Dettagli sulla pubblicità] gruppo di campi schema

[!UICONTROL Dettagli sulla pubblicità] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] Classe](../../classes/experienceevent.md). Il gruppo di campi fornisce un singolo `advertising` a uno schema che acquisisce informazioni relative a impression pubblicitarie, clic e attribuzione.

![Struttura del gruppo di campi](../../images/field-groups/advertising-details/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `adAssetReference` | Oggetto | Acquisisce informazioni sulle risorse relative all’annuncio. Consulta la sezione [sottosezione](#adAssetReference) per ulteriori informazioni sulla struttura dell&#39;oggetto. |
| `adAssetViewDetails` | Oggetto | Acquisisce i dettagli di visualizzazione per la riproduzione dell’annuncio. Consulta la sezione [sottosezione](#adAssetViewDetails) per ulteriori informazioni sulla struttura dell&#39;oggetto. |
| `adViewability` | Oggetto | Acquisisce il numero di impression visualizzate dagli utenti finali, ad esempio il volume del lettore, la versione della libreria, lo stato della finestra e le dimensioni del riquadro di visualizzazione degli annunci. Consulta la sezione [sottosezione](#adViewability) per ulteriori informazioni sulla struttura dell&#39;oggetto. |
| `clicks` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di azioni clic sull&#39;annuncio. |
| `completes` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui è stata controllata al completamento una risorsa multimediale temporizzata. Questo non significa necessariamente che l&#39;utente finale abbia guardato l&#39;intero video, in quanto potrebbe aver saltato in avanti. |
| `conversions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un&#39;azione (o azioni) predefinita ha attivato un evento per la valutazione delle prestazioni. |
| `federated` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica se è stato creato un evento esperienza tramite la federazione di dati, ad esempio la condivisione di dati tra i clienti. |
| `firstQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale ha riprodotto fino al 25% della sua durata a velocità normale. |
| `impressions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di ad impression inviate a un utente finale con il potenziale di visualizzazione. |
| `midpoints` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale ha riprodotto fino al 50% della sua durata a velocità normale. |
| `starts` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale ha iniziato a essere riprodotto. |
| `thirdQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il numero di volte in cui un annuncio video digitale ha riprodotto fino al 75% della sua durata a velocità normale. |
| `timePlayed` | [[!UICONTROL Misura]](../../data-types/measure.md) | Il tempo trascorso da un utente finale su una specifica risorsa multimediale temporizzata. |
| `downloadedPlayback` | Booleano | Quando è impostato su `true`, indica che l&#39;hit è generato a causa della riproduzione di una sessione pubblicitaria scaricata. |

{style=&quot;table-layout:auto&quot;}

## `adAssetReference` {#adAssetReference}

La `adAssetReference` acquisisce le informazioni sulle risorse relative all&#39;annuncio.

![struttura adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_dc.title` | Stringa | Il nome descrittivo e leggibile della risorsa dell&#39;annuncio. |
| `_xmpDM.duration` | Intero | La lunghezza o la durata della risorsa in secondi. |
| `_id` | Stringa | Un identificatore univoco della risorsa dell’annuncio, dopo la [Standard per AdID](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | Stringa | Azienda o marchio il cui prodotto è inserito nell’annuncio. |
| `campaign` | Stringa | ID della campagna pubblicitaria. |
| `creativeID` | Stringa | ID del contenuto creativo. |
| `creativeURL` | Stringa | URL del contenuto dell’annuncio. |
| `placementID` | Stringa | ID di posizionamento dell’annuncio. |
| `siteID` | Stringa | ID del sito dell’annuncio. |

{style=&quot;table-layout:auto&quot;}

## `adAssetViewDetails` {#adAssetViewDetails}

La `adAssetViewDetails` acquisisce i dettagli di visualizzazione per la riproduzione dell&#39;annuncio.

![struttura adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Pausa annunci]](../../data-types/ad-break.md) | Descrive come viene inserito un annuncio temporizzato nei file multimediali temporizzati. |
| `index` | Intero | Indice dell&#39;annuncio all&#39;interno dell&#39;interruzione pubblicitaria principale. Ad esempio, il primo annuncio ha un indice `0` e il secondo annuncio ha indice `1`. |
| `playerName` | Stringa | Nome del lettore che esegue il rendering dell’annuncio. |

{style=&quot;table-layout:auto&quot;}

## `adViewability` {#adViewability}

La `adViewability` acquisisce il numero di impression visualizzate dagli utenti finali, ad esempio il volume del lettore, la versione della libreria, lo stato della finestra e le dimensioni del riquadro di visualizzazione dell&#39;annuncio.

![struttura adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Dettagli di implementazione]](../../data-types/implementation-details.md) | Nome e versione della libreria utilizzata per misurare le metriche di visualizzabilità. |
| `measuredAdNotVisible` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che l&#39;annuncio non è visibile come misurato da una libreria di visualizzabilità al momento dell&#39;impression. |
| `measuredMuted` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che l’annuncio è disattivato come misurato da una libreria di visualizzabilità al momento dell’impression. |
| `unmeasurableIframe` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che l’annuncio viene visualizzato in una finestra inattiva, misurata da una libreria di visualizzabilità al momento dell’impression. |
| `unmeasurableOther` | [[!UICONTROL Misura]](../../data-types/measure.md) | Indica che la libreria di visualizzabilità non è in grado di eseguire correttamente le misurazioni a causa dell&#39;annuncio visualizzato all&#39;interno di un iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Impression(e) di un annuncio a un utente finale con la libreria di visualizzabilità strumentata. |
| `viewabilityCompletes` | [[!UICONTROL Misura]](../../data-types/measure.md) | Completamento di un annuncio pubblicitario per un utente finale ritenuto visualizzabile al momento del completamento da una libreria di visualizzabilità. |
| `viewableFirstQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Primo quartile(i) di un annuncio a un utente finale ritenuto visualizzabile al primo quartile di gioco da una libreria di visualizzabilità. |
| `viewableImpressions` | [[!UICONTROL Misura]](../../data-types/measure.md) | Impression di un annuncio a un utente finale ritenuto visualizzabile dopo due secondi di riproduzione da una libreria di visualizzabilità. |
| `viewableMidpoints` | [[!UICONTROL Misura]](../../data-types/measure.md) | Punto intermedio di un annuncio pubblicitario per un utente finale considerato visualizzabile al punto centrale del gioco da una libreria di visualizzabilità. |
| `viewableThirdQuartiles` | [[!UICONTROL Misura]](../../data-types/measure.md) | Terzo quartile(i) di un annuncio a un utente finale ritenuto visualizzabile al terzo quartile di gioco da una libreria di visualizzabilità. |
| `activeWindow` | Booleano | Indica se l&#39;annuncio è stato visualizzato nella finestra attiva del dispositivo dell&#39;utente. |
| `adHeight` | Intero | Il numero di pixel verticali del lettore, misurati in fase di runtime. Può essere più grande delle dimensioni dell&#39;annuncio se il lettore dispone di controlli o miniature aggiuntivi. |
| `adUnitDepth` | Intero | Gli editori possono incorporare le unità pubblicitarie all&#39;interno dei contenitori (iFrames) per limitare l&#39;accesso dell&#39;annuncio solo al codice della pagina. Questo valore descrive quanti contenitori l&#39;unità dell&#39;annuncio viene visualizzata all&#39;interno di. |
| `adWidth` | Intero | Il numero di pixel orizzontali del lettore, misurati in fase di runtime. Può essere più grande delle dimensioni dell&#39;annuncio se il lettore dispone di controlli o miniature aggiuntivi. |
| `measurementEligible` | Booleano | Se l’annuncio era idoneo o meno alla misurazione della visualizzabilità. Un annuncio è idoneo se l&#39;unità dispone di un formato creativo e di un tipo di tag supportati. |
| `percentViewable` | Intero | La percentuale di pixel nell’annuncio ritenuto visualizzabile al momento della misurazione. |
| `playerVolume` | Intero | Percentuale del volume del lettore misurata in fase di runtime, dove `0` è disattivato e `100` è il volume massimo. |
| `viewable` | Booleano | Indica se l&#39;annuncio è stato visualizzabile in fase di runtime. Gli annunci visualizzati sono considerati visualizzabili quando almeno il 50% dell’annuncio è visibile per almeno un secondo. Gli annunci video sono considerati visualizzabili quando almeno il 50% dell’annuncio è visibile durante la riproduzione del video per almeno due secondi consecutivi. |
| `viewportHeight` | Intero | La dimensione verticale (in pixel) della finestra in cui veniva visualizzata l’esperienza durante la misurazione in fase di runtime. Per un evento di visualizzazione Web, questo valore indica l&#39;altezza del riquadro di visualizzazione del browser. |
| `viewportWidth` | Intero | La dimensione orizzontale (in pixel) della finestra in cui veniva visualizzata l’esperienza durante la misurazione in fase di runtime. Per un evento di visualizzazione Web, questo valore indica la larghezza della finestra del browser. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
