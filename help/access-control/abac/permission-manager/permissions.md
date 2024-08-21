---
title: Gestione delle autorizzazioni di controllo degli accessi basato su attributi
description: Scopri come utilizzare Gestione autorizzazioni in Adobe Experience Platform per generare rapporti e convalidare le autorizzazioni di accesso.
source-git-commit: 3f2a899705d2c05b12300b6d5b0b860ad2c05bfd
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# Gestione autorizzazioni

>[!NOTE]
>
>Per accedere a [!UICONTROL Gestione autorizzazioni], è necessario essere un amministratore di prodotto. Se non disponi dei privilegi di amministratore, contatta l’amministratore di sistema per ottenere l’accesso.

Utilizza query semplici in [!UICONTROL Gestione autorizzazioni] per creare rapporti concisi che ti aiuteranno a comprendere la gestione degli accessi e a risparmiare tempo nella convalida delle autorizzazioni di accesso in molti flussi di lavoro e livelli di granularità. È possibile utilizzare [!UICONTROL Gestione autorizzazioni] per trovare gli utenti che appartengono a un gruppo di utenti e dispongono dei privilegi di accesso specificati, nonché i ruoli con etichette specifiche.

## Eseguire una ricerca di utenti all&#39;interno di un gruppo di utenti specificato {#search-users}

>[!CONTEXTUALHELP]
>id="platform_permission_manager"
>title="Gestione autorizzazioni"
>abstract="Utilizza i selettori a discesa nella pagina per ottenere rapporti sul livello di accesso di diversi livelli di granularità per utenti e ruoli."
<!-- >additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-manager/permissions.html" text="Permission manager" -->

Utilizzando il menu a discesa, selezionare l&#39;attributo **[!UICONTROL Utenti]**.

![Elenco a discesa degli attributi che evidenzia gli utenti.](../../images/permission-manager/users-select.png)

Selezionare quindi il **[!UICONTROL gruppo utenti]** che si desidera cercare utilizzando il menu a discesa.

>[!INFO]
>
>[!UICONTROL Il gruppo utenti] non è un campo obbligatorio. Puoi selezionare un solo gruppo di utenti per ogni rapporto.

![Elenco a discesa Gruppo utenti evidenziato.](../../images/permission-manager/user-group-select.png)

Per un rapporto più granulare, puoi specificare la risorsa con le azioni in una particolare sandbox. Seleziona **[!UICONTROL Risorsa]**, **[!UICONTROL Azioni]** e **[!UICONTROL Sandbox]** dal menu a discesa, quindi seleziona **[!UICONTROL Mostra risultati]**.

>[!INFO]
>
>[!UICONTROL Risorsa], [!UICONTROL Azioni] e [!UICONTROL Sandbox] non sono campi obbligatori. È possibile selezionare una sola [!UICONTROL risorsa] per ogni report. Una volta aggiunta, è possibile rimuovere un&#39;azione o una sandbox selezionando **&#39;x&#39;** accanto alla selezione da rimuovere.

![Risorse, azioni, sandbox ed evidenziazione dei risultati](../../images/permission-manager/users-additional-attributes-select.png)

Un elenco di utenti e il loro indirizzo e-mail vengono segnalati in base ai criteri selezionati. Utilizza il menu dei filtri a sinistra per aggiornare gli attributi e i risultati. Per ulteriori informazioni su un utente specifico, selezionare il nome utente dall&#39;elenco.

![Report generato in base agli attributi selezionati evidenziati](../../images/permission-manager/users-report.png)

## Cerca ruoli con etichette specifiche {#search-roles}

Utilizzando il menu a discesa, seleziona l&#39;attributo **[!UICONTROL Ruoli]**.

>[!INFO]
>
>[!UICONTROL Etichette] non è un campo obbligatorio. Puoi selezionare più etichette, che verranno elencate sotto questo elenco a discesa una volta selezionate. Una volta aggiunta, è possibile rimuovere un&#39;etichetta selezionando **&#39;x&#39;** accanto all&#39;azione.

![L&#39;elenco a discesa degli attributi evidenzia i ruoli.](../../images/permission-manager/roles-select.png)

Quindi, seleziona le **[!UICONTROL etichette]** che desideri cercare utilizzando il menu a discesa.

![Elenco a discesa Etichette evidenziato.](../../images/permission-manager/roles-labels-select.png)

Per un rapporto più granulare, puoi specificare la risorsa con le azioni in una particolare sandbox. Seleziona **[!UICONTROL Risorsa]**, **[!UICONTROL Azioni]** e **[!UICONTROL Sandbox]** dal menu a discesa, quindi seleziona **[!UICONTROL Mostra risultati]**.

>[!INFO]
>
>[!UICONTROL Risorsa], [!UICONTROL Azioni] e [!UICONTROL Sandbox] non sono campi obbligatori. È possibile selezionare una sola [!UICONTROL risorsa] per ogni report. Una volta aggiunta, è possibile rimuovere un&#39;azione o una sandbox selezionando **&#39;x&#39;** accanto alla selezione da rimuovere.

![Risorse, azioni, sandbox ed evidenziazione dei risultati](../../images/permission-manager/roles-additional-attributes-select.png)

Viene segnalato un elenco di ruoli in base ai criteri selezionati. Utilizza il menu dei filtri a sinistra per aggiornare gli attributi e i risultati. Per ulteriori informazioni su un ruolo specifico, selezionarlo dall&#39;elenco.

Per ogni ruolo corrispondente ai criteri specificati vengono visualizzate le seguenti informazioni:

| Attributo | Descrizione |
| --- | --- |
| Descrizione | Breve descrizione del ruolo. |
| Etichette | Elenco di etichette associate al ruolo. |
| Sandbox | Un elenco di Sanbox contenenti questo ruolo. |
| Modificato | La data e la marca temporale dell’ultimo aggiornamento del ruolo. |
| Creato a | La data e la marca temporale di creazione del ruolo. |
| Creato da | Dettagli del creatore del ruolo. |

![Report generato in base agli attributi selezionati evidenziati](../../images/permission-manager/roles-report.png)

## Passaggi successivi

Ora hai imparato a generare rapporti per utenti e ruoli. Per ulteriori informazioni sul controllo degli accessi basato su attributi, vedere la [panoramica sul controllo degli accessi basato su attributi](../overview.md).
