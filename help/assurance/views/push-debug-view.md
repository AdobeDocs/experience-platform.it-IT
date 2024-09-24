---
title: Visualizzazione debug push
description: Questa guida contiene informazioni dettagliate sulla visualizzazione Debug push in Adobe Experience Platform Assurance.
exl-id: a9558ee2-2e80-4b0d-ab45-2020be85e634
source-git-commit: f9cc088cdda4323c80e35978fcde373cbba9204d
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 86%

---

# Visualizzazione debug push

La visualizzazione debug push all’interno di Adobe Experience Platform Assurance consente di convalidare la configurazione push per l’app e inviare un messaggio di test al tuo dispositivo.

## Client

![Client push](./images/push-debug-view/clients.png)

Il menu a discesa client contiene l’elenco di ogni client univoco connesso a questa sessione di Assurance. Un client è un dispositivo univoco o un’installazione app univoca per un dispositivo. Ad esempio, se un dispositivo Android e un dispositivo iOS sono stati collegati alla sessione, tali client verranno visualizzati nel menu a discesa Client.

Dopo aver reinstallato e riconnesso l’app su un dispositivo, verrà visualizzato un altro client. Se un dispositivo con quel nome esiste già, il nuovo menu a discesa aggiungerà un #2 al nome.

Questa vista è abilitata solo per un singolo client, quindi selezionando un client diverso verranno modificati i dettagli sullo schermo.

## Convalida configurazione

La scheda **[!UICONTROL Convalida configurazione]** convalida e fornisce ulteriori dettagli sulla configurazione push dell’app. Sono disponibili tre pannelli che eseguono le convalide. Se tutte le convalide hanno esito positivo, verrà visualizzato un segno di spunta verde. Se sono presenti tre segni di spunta verdi, significa che l’app è stata configurata correttamente per i messaggi push, scrive token push nel profilo utente e dispone di una configurazione di canale associata.

Se qualcosa non funziona come previsto, viene visualizzato un avviso con i dettagli su come risolvere il problema:

![Stato non valido](./images/push-debug-view/invalid-state.png)

### Dettagli client

Questo pannello verifica che il dispositivo sia configurato correttamente. Ciò include la configurazione dell’estensione nell’interfaccia utente di Raccolta dati, l’inizializzazione dell’estensione e dei relativi prerequisiti nell’applicazione e l’acquisizione del token push dal dispositivo.

Se valido, il pannello visualizza l’ECID del dispositivo, il token push, il nome e il tipo della sandbox Edge.

### Dettagli profilo

Una volta configurato correttamente il client, questo pannello verifica che il dispositivo stia scrivendo sul profilo. Inoltre, verifica che il token push nel profilo corrisponda a quello sul dispositivo.

Se valido, il pannello mostrerà l’ECID del dispositivo, il token push, l’ID app dell’applicazione, la piattaforma di messaggistica e se il token push è stato inserito nell’elenco non consentiti. Il token può essere inserito nell’elenco non consentiti per vari motivi, ad esempio se l’utente ha disinstallato l’app o se ha disabilitato i messaggi push per l’app.

![Bloccato](./images/push-debug-view/deny-list-blocked.png)

Infine, nella parte inferiore del pannello è presente un collegamento che consente di aprire questo profilo specifico in una nuova scheda.

### Credenziali e configurazione di AppStore

Questo pannello verifica che per l’ID app e la piattaforma di messaggistica salvati nel profilo sia stata creata una configurazione di canale corrispondente. In una configurazione di canale vengono caricate le credenziali push per l’applicazione.

Se valido, il profilo visualizzerà il nome della configurazione del canale, l’ID dell’app e il nome del servizio di messaggistica.

## Invia push di test

La scheda **[!UICONTROL Invia push di test]** può essere utilizzata per inviare un messaggio di test al dispositivo.

È possibile configurare diversi riquadri per testare diverse funzioni push di iOS e Android. Una volta configurati, seleziona **[!UICONTROL Invia notifica push di test]** per inviare il messaggio.

![Invia push](./images/push-debug-view/send.png)

### Messaggio

Nel riquadro **[!UICONTROL Messaggio]**, è possibile specificare un titolo e un corpo per il messaggio. Qui può essere abilitata la funzione di notifica silenziosa.

![Riquadro messaggio](./images/push-debug-view/message-pane.png)

### Destinazione push

Il riquadro **[!UICONTROL Destinazione push]** consente di personalizzare il token push e la configurazione del canale da utilizzare per l&#39;invio del messaggio push.

Queste informazioni vengono fornite per impostazione predefinita se la scheda **[!UICONTROL Convalida configurazione]** mostra tre segni di spunta verdi. Tuttavia, puoi fornire un token push personalizzato e la configurazione del canale, anche se l’app non è completamente configurata.

![Riquadro di destinazione](./images/push-debug-view/target-pane.png)

### Comportamento dei clic

Dal riquadro **[!UICONTROL Comportamento del clic]**, è possibile scegliere il comportamento da adottare quando si fa clic sulla notifica push sul dispositivo. Per impostazione predefinita, l’app viene aperta, ma è possibile aprire un deep link o una pagina web.

Se scegli di utilizzare un deep link, lo sviluppatore dell’app deve crearne uno per te.

![Riquadro Comportamento](./images/push-debug-view/click-behavior.png)

### Contenuti multimediali avanzati

Il riquadro **[!UICONTROL Contenuti multimediali avanzati]** consente di aggiungere al messaggio altri contenuti multimediali, ad esempio immagini, video o GIF. Per abilitare questa funzione, lo sviluppatore dell’app deve aggiungere il codice all’app.

![Riquadro avanzato](./images/push-debug-view/rich-pane.png)

### Pulsanti

Il riquadro **[!UICONTROL Pulsanti]** consente di aggiungere pulsanti aggiuntivi alla notifica push. Ogni pulsante può aprire l’app, un deep link nell’app o una pagina web.

Per abilitare questa funzione, lo sviluppatore dell’app deve aggiungere il codice all’app.

![Riquadro pulsanti](./images/push-debug-view/buttons-pane.png)

### Dati personalizzati

Il riquadro **[!UICONTROL Dati personalizzati]** consente di aggiungere dati personalizzati alla notifica push. Ogni coppia chiave/valore viene inviata come metadati insieme al messaggio e può essere utilizzata dagli sviluppatori per creare esperienze efficaci e aggiungere un ulteriore tracciamento.

![Riquadro personalizzato](./images/push-debug-view/custom-pane.png)

## Risultati del test

Dopo aver inviato un messaggio, la sezione **[!UICONTROL Risultati del test]** riceve i dati dal servizio push per il messaggio. Qui puoi vedere se il messaggio è stato inviato ai servizi di messaggistica Google/iOS:

![Risultati del test](./images/push-debug-view/test-results.png)

Se si sono verificati dei problemi, vengono visualizzati qui:

![Errore nei risultati test](./images/push-debug-view/test-error.png)

## Avanzate

### Visualizza payload del messaggio

Accanto al pulsante **[!UICONTROL Invia notifica push di test]** sono presenti dei puntini di sospensione con un menu a comparsa. Da qui puoi visualizzare il payload del messaggio. Questo consente di visualizzare il messaggio esatto che verrà inviato al servizio di messaggistica remota. Puoi rivedere questo payload o anche copiarlo e incollarlo in uno strumento per testare push sul desktop.

![Riquadro personalizzato](./images/push-debug-view/message-payload.png)
