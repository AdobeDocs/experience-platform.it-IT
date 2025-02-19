---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC;;home;popular topic;access control;attribute-based access control;ABAC
title: Gestire i criteri di controllo di accesso
description: Questo documento fornisce informazioni sulla gestione dei criteri di controllo di accesso tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: afd883c530ab1b335888e79b5f4075e774fced4b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

# Gestire i criteri di controllo dell’accesso

I criteri di controllo degli accessi sono istruzioni che riuniscono attributi per stabilire azioni consentite e inammissibili. I criteri di accesso possono essere locali o globali e possono ignorare altri criteri. Adobe fornisce una policy predefinita che può essere attivata immediatamente o ogni volta che l’organizzazione è pronta per iniziare a controllare l’accesso a oggetti specifici in base alle etichette. Il criterio predefinito sfrutta le etichette applicate alle risorse per negare l’accesso, a meno che gli utenti non abbiano un ruolo con un’etichetta corrispondente.

>[!IMPORTANT]
>
>I criteri di accesso non devono essere confusi con i criteri di utilizzo dei dati, che controllano il modo in cui i dati vengono utilizzati in Adobe Experience Platform anziché gli utenti dell’organizzazione che vi hanno accesso. Per ulteriori informazioni, consulta la guida sulla creazione di [criteri di utilizzo dei dati](../../../data-governance/policies/create.md).

<!-- ## Create a new policy

To create a new policy, select the **[!UICONTROL Policies]** tab in the sidebar and select **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** dialog appears, prompting you to enter a name, and an optional description. When finished, select **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Using the dropdown arrow select if you would like to **Permit access to** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png)) a resource or **Deny access to** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) a resource.

Next, select the resource that you would like to include in the policy using the dropdown menu and search access type, read or write.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Next, using the dropdown arrow select the condition you would like to apply to this policy, **The following being true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) or **The following being false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Select the plus icon to **Add matches expression** or **Add expression group** for the resource. 

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Using the dropdown, select the **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Next, using the dropdown select the **Matches**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Next, using the dropdown, select the type of label (**[!UICONTROL Core label]** or **[!UICONTROL Custom label]**) to match the label assigned to the User in roles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finally, select the **Sandbox** that you would like the policy conditions to apply to, using the dropdown menu.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Add resource** to add more resources. Once finished, select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The new policy is successfully created, and you are redirected to the **[!UICONTROL Policies]** tab, where you will see the newly created policy appear in the list. 

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Edit a policy

To edit an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to the policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select edit from the dropdown.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

The policy permissions screen appears. Make the updates then select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The policy is successfully updated, and you are redirected to the **[!UICONTROL Policies]** tab.

## Duplicate a policy

To duplicate an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select duplicate from the dropdown.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** dialog appears, prompting you to confirm the duplication. 

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

The new policy appears in the list as a copy of the original on the **[!UICONTROL Policies]** tab.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Delete a policy

To delete an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to delete.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select delete from the dropdown.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** dialog appears, prompting you to confirm the deletion. 

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

You are returned to the **[!UICONTROL policies]** tab and a confirmation of deletion pop over appears.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png) -->

## Configurare i criteri per una sandbox

>[!IMPORTANT]
>
>Per impostazione predefinita, la funzione [!UICONTROL Inclusione automatica] è attivata per tutti i clienti, il che significa che tutte le sandbox sono aggiunte al criterio.

>[!NOTE]
>
>Il criterio **[!UICONTROL Default-Label-Based-Access-Control-Policy]** è attualmente l&#39;unico disponibile per la configurazione.

Per visualizzare le sandbox associate a un criterio, seleziona il criterio dalla scheda **[!UICONTROL Criteri]**.

![La pagina dei criteri mostra un elenco dei criteri esistenti disponibili.](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Quindi, seleziona il criterio, quindi seleziona la scheda **[!UICONTROL Sandbox]**. Viene visualizzato un elenco di sandbox associate al criterio.

![La pagina dei criteri mostra un elenco dei criteri esistenti disponibili.](../../images/flac-ui/abac-policies-sandboxes-tab.png)

### Aggiungi criterio a tutte le sandbox

Utilizza l&#39;interruttore **[!UICONTROL Inclusione automatica]** nella scheda **[!UICONTROL Sandbox]** per attivare i criteri per tutte le sandbox.

![La scheda [!UICONTROL Sandbox] mostra l&#39;interruttore [!UICONTROL Inclusione automatica].](../../images/flac-ui/abac-policies-auto-include.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Abilita inclusione automatica]** in cui viene richiesto di confermare la selezione. Seleziona **[!UICONTROL Abilita]** per completare l&#39;impostazione di configurazione.

![La finestra di dialogo [!UICONTROL Attiva inclusione automatica] evidenzia [!UICONTROL Attiva].](../../images/flac-ui/abac-policies-auto-include-enable.png)

>[!SUCCESS]
>
>Il criterio viene attivato per tutte le sandbox esistenti e verrà aggiunto automaticamente a tutte le nuove sandbox quando saranno disponibili.

### Aggiungi criterio per selezionare sandbox

>[!IMPORTANT]
>
>Le sandbox future non saranno incluse nel criterio per impostazione predefinita se l&#39;opzione [!UICONTROL Inclusione automatica] è disattivata. Sarà necessario gestire e aggiungere manualmente le sandbox al criterio.

Utilizza l&#39;interruttore **[!UICONTROL Inclusione automatica]** nella scheda **[!UICONTROL Sandbox]** per disabilitare i criteri per tutte le sandbox.

![La scheda [!UICONTROL Sandbox] mostra l&#39;interruttore [!UICONTROL Inclusione automatica].](../../images/flac-ui/abac-policies-auto-include.png)

Dalla scheda **[!UICONTROL Sandbox]**, seleziona **[!UICONTROL Aggiungi sandbox]** per selezionare le sandbox a cui verrà applicato questo criterio.

![La scheda [!UICONTROL Sandbox] mostra un elenco di sandbox aggiunte al criterio.](../../images/flac-ui/abac-policies-sandboxes-tab-add.png)

Viene visualizzato un elenco di sandbox. Seleziona la sandbox da aggiungere dall’elenco. In alternativa, utilizza la barra di ricerca per cercare la sandbox. Seleziona **[!UICONTROL Salva]**.

![Pagina [!UICONTROL Aggiungi sandbox] contenente l&#39;elenco delle sandbox esistenti disponibili da aggiungere ai criteri.](../../images/flac-ui/abac-policies-sandboxes-list.png)

>[!SUCCESS]
>
>Le sandbox selezionate sono state aggiunte correttamente al criterio.

### Rimuovere le sandbox da un criterio

Per rimuovere una sandbox, seleziona l&#39;icona **X** accanto al nome della sandbox.

![La scheda [!UICONTROL Sandbox] mostra un elenco di sandbox ed evidenzia le [!UICONTROL X] da eliminare.](../../images/flac-ui/abac-policies-remove-sandbox-x.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Rimuovi]** in cui viene richiesto di confermare la selezione. Seleziona **[!UICONTROL Conferma]** per completare la rimozione.

![La finestra di dialogo [!UICONTROL Rimuovi] evidenzia [!UICONTROL Conferma].](../../images/flac-ui/abac-policies-remove-sandbox.png)

>[!SUCCESS]
>
>La sandbox selezionata è stata rimossa correttamente dal criterio.

## Attivare un criterio {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Cosa sono i criteri?"
>abstract="I criteri sono dichiarazioni che riuniscono alcuni attributi al fine di definire azioni ammissibili e non ammissibili. Ogni organizzazione viene fornita con una policy predefinita che è necessario attivare per iniziare a controllare l’accesso a oggetti specifici in base alle etichette. Le etichette applicate alle risorse negano l’accesso a meno che gli utenti non siano assegnati a un ruolo con un’etichetta corrispondente. Non è possibile modificare o eliminare i criteri predefiniti, ma è possibile attivarli o disattivarli."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Gestisci etichette"

Per attivare un criterio esistente, selezionarlo dalla scheda **[!UICONTROL Criteri]**.

![flac-policy-select](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Quindi, selezionare i puntini di sospensione (`…`) accanto al nome di un criterio e un menu a discesa visualizza i controlli per modificare, attivare, eliminare o duplicare il ruolo. Seleziona attiva dal menu a discesa.

![flac-policy-activate](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Attiva criterio]** in cui viene richiesto di confermare l&#39;attivazione.

![flac-policy-activate-confirm](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


Sei tornato alla scheda **[!UICONTROL criteri]** e viene visualizzata una conferma del pop-over di attivazione. Lo stato del criterio viene visualizzato come attivo.

![flac-policy-enabled](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## Passaggi successivi

Attivando un criterio, puoi passare al passaggio successivo per [gestire le autorizzazioni per un ruolo](permissions.md).
