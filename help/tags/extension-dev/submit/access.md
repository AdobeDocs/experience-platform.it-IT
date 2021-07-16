---
title: Concedere l’accesso agli utenti
description: Imposta gli account utente e le autorizzazioni dei tag dei membri del tuo team in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 25%

---

# Concedere l’accesso agli utenti

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Prima di iniziare a usare l’extension_package, è necessario fornire a ogni membro del gruppo un proprio account utente e le relative autorizzazioni. Puoi eseguire questa operazione in [Adobe Admin Console](https://adminconsole.adobe.com/).

Questo documento fornisce passaggi per consentire l’accesso ai tag in Adobe Experience Platform tramite Admin Console.

## Prerequisiti 

Per questa guida si presuppone che chi legge sia un Amministratore dell’organizzazione designato da Admin Console. Per ulteriori informazioni su Admin Console e sull’assegnazione dei ruoli, consulta le seguenti risorse:

* [Guida utente per l’amministrazione](https://helpx.adobe.com/it/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js): informazioni su tutte le funzioni di Admin Console
* [Ruoli di amministrazione Enterprise](https://helpx.adobe.com/it/enterprise/using/admin-roles.html): informazioni sui diversi tipi di ruolo di amministrazione. Per quanto riguarda la presente guida, si presuppone che chi legge sia un Amministratore dell’organizzazione.

## Scegliere l&#39;organizzazione

L’amministratore dell’organizzazione Adobe Experience Cloud deve effettuare l’accesso ad [Admin Console](https://adminconsole.adobe.com/). La prima schermata è la panoramica.

![Scheda Panoramica di Admin Console](../images/getting-started/admin-console-overview.png)

Alcuni di voi possono avere accesso a più organizzazioni (Org). Per aggiungere la funzionalità tag all’organizzazione corretta, seleziona il nome dell’organizzazione visualizzato nell’angolo in alto a destra dello schermo. Quindi scegli l’organizzazione in cui desideri utilizzare i tag dall’elenco a discesa.

![Menu a discesa per la selezione dell’organizzazione di Admin Console](../images/getting-started/admin-console-choose-org.png)

## Creare un profilo di prodotto

Un profilo di prodotto è un gruppo. Quando si assegnano specifici diritti a un profilo prodotto, questi vengono applicati a tutti gli utenti inclusi nel profilo.

Scegli il collegamento **[!UICONTROL Prodotti]** in alto e **[!UICONTROL Experience Cloud]** a sinistra. Se Adobe Experience Platform Launch non è presente nell’elenco, i clienti devono contattare il team del proprio account e i partner devono inviare un messaggio e-mail <ExchangeTechEC@adobe.com>.

![Scheda Prodotti di Admin Console](../images/getting-started/admin-console-products-launch.png)

La schermata precedente mostra un profilo di esempio, potresti non averne ancora uno. Per crearne uno, seleziona **[!UICONTROL Nuovo profilo]**. Nella schermata **Crea un nuovo profilo**, aggiungi un **Nome profilo** (ad esempio, test di raccolta dati) e un **Descrizione** facoltativo, quindi seleziona **[!UICONTROL Salva]**:

![Crea nuova visualizzazione profilo](../images/getting-started/admin-console-create-a-new-profile.png)

Il profilo di prodotto è stato aggiunto all’organizzazione. Quindi, aggiungi gli utenti al profilo di prodotto.

## Assegnare gli utenti al profilo di prodotto

Il profilo di prodotto mostra zero per **UTENTI TITLED** e **AMMINS**. Seleziona il nome del profilo di prodotto creato (test di raccolta dati nel nostro esempio).

![Visualizzazione dei profili di prodotto](../images/getting-started/admin-console-profiles-add-user.png)

Seleziona la scheda **[!UICONTROL Utenti]** . Qui puoi cercare gli utenti Adobe ID esistenti tramite e-mail o aggiungere nuovi utenti a questo profilo di prodotto. Seleziona **[!UICONTROL Aggiungi collegamento utente]**.

![Scheda Utenti dei profili di prodotto](../images/getting-started/admin-console-add-launch-user.png)

Immetti un nome, un gruppo di utenti o un indirizzo e-mail nel campo di testo appropriato. Se possibile, si consiglia di includere un nome e un cognome. Seleziona **[!UICONTROL Salva]** per aggiungere l&#39;utente.

![Aggiungi utente alla visualizzazione Profilo](../images/getting-started/admin-console-add-user.png)

Quando disponi di tutti gli utenti necessari in questo profilo di prodotto, verranno aggiunte le relative autorizzazioni. Seleziona la scheda **[!UICONTROL Autorizzazioni]** . Nella schermata delle autorizzazioni vengono visualizzati **[!UICONTROL Proprietà]**, **[!UICONTROL Diritti aziendali]** e **[!UICONTROL Diritti di proprietà]**. Selezionare **[!UICONTROL Modifica]**.

![Scheda Autorizzazioni dei profili di prodotto](../images/getting-started/admin-console-profile-permissions.png)

Per creare estensioni, il team deve disporre di almeno le seguenti autorizzazioni:

* &quot;Gestisci proprietà&quot; dal gruppo aziendale.
* &quot;Gestisci estensioni&quot;, &quot;Gestisci ambienti&quot; e &quot;Sviluppa&quot; dal gruppo di proprietà.

Puoi creare profili di prodotto aggiuntivi con diritti più limitati in un secondo momento, ma per ora seleziona semplicemente **[!UICONTROL + Aggiungi tutto]** sia per **Diritti aziendali** che per **Diritti di proprietà**. Assicurati di selezionare **[!UICONTROL Salva]** su ciascuno di essi.

![Gestisci diritti di proprietà](../images/getting-started/admin-console-add-all-property-rights.png)

![Gestire i diritti aziendali](../images/getting-started/admin-console-add-all-company-rights.png)

Finora abbiamo scelto l’organizzazione appropriata, creato un profilo di prodotto, aggiunto utenti al profilo di prodotto e assegnato le autorizzazioni.

Questa operazione completa la configurazione richiesta in Admin Console. Ora tu e il tuo team che sono stati configurati come utenti puoi accedere a [Interfaccia utente di raccolta dati](https://launch.adobe.com/).

## Conferma del provisioning

Dopo aver effettuato il provisioning della tua azienda con accesso ai tag e aver configurato i tuoi utenti come descritto in precedenza, dovresti essere in grado di accedere all’ambiente di produzione dall’ [Interfaccia di raccolta dati](https://launch.adobe.com/). Se hai effettuato il provisioning dei tag e hai completato i passaggi di Admin Console descritti qui sopra, ma non riesci ancora ad accedere all’interfaccia utente di raccolta dati, contatta il tuo rappresentante di supporto Adobe.
