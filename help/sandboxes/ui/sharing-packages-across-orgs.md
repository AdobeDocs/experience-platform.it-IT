---
title: Condivisione di pacchetti tra organizzazioni tramite strumenti sandbox
description: Scopri come utilizzare gli strumenti Sandbox in Adobe Experience Platform per condividere pacchetti tra diverse organizzazioni.
badge: Beta
source-git-commit: 492f1d9dc08965dba3f1c5b6e1d479ef645afd04
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Condividere pacchetti tra organizzazioni utilizzando gli strumenti sandbox

>[!NOTE]
>
>La condivisione di pacchetti tra organizzazioni è attualmente in versione beta e disponibile solo per alcuni clienti beta.

Questo documento illustra come utilizzare gli strumenti sandbox in Adobe Experience Platform per condividere pacchetti tra diverse organizzazioni.

Migliora la precisione della configurazione nelle sandbox ed esporta e importa facilmente le configurazioni sandbox tra sandbox di diverse organizzazioni con la funzione di strumenti sandbox. Esistono due tipi di pacchetti condivisi:

**Pacchetto privato**

I pacchetti privati possono essere condivisi solo con le organizzazioni che hanno approvato la richiesta di condivisione dall’organizzazione di origine tramite un elenco consentiti di consenso.

**Pacchetto pubblico**

I pacchetti pubblici sono disponibili per l’importazione senza alcuna approvazione aggiuntiva. Questi pacchetti possono essere condivisi sul sito web, sul blog o sulla piattaforma di un partner. Il payload del pacchetto consente di copiare e incollare i pacchetti da questi canali nell’organizzazione di destinazione.

## Pacchetti privati

>[!NOTE]
>
>Per avviare e approvare una richiesta di condivisione e condividere pacchetti tra organizzazioni, è necessario disporre dell&#39;autorizzazione di controllo dell&#39;accesso basata su ruolo **condivisione pacchetti**.

La funzione di strumenti sandbox consente di creare partnership tra organizzazioni, monitorare gli stati di una richiesta di partnership, gestire le partnership esistenti e condividere pacchetti con le organizzazioni partner.

### Creare una richiesta di partnership organizzazione

Per creare una richiesta di partnership organizzazione, passa alla scheda [!UICONTROL Sandbox] **[!UICONTROL Organizzazioni partner]**. Selezionare **[!UICONTROL Gestisci organizzazioni partner]**.

![Interfaccia utente sandbox con le schede Organizzazioni partner e Gestisci organizzazioni partner evidenziate.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Nella finestra di dialogo [!UICONTROL Gestione partner del pacchetto], immetti l&#39;ID organizzazione in **[!UICONTROL Immetti l&#39;ID organizzazione]** e premi Invio. L&#39;ID organizzazione viene visualizzato nella sezione **[!UICONTROL ID organizzazione selezionati]** di seguito. Dopo aver aggiunto gli ID, seleziona **[!UICONTROL Conferma]**.

>[!TIP]
>
>È possibile immettere più ID organizzazione alla volta utilizzando elenchi separati da virgole o immettendo ogni ID organizzazione seguito da INVIO.

![Finestra di dialogo Organizzazioni partner del pacchetto con immissione dell&#39;ID organizzazione, ID organizzazione selezionati e conferma evidenziati.](../images/ui/sandbox-tooling/private-enter-org-id.png)

La richiesta di condivisione è stata inviata all&#39;organizzazione partner e si è tornati alla scheda [!UICONTROL Sandbox] **[!UICONTROL Organizzazioni partner]**, in cui è visualizzata la **[!UICONTROL richiesta in uscita]**.

![Scheda Organizzazioni partner con richiesta in uscita evidenziata.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Autorizzare una richiesta di partnership

Per autorizzare una richiesta di partnership tra organizzazioni, passa alla scheda [!UICONTROL Sandbox] **[!UICONTROL Organizzazioni partner]**. Selezionare **[!UICONTROL Richiesta in ingresso]**.

![L&#39;interfaccia utente delle sandbox con la scheda Organizzazioni partner e la richiesta in ingresso evidenziata.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Il **[!UICONTROL Stato]** corrente per la richiesta è **In sospeso**. Per approvare la richiesta, seleziona i puntini di sospensione (`...`) accanto alla richiesta selezionata, quindi seleziona **[!UICONTROL Approva]** dal menu a discesa.

![Elenco delle richieste in arrivo con il menu a discesa con Approva evidenziato.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

Nella finestra di dialogo **[!UICONTROL Rivedi richiesta organizzazione partner]** sono visualizzati i dettagli relativi alla richiesta di partnership organizzazione. Immetti un [!UICONTROL motivo] per l&#39;approvazione, quindi seleziona **[!UICONTROL Approva]**.

![Finestra di dialogo per la richiesta dell&#39;organizzazione partner di revisione con Motivo e approvazione evidenziati.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Si è tornati alla pagina [!UICONTROL Richiesta in ingresso] e lo stato della richiesta è stato aggiornato a **[!UICONTROL Approvato]**.

![Elenco delle richieste in arrivo con Approvato evidenziato.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Ora puoi condividere i pacchetti tra la tua organizzazione e l’organizzazione di origine.

### Condividere pacchetti con le organizzazioni partner

>[!NOTE]
>
>Solo i pacchetti con lo stato **Pubblicato** possono essere condivisi.

Per condividere un pacchetto con un&#39;organizzazione partner approvata, passare alla scheda [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]**. Selezionare quindi i puntini di sospensione (`...`) accanto al pacchetto, quindi selezionare **[!UICONTROL Condividi pacchetto]** dal menu a discesa.

![Elenco di pacchetti che mostra il menu a discesa con Share package evidenziato.](../images/ui/sandbox-tooling/private-share-package.png)

Nella finestra di dialogo **[!UICONTROL Condividi pacchetto]**, seleziona il pacchetto da condividere dal menu a discesa **[!UICONTROL Condividi impostazioni]**, quindi seleziona **[!UICONTROL Conferma]**.

![Finestra di dialogo Condividi pacchetto con impostazioni di condivisione e Conferma evidenziata.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

>[!TIP]
>
>È possibile selezionare più di un’organizzazione. Le organizzazioni selezionate verranno visualizzate sotto il menu a discesa [!UICONTROL Impostazioni condivisione].

## Passaggi successivi

Questo documento illustra come utilizzare la funzione Strumenti Sandbox per condividere i pacchetti tra diverse organizzazioni. Per ulteriori informazioni, consulta la [guida agli strumenti sandbox](../ui/sandbox-tooling.md).

Per i passaggi relativi all&#39;esecuzione di diverse operazioni tramite l&#39;API Sandbox, consulta la [guida per gli sviluppatori di sandbox](../api/getting-started.md). Per una panoramica di alto livello delle sandbox in Experience Platform, consulta la [documentazione sulla panoramica](../home.md).
