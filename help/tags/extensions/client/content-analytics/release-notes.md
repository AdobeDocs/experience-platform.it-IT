---
title: Note sulla versione per l’estensione Adobe Content Analytics
description: Note aggiornate sulla versione dell’estensione tag Content Analytics in Adobe Experience Platform.
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Note sulla versione dell’estensione Adobe Content Analytics

Di seguito è riportato un elenco delle note sulla versione dell’estensione tag Content Analytics.

| Versione | Data | Correzioni |
|---|---|---|
| <p>1.0.47</p> | <p>23 luglio 2025</p> | <ul><li>È stato corretto il bug che un cliente incontrava quando le esperienze non erano abilitate e il controllo delle espressioni regolari non riusciva. In questo modo i dati Content Analytics non vengono raccolti.</li><li>È stato corretto il bug predefinito relativo alla lingua che impediva la visualizzazione dell’interfaccia utente Tag per alcuni utenti se la lingua predefinita primaria non era impostata in Experience Cloud.</li></ul> |
| <p>1.0.46</p> | <p>18 giugno 2025</p> | <ul><li>Aggiunge una notifica popup se non è presente un flusso di dati di produzione durante il tentativo di salvare la configurazione dell’estensione.</li><li>Corregge temporaneamente il payload di Content Analytics in modo che sia visibile, ma inserisce il contenuto del payload di Content Analytics nella console.</li><li>Aggiunge la localizzazione all’interfaccia utente dell’estensione.</li><li>Corregge parzialmente un problema CSS con spaziatura aggiuntiva per il contenuto dell’interfaccia utente dell’estensione.</li></ul> |
| <p>1.0.45</p> | <p>14 aprile 2025</p> | <ul><li>Risolve alcuni bug nelle impostazioni di configurazione per quando si tengono eventi Content Analytics durante l’attesa degli eventi di visualizzazione della pagina. Ora Content Analytics attenderà per impostazione predefinita che vengano attivati gli eventi finché non si verifica l’evento PRIMA visualizzazione pagina.</li></ul> |
| <p>1.0.44</p> | <p>31 marzo 2025</p> | <ul><li>Prima iterazione dell’integrazione AppMeasurement.</li><li>Questa versione non supporta il filtro su richieste specifiche (ad esempio, visualizzazioni di pagina), ma potrebbe essere aggiunta in una data successiva.  Utilizza anche la prima istanza di AppMeasurement trovata nella pagina.</li></ul> |
| <p>1.0.43</p> | <p>10 marzo 2025</p> | <ul><li>Versione iniziale dell’estensione.</li></ul> |

