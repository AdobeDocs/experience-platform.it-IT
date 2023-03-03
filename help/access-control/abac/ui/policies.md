---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC
title: Gestire i criteri di controllo di accesso
description: Questo documento fornisce informazioni sulla gestione dei criteri di controllo di accesso tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 504c73fc73ce41f2c1b3159478fc7fe9b4d20a9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Gestire i criteri di controllo dell’accesso

I criteri di controllo degli accessi sono istruzioni che riuniscono attributi per stabilire azioni consentite e inammissibili. I criteri di accesso possono essere locali o globali e possono ignorare altri criteri. Adobe fornisce una policy predefinita che può essere attivata immediatamente o ogni volta che l’organizzazione è pronta per iniziare a controllare l’accesso a oggetti specifici in base alle etichette. Il criterio predefinito sfrutta le etichette applicate alle risorse per negare l’accesso, a meno che gli utenti non abbiano un ruolo con un’etichetta corrispondente.

>[!IMPORTANT]
>
>I criteri di accesso non devono essere confusi con i criteri di utilizzo dei dati, che controllano il modo in cui i dati vengono utilizzati in Adobe Experience Platform anziché gli utenti dell’organizzazione che vi hanno accesso. Consulta la guida alla creazione di [criteri di utilizzo dati](../../../data-governance/policies/create.md) per ulteriori informazioni.

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

## Attivare un criterio

Per attivare un criterio esistente, selezionalo da **[!UICONTROL Criteri]** scheda.

![flac-policy-select](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Quindi, seleziona i puntini di sospensione (`…`) accanto al nome di un criterio e un menu a discesa visualizza i controlli per modificare, attivare, eliminare o duplicare il ruolo. Seleziona attiva dal menu a discesa.

![flac-policy-activate](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Il **[!UICONTROL Attiva criterio]** viene visualizzata una finestra di dialogo che richiede di confermare l&#39;attivazione.

![flac-policy-activate-confirm](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


Viene visualizzata di nuovo la **[!UICONTROL criteri]** e viene visualizzata una conferma del pop-over di attivazione. Lo stato del criterio viene visualizzato come attivo.

![flac-policy-enabled](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## Passaggi successivi

Attivando un criterio, puoi procedere al passaggio successivo per [gestire le autorizzazioni per un ruolo](permissions.md).
