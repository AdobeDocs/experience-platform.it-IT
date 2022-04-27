---
title: Note sulla versione per i tag
description: Note aggiornate sulla versione dei tag di Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 58%

---

# Note sulla versione dei tag in Adobe Experience Platform

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 15 novembre 2021

**Accettare il codice ES6 nei tag** - È ora possibile utilizzare estensioni e codice personalizzato contenente codice ES6 in Tags. Nel catalogo delle estensioni verrà visualizzata un&#39;etichetta ES6+ all&#39;interno della scheda di ogni estensione che contiene codice ES6. IE10 e IE11 non supportano il codice ES6. Prima di utilizzare il codice ES6 nelle librerie dei tag, esegui la dovuta diligenza.

**Utilizzo di Terser come compressore JavaScript** - Uglifier è stato sostituito con Terser. A partire da questa versione, tutte le librerie di tag vengono minimizzate da Terser.

## 21 ottobre 2021

**Inviare dati agli endpoint autenticati nell&#39;inoltro eventi** - Utilizzando i segreti, puoi inviare dati agli endpoint che richiedono i seguenti protocolli di autenticazione:

* **[!UICONTROL Token]**: Una singola stringa di caratteri che rappresenta un valore del token di autenticazione.
* **[!UICONTROL HTTP semplice]**: Contiene due attributi di stringa per un nome utente e una password.
* **[!UICONTROL OAuth2]**: Contiene diversi attributi per supportare il [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) specifiche

Per ulteriori informazioni, consulta le guide [gestione dei segreti nell’interfaccia utente Raccolta dati](../ui/event-forwarding/secrets.md) o [gestione dei segreti nell’API di Reactor](../api/guides/secrets.md).

## 19 luglio 2021

**Regolazioni a destra di &quot;Gestisci proprietà&quot;** - Il diritto Manage Properties (Gestisci proprietà) ha riscontrato un problema per cui un utente disponeva dell&#39;autorizzazione per creare una nuova proprietà ma non poteva visualizzarla dopo la creazione (come descritto nel thread della community) [qui](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). Una correzione è ora attiva e le autorizzazioni vengono applicate come descritto nell&#39;articolo.

>[!NOTE]
>
>Se assegni il nuovo diritto &quot;Modifica proprietà&quot; a un gruppo di utenti, l’interfaccia utente non si aggiorna per abilitare i campi nella schermata di configurazione delle proprietà. Una correzione di questo problema verrà implementata in una prossima versione.

## 17 maggio 2021

**Gestione migliore delle modifiche non salvate**: in passato, quando ci si allontanava da una vista delle impostazioni (estensioni, elementi dati e componenti regola) veniva richiesto se si desiderasse ignorare le modifiche. Tuttavia, la logica per determinare questa situazione non era molto efficiente e spesso veniva chiesto di salvare i cambiamenti anche se non ce n’erano. Questo problema è stato corretto. Da ora in poi, il messaggio dovrebbe comparire solo se sono state effettivamente apportate delle modifiche.

## 10 maggio 2021

**Pubblicazione semplificata**: non è più necessario creare nell’ambiente di staging. Se disponi dei diritti appropriati, puoi saltare completamente lo stato Inviato e pubblicare direttamente dall’ambiente Sviluppo, purché la build sia stata compilata correttamente e non siano presenti altre librerie a monte.

## 22 aprile 2021

**Data Collection di Adobe Experience Platform**: l’invio di dati ad Adobe non riguarda solo la distribuzione di tag nel sito o la configurazione nell’app.  L’utilizzo degli SDK per Experience Platform e della rete Edge richiede l’accesso ad altre funzionalità di Platform. Questo richiedeva l’accesso ad alcuni strumenti diversi, che ora sono tutti disponibili in un unico posto.

Data Collection di Platform è composto da sei funzionalità; inoltre, il nuovo e più semplice sistema di navigazione conterrà solo gli elementi a cui la tua azienda e il tuo account utente hanno accesso.  Alcuni dei nomi delle funzionalità sono stati aggiornati per corrispondere ai pattern di denominazione di Experience Platform.

* Client (precedentemente disponibile come Client Side)
* Datastream (precedentemente disponibili come Configurazioni Edge)
* Server (precedentemente disponile come Server Side)
* Configurazioni app
* Schemi
* Identità

Man mano che Experience Platform e la funzionalità di raccolta dati continuano a evolvere, verranno rilasciati ulteriori aggiornamenti.

## 18 febbraio 2021

* L’interfaccia utente diData Collection è stata aggiornata a react-spectrum v3
* Schede di estensione aggiornate ai pattern Spectrum più recenti
* Sono state aumentate le dimensioni dei campi nome in tutta l’app.

## 13 gennaio 2021

**Disponibilità generale: Inoltro eventi** Inoltra i dati a livello di evento alla rete edge di Adobe Experience Platform, quindi utilizza l’inoltro degli eventi per trasformare, arricchire e inviare tali dati a un endpoint non Adobe utilizzando i server di Adobe, non il client, con latenza ridotta.

Consulta la sezione [panoramica sull&#39;inoltro eventi](../ui/event-forwarding/overview.md) e [guida introduttiva](../ui/event-forwarding/getting-started.md) per ulteriori informazioni.
