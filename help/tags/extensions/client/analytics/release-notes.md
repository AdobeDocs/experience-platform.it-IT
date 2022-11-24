---
title: Note sulla versione di Adobe Analytics Extension
description: Note aggiornate sulla versione dell’estensione tag Adobe Analytics in Adobe Experience Platform.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 90%

---

# Note sulla versione dell’estensione Adobe Analytics

Di seguito è riportato un elenco di note sulla versione per l’estensione tag di Adobe Analytics.

>[!NOTE]
>
>L’estensione tag di Analytics viene spesso aggiornata in risposta agli aggiornamenti apportati al [Libreria JavaScript AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it). Fai riferimento a [Note sulla versione di AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it) per informazioni dettagliate sulle versioni specifiche menzionate di seguito.

## 23 settembre 2022

**Estensione Adobe Analytics 1.9.1**

**Funzioni**:

* Aggiornamento ad AppMeasurement v2.23.0.
* L&#39;estensione ora può raccogliere entropia elevata [suggerimenti client agente utente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) come supportato dall’ultima versione di AppMeasurement.

## 28 febbraio 2022

**Estensione Adobe Analytics 1.9.0**

**Correzioni di bug**:

* Sono state rimosse alcune istruzioni di debug in AppMeasurement.

## 29 novembre 2021

**Estensione Adobe Analytics 1.8.8**

**Correzioni di bug**:

* È stato aggiornato AppMeasurement alla versione v2.22.3.

## 16 settembre 2021

**Estensione Adobe Analytics 1.8.7**

**Correzioni di bug**:

* È stato aggiornato AppMeasurement alla versione v2.22.2.
* BuildInfo.environment è stato rimosso

## 24 agosto 2021

**Estensione Adobe Analytics 1.8.6**

**Correzioni di bug**:

* Aggiornato [AppMeasurement alla versione 2.2.1](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* È stato aggiornato fallback linkName per eseguire il mirroring della logica Activity Map invece di utilizzare innerHTML.

## 6 agosto 2020

**Estensione Adobe Analytics 1.8.5**

**Correzioni di bug**:

* Nelle impostazioni del modulo AAM veniva impostato un nome cookie errato se tale campo veniva lasciato vuoto. Questo problema è stato risolto.

**Funzioni**:

* È stato aggiornato [AppMeasurement alla versione 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html).
* È stata introdotta una piccola modifica nell’interfaccia utente e l’impostazione aggiuntiva è inserita in modalità ridotta in un pannello a soffietto, anziché come casella di controllo.

## 2 giugno 2020

**Estensione Adobe Analytics 1.8.4**

**Correzioni di bug**:

* È stato corretto un bug a causa del quale gli eventi del carrello (prodView, scAdd, scView, ecc.) non venivano visualizzati nel menu a discesa degli eventi. Ora dovrebbe essere possibile selezionare questi eventi dall’elenco a discesa.

**Funzioni**:

* Ora puoi disattivare Activity Map nell’estensione senza dover utilizzare un codice personalizzato. Activity Map viene caricato come modulo separato (come nel caso del modulo AAM) e puoi disattivarlo se lo desideri.
* È stata ripulita l’interfaccia utente riducendo al minimo le variabili della gerarchia e altre opzioni.
* È stato aggiunto un campo per impostare gli ID acquisto dall’interfaccia utente della configurazione dell’estensione.

## 10 marzo 2020

**Estensione Adobe Analytics 1.8.3**

**Correzioni di bug**:

* È stato corretto un bug che interessava la configurazione della regola che generava un errore quando si tentava di impostare le variabili, se si utilizzava una libreria personalizzata e le suite di rapporti non erano configurate in Analytics.
* Durante la creazione di un&#39;eVar, si è verificato un bug che non consentiva di visualizzare l&#39;opzione &quot;duplicare da&quot; un oggetto o viceversa. Ora è stato corretto per rispecchiare il comportamento delle versioni precedenti.

**Funzioni**:

* È stato aggiornato [AppMeasurement alla versione 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)

## 2 marzo 2020

**Estensione Adobe Analytics 1.8.2**

**Correzioni di bug**:

* È stato risolto un problema che causava l&#39;utilizzo di una sintassi non corretta per gli eventi numerici e la valuta serializzata

**Funzioni**:

* È stato aggiornato [AppMeasurement alla versione 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)
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

**Funzioni**:

* Ordina numericamente eVar, prop ed eventi nella visualizzazione Estensione
* Modifiche apportate sullo schema back-end per supportare i dati contestuali di Magento

## 6 settembre 2019

**Estensione Adobe Analytics 1.7.8**

**Correzioni di bug**:

* È stato corretto un bug per cui alcuni utenti non visualizzavano le opzioni della suite dei rapporti nel menu a discesa.
* È stato corretto un bug a causa del quale gli eventi non venivano attivati correttamente

## 5 settembre 2019

**Estensione Adobe Analytics 1.7.7**

**Funzioni**:

* AppMeasurement aggiornato alla versione 2.17
* Il modulo Gestione dell&#39;audience è stato aggiornato per supportare DIL 9.3
* Larghezze di campo aggiornate per offrire più spazio

**Correzioni di bug**:

* È stato corretto un bug per l&#39;impostazione di consenso/diniego
* È stato corretto un bug per cui le variabili non venivano impostate correttamente quando si utilizzava ECID

## 18 luglio 2019

**Estensione Adobe Analytics 1.7.6**

**Funzioni**:

* Aggiornamento dell&#39;estensione Adobe Analytics per supportare DIL 9.2 per Audience Manager

* Estensione aggiornata per supportare [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)
* È stata rimossa la seguente casella di controllo perché non è più supportata: &quot;Non allegare la destinazione che pubblica IFRAME al DOM o alle destinazioni di attivazione&quot;

## 4 giugno 2019

**Estensione Adobe Analytics 1.7.5**

**Funzioni**:

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

**Funzioni**:

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

**Funzioni**:

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

**Funzioni**:

* Aggiornamento dell&#39;estensione Adobe Analytics per supportare DIL 8.0 in Audience Manager
* Separazione del campo &quot;Serialize from value&quot; in due, &quot;Event ID&quot; e &quot;Event Value&quot;. Questo corregge il problema che stava assegnando un valore invece di serializzare un evento
   * Nota: se utilizzi il campo corrente per aggiungere un ID utilizzando una stringa (ad esempio Event7=3:abc123) dovrai aggiornare l&#39;input per riflettere l&#39;ID nel campo &quot;Event ID&quot;

**Correzioni di bug**:

* Correzione di un bug che non consentiva la corretta compilazione del codice valuta

## 11 ottobre 2018

**Estensione Adobe Analytics 1.4**

**Funzioni**:

* Migrazione del nome del cookie di tracciamento alla configurazione dell&#39;estensione.

**Correzioni di bug**:

* Correzione di un bug che consente ora alle variabili impostate di non bloccarsi se non è disponibile alcun oggetto trackerProperties.

## 5 giugno 2018

**Estensione Adobe Analytics 1.3**

**Funzioni**:

* Estensione Adobe Analytics aggiornata per supportare AppMeasurement 2.9.
* Aggiunta dell&#39;opzione &quot;Make tracker globally accessible&quot; nell&#39;estensione Adobe Analytics, che consente al tracker di essere delimitato a livello globale sotto`windows.s`.

**Correzioni di bug**:

* Correzione di un bug che causava il reset della visualizzazione elenco quando si tornava dalla visualizzazione di dettaglio
* Correzione di alcuni bug per migliorare il caricamento delle risorse nel selettore della revisione
* Correzione di un bug a causa del quale più regole sovrascrivevano s.events nell&#39;estensione Adobe Analytics

## 20 marzo 2018

**Estensione Adobe Analytics 1.2**

**Funzioni**:

* Aggiorna AppMeasurement.js a 2.8.0
* Aggiunge il supporto per l&#39;inoltro lato server

## 8 febbraio 2018

**Estensione Adobe Analytics 1.1**

**Funzioni**:

* AppMeasurement è stato aggiornato alla versione 2.6
* Il tracker inizializzato di Analytics ora è esposto tramite un modulo condiviso nell’estensione tag Adobe Experience Platform, così altre estensioni possono includere il codice necessario per interagire con esso.

**Correzioni di bug**:

* Risoluzione di un errore nell&#39;estensione Adobe Analytics che causava l&#39;apparizione di &quot;Error, missing Report Suite ID in AppMeasurement initialization&quot; nella console del browser.
