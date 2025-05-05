---
title: Note sulla versione di Adobe Analytics Extension
description: Note aggiornate sulla versione dell’estensione tag Adobe Analytics in Adobe Experience Platform.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: 5f4e157a39bf927b3821931d55f968862b2ed16d
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 69%

---

# Note sulla versione dell’estensione Adobe Analytics

Di seguito è riportato un elenco delle note sulla versione dell’estensione tag Adobe Analytics.

>[!NOTE]
>
>Estensione tag Analytics se spesso aggiornata in risposta agli aggiornamenti alla [libreria JavaScript AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it). Consulta le [note sulla versione dell&#39;AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it) per informazioni dettagliate sulle versioni specifiche menzionate di seguito.

## 28 ottobre 2024

**Estensione Adobe Analytics 1.9.6**

**Caratteristiche**:

* È stata aggiunta una nuova funzionalità che consente agli utenti di visualizzare e modificare una versione JSON dell&#39;[azione Imposta variabili](https://experienceleague.adobe.com/it/docs/experience-platform/tags/extensions/client/analytics/overview#set-variables). L&#39;estensione Adobe Web SDK include anche un&#39;azione per [compilare una variabile di analisi](https://experienceleague.adobe.com/it/docs/experience-platform/tags/extensions/client/web-sdk/data-element-types) fornendo JSON. Copiando i dati JSON dall’estensione AA all’estensione Web SDK, i clienti che eseguono la migrazione possono facilmente trasferire più impostazioni contemporaneamente, anziché aggiungere manualmente ogni variabile.

## 12 agosto 2024

**Estensione Adobe Analytics 1.9.5**

**Caratteristiche**:

* Aggiornamento a [AppMeasurement a v2.27.0](https://github.com/adobe/appmeasurement/releases/tag/v2.27.0).

## martedì 4 marzo 2024

**Estensione Adobe Analytics 1.9.4**

**Caratteristiche**:

* Aggiornamento a [AppMeasurement a v2.26.0](https://github.com/adobe/appmeasurement/releases/tag/v2.26.0).

## sabato 15 settembre 2023

**Estensione Adobe Analytics 1.9.3**

**Caratteristiche**:

* Aggiornamento a [AppMeasurement a v2.25.0](https://github.com/adobe/appmeasurement/releases/tag/v2.25.0).


## giovedì 19 luglio 2023

**Estensione Adobe Analytics 1.9.2**

**Caratteristiche**:

* Aggiornamento a [AppMeasurement v2.24.0](https://github.com/adobe/appmeasurement/releases/tag/v2.24.0).
* È stata aggiunta una configurazione facoltativa (`decodeLinkParameters` `false` predefinito) che decodifica gli URL di collegamento che includono caratteri con codifica a doppio byte.

**Correzioni di bug**:

* È stata aggiunta una gestione aggiuntiva degli errori per i browser con API [User-Agent client hints](https://experienceleague.adobe.com/docs/analytics/technotes/client-hints.html?lang=it) errate ad alta entropia.
* Intestazione Content-Type [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) modificata per l&#39;utilizzo di `x-www-form-urlencoded` per impostazione predefinita.

## sabato 23 settembre 2022

**Estensione Adobe Analytics 1.9.1**

**Caratteristiche**:

* Aggiornato all’AppMeasurement v2.23.0.
* L&#39;estensione può ora raccogliere [hint client dall&#39;agente utente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) ad alta entropia come supportato dall&#39;ultima versione di AppMeasurement.

## martedì 28 febbraio 2022

**Estensione Adobe Analytics 1.9.0**

**Correzioni di bug**:

* Sono state rimosse alcune istruzioni di debug in AppMeasurement.

## martedì 29 novembre 2021

**Estensione Adobe Analytics 1.8.8**

**Correzioni di bug**:

* È stato aggiornato l’AppMeasurement alla versione v2.22.3.

## 16 settembre 2021

**Estensione Adobe Analytics 1.8.7**

**Correzioni di bug**:

* È stato aggiornato l’AppMeasurement alla versione v2.22.2.
* BuildInfo.environment obsoleto rimosso

## 24 agosto 2021

**Estensione Adobe Analytics 1.8.6**

**Correzioni di bug**:

* [AppMeasurement aggiornato alla versione v2.22.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it).
* LinkName di fallback aggiornato per riflettere la logica Activity Map anziché utilizzare innerHTML.

## 6 agosto 2020

**Estensione Adobe Analytics 1.8.5**

**Correzioni di bug**:

* Nelle impostazioni del modulo AAM veniva impostato un nome cookie errato se tale campo veniva lasciato vuoto. Questo problema è stato risolto.

**Caratteristiche**:

* È stato aggiornato [AppMeasurement alla versione 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it).
* È stata introdotta una piccola modifica nell’interfaccia utente e l’impostazione aggiuntiva è inserita in modalità ridotta in un pannello a soffietto, anziché come casella di controllo.

## 2 giugno 2020

**Estensione Adobe Analytics 1.8.4**

**Correzioni di bug**:

* È stato corretto un bug a causa del quale gli eventi del carrello (prodView, scAdd, scView, ecc.) non venivano visualizzati nel menu a discesa degli eventi. Ora dovrebbe essere possibile selezionare questi eventi dall’elenco a discesa.

**Caratteristiche**:

* Ora puoi disattivare Activity Map nell’estensione senza dover utilizzare un codice personalizzato. Activity Map viene caricato come modulo separato (come nel caso del modulo AAM) e puoi disattivarlo se lo desideri.
* È stata ripulita l’interfaccia utente riducendo al minimo le variabili della gerarchia e altre opzioni.
* È stato aggiunto un campo per impostare gli ID acquisto dall’interfaccia utente della configurazione dell’estensione.

## 10 marzo 2020

**Estensione Adobe Analytics 1.8.3**

**Correzioni di bug**:

* È stato corretto un bug che interessava la configurazione della regola che generava un errore quando si tentava di impostare le variabili, se si utilizzava una libreria personalizzata e le suite di rapporti non erano configurate in Analytics.
* Durante la creazione di un&#39;eVar, si è verificato un bug che non consentiva di visualizzare l&#39;opzione &quot;duplicare da&quot; un oggetto o viceversa. Ora è stato corretto per rispecchiare il comportamento delle versioni precedenti.

**Caratteristiche**:

* È stato aggiornato [AppMeasurement alla versione 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it)

## 2 marzo 2020

**Estensione Adobe Analytics 1.8.2**

**Correzioni di bug**:

* È stato risolto un problema che causava l&#39;utilizzo di una sintassi non corretta per gli eventi numerici e la valuta serializzata

**Caratteristiche**:

* È stato aggiornato [AppMeasurement alla versione 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it)
* È stata aggiornata la libreria DIL nel modulo Audience Manager alla versione 9.4
* È stata aumentata la lunghezza dei campi di input nell&#39;estensione
* Le eVar e le proprietà nelle configurazioni di estensione e azione ora mostrano il nome descrittivo di Analytics
* È stata aggiunta una casella di controllo nella sezione &quot;Cookie&quot; della configurazione di estensione che consente di scrivere cookie protetti
* Sono state aggiunte tre nuove configurazioni al modulo Audience Manager. È stata aggiunta un&#39;impostazione per abilitare la registrazione, le destinazioni URL e le destinazioni dei cookie

## 13 novembre 2019

**Estensione Adobe Analytics 1.8.1**

**Correzioni di bug**:

* È stato corretto un bug a causa del quale le variabili eVar e prop non venivano salvate.

## 1 novembre 2019

**Estensione Adobe Analytics 1.8.0**

**Correzioni di bug**:

* Correzione di un bug a causa del quale una piccola quantità di clienti non poteva visualizzare le opzioni della suite di report nel menu a discesa
* Correzione di un bug per cui le variabili non venivano impostate correttamente quando si utilizzava ECID

**Caratteristiche**:

* Ordina numericamente eVar, prop ed eventi nella visualizzazione Estensione
* Modifiche apportate sullo schema back-end per supportare i dati contestuali di Magento

## 6 settembre 2019

**Estensione Adobe Analytics 1.7.8**

**Correzioni di bug**:

* È stato corretto un bug per cui alcuni utenti non visualizzavano le opzioni della suite dei rapporti nel menu a discesa.
* È stato corretto un bug a causa del quale gli eventi non venivano attivati correttamente

## 5 settembre 2019

**Estensione Adobe Analytics 1.7.7**

**Caratteristiche**:

* AppMeasurement aggiornato alla versione 2.17
* Il modulo Gestione dell&#39;audience è stato aggiornato per supportare DIL 9.3
* Larghezze di campo aggiornate per offrire più spazio

**Correzioni di bug**:

* È stato corretto un bug per l&#39;impostazione di consenso/diniego
* È stato corretto un bug per cui le variabili non venivano impostate correttamente quando si utilizzava ECID

## 18 luglio 2019

**Estensione Adobe Analytics 1.7.6**

**Caratteristiche**:

* Aggiornamento dell&#39;estensione Adobe Analytics per supportare DIL 9.2 per Audience Manager

* Estensione aggiornata per supportare [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it#version-2.15.0)
* È stata rimossa la seguente casella di controllo perché non è più supportata: &quot;Do not attach the destination publishing IFRAME to the DOM or fire destinations&quot;

## 4 giugno 2019

**Estensione Adobe Analytics 1.7.5**

**Caratteristiche**:

* Aggiornamento dell&#39;estensione [Adobe Analytics ad AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it#version-2.14.0) che include una correzione a un problema clearVar noto
* Aggiunta di un collegamento Exchange all&#39;estensione. L&#39;elenco di Exchange può essere raggiunto facendo clic sul menu a discesa e selezionando &quot;informazioni estensione&quot;

**Correzioni di bug**:

* Correzione di un bug nell&#39;interfaccia utente che mostrava l&#39;eliminazione di un eVar errato da un elenco
* Correzione di un bug che richiedeva un server di tracciamento SSL quando si tentavano di aggiungere più suite di rapporti. Quando si aggiungono più suite di rapporti è necessario un server di tracciamento, ma il campo del server di tracciamento SSL è facoltativo.

## 15 aprile 2019

**Estensione Adobe Analytics 1.7.4**

**Correzioni di bug**:

* Estensione ridotta dopo aver trovato un bug in AppMeasurement 2.13.0. causava un problema che non inviava l&#39;ECID, quindi se hai installato 1.7.3 ti consigliamo di effettuare l&#39;aggiornamento alla versione 1.7.4 per evitare il problema. I clearVar continueranno fino a quando non verrà distribuita una versione aggiornata di AppMeasurement

## 12 aprile 2019

**Estensione Adobe Analytics 1.7.3**

**Correzioni di bug**:

* Aggiornamento dell&#39;estensione Adobe Analytics ad AppMeasurement 2.13.0 che include una correzione a un problema clearVar noto.

## 21 marzo 2019

**Estensione Adobe Analytics 1.7.2**

**Caratteristiche**:

* Aggiornamento dell&#39;estensione Adobe Analytics a DIL 9.1.
* Aggiornamento dell&#39;estensione Adobe Analytics ad AppMeasurement 2.12.
* Aggiornamento della visualizzazione dell&#39;estensione Adobe Analytics a React-Spectrum.
* Durante la configurazione delle suite di rapporti nella pagina di configurazione, ora visualizzi un menu a discesa di tutte le suite di rapporti della società per facilitare la selezione della suite di rapporti appropriata.

## 7 marzo 2019

**Estensione Adobe Analytics 1.7.1**

**Correzioni di bug**:

* Rollback dell&#39;estensione alla versione 1.6 dopo che è stato trovato un bug in 1.7.

## 11 febbraio 2019

**Estensione Adobe Analytics 1.6**

**Caratteristiche**:

* Aggiornamento dell&#39;estensione Adobe Analytics a DIL 9.0, che supporterà l&#39;opt-in.
* Aggiornamento dell&#39;estensione Adobe Analytics ad AppMeasurement 2.11 per supportare l&#39;opt-in.

**Correzioni di bug**:

* Risoluzione di un conflitto con Prototype JS. L&#39;estensione Analytics ora supporterà le librerie prototype.js standard.

## 9 novembre 2018

**Estensione Adobe Analytics 1.5.1**

**Correzioni di bug**:

* Downgrade del modulo DIL a 7.0 per correggere una questione che causava problemi con i beacon Analytics non attivati

## 5 novembre 2018

**Estensione Adobe Analytics 1.5**

**Caratteristiche**:

* Aggiornamento dell&#39;estensione Adobe Analytics per supportare DIL 8.0 in Audience Manager
* Separazione del campo &quot;Serialize from value&quot; in due, &quot;Event ID&quot; e &quot;Event Value&quot;. Questo corregge il problema che stava assegnando un valore invece di serializzare un evento
   * Nota: se utilizzi il campo corrente per aggiungere un ID utilizzando una stringa (ad esempio Event7=3:abc123) dovrai aggiornare l&#39;input per riflettere l&#39;ID nel campo &quot;Event ID&quot;

**Correzioni di bug**:

* Correzione di un bug che non consentiva la corretta compilazione del codice valuta

## 11 ottobre 2018

**Estensione Adobe Analytics 1.4**

**Caratteristiche**:

* Migrazione del nome del cookie di tracciamento alla configurazione dell&#39;estensione.

**Correzioni di bug**:

* Correzione di un bug che consente ora alle variabili impostate di non bloccarsi se non è disponibile alcun oggetto trackerProperties.

## 5 giugno 2018

**Estensione Adobe Analytics 1.3**

**Caratteristiche**:

* Estensione Adobe Analytics aggiornata per supportare AppMeasurement 2.9.
* Aggiunta dell&#39;opzione &quot;Make tracker globally accessible&quot; nell&#39;estensione Adobe Analytics, che consente al tracker di essere delimitato a livello globale sotto`windows.s`.

**Correzioni di bug**:

* Correzione di un bug che causava il reset della visualizzazione elenco quando si tornava dalla visualizzazione di dettaglio
* Correzione di alcuni bug per migliorare il caricamento delle risorse nel selettore della revisione
* Correzione di un bug a causa del quale più regole sovrascrivevano s.events nell&#39;estensione Adobe Analytics

## 20 marzo 2018

**Estensione Adobe Analytics 1.2**

**Caratteristiche**:

* Aggiorna AppMeasurement.js a 2.8.0
* Aggiunge il supporto per l&#39;inoltro lato server

## 8 febbraio 2018

**Estensione Adobe Analytics 1.1**

**Caratteristiche**:

* AppMeasurement è stato aggiornato alla versione 2.6
* Il tracker inizializzato di Analytics ora è esposto tramite un modulo condiviso nell’estensione tag Adobe Experience Platform, così altre estensioni possono includere il codice necessario per interagire con esso.

**Correzioni di bug**:

* Risoluzione di un errore nell&#39;estensione Adobe Analytics che causava l&#39;apparizione di &quot;Error, missing Report Suite ID in AppMeasurement initialization&quot; nella console del browser.
