---
title: Gestione utente avanzata
description: Migliora la visibilità dei dati, semplifica le attività di reporting, personalizza l’accesso dei gruppi di utenti, semplifica la condivisione delle dashboard e garantisce sicurezza e scalabilità per la tua organizzazione.
role: Admin, User
feature: User Management
source-git-commit: 42871886d12b97ee52aa270da6f0186a9a4eaddc
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# Gestione utente avanzata

La funzionalità [!DNL Advanced User Management] fornisce controlli di visibilità dei dati migliorati e consente il filtraggio dei dati logici in base ai gruppi di utenti (aree organizzative). Consente di personalizzare la visibilità dei dati in base ai gruppi di utenti ed elimina la necessità di creare una replica delle dashboard esistenti per soddisfare i requisiti di reporting specifici di ogni area ogni volta che l’azienda si espande in una nuova area.

[!DNL Advanced User Management] semplifica la condivisione del dashboard e la visibilità dei dati, garantendo al contempo sicurezza e scalabilità per le organizzazioni di grandi dimensioni. La flessibilità di configurare gruppi di utenti, ruoli e autorizzazioni rende Commerce Intelligence uno strumento potente per i requisiti a livello aziendale.

Con [!DNL Advanced User Management] abilitato, solo gli utenti amministratori hanno accesso alla configurazione dei seguenti elementi:

- Metriche
- Visual Report Builder
- Rapporti basati su SQL
- Riepilogo e-mail
- Esportazioni raw

## Matrice di funzioni

[!DNL Advanced User Management] ha un impatto su diverse funzionalità in Commerce Intelligence. Nella tabella seguente vengono descritte le funzionalità, le autorizzazioni e la loro disponibilità per vari ruoli in base alla funzionalità attivata o disattivata.

<table><thead>
  <tr>
    <th colspan="3" rowspan="2">Funzioni di Commerce Intelligence</th>
    <th colspan="6">Funzioni di Advanced User Management (AUM)</th>
  </tr>
  <tr>
    <th colspan="3">Disabilitato</th>
    <th colspan="3">Abilitato</th>
  </tr></thead>
<tbody>
  <tr>
    <td>Gruppo di funzioni</td>
    <td>Funzionalità</td>
    <td>Autorizzazioni</td>
    <td>Amministratore</td>
    <td>Standard</td>
    <td>Sola lettura</td>
    <td>Amministratore</td>
    <td>Standard</td>
    <td>Sola lettura</td>
  </tr>
  <tr>
    <td rowspan="7">Gestisci utenti (accessibile a tutti gli amministratori e con impatto su tutti i ruoli)</td>
    <td>Configurare i gruppi di utenti</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Invita utente</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Scheda Autorizzazioni - Mappatura dei ruoli</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Scheda Autorizzazioni - Mappatura gruppo utenti (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Scheda Autorizzazioni - Memorizza la mappatura del sottoinsieme (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Scheda Metriche</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Scheda Dashboard condivisi</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Report Builder</td>
    <td>Visual Report Builder</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>SQL REPORT BUILDER</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Riepilogo e-mail</td>
    <td>Creare riepiloghi e-mail senza partizionamento dei dati</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Creare riepiloghi e-mail con partizionamento dei dati (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="4">Dashboard  - Condividi</td>
    <td>Condividere il dashboard con gli utenti tra i ruoli</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Condividi dashboard con gruppi di utenti e amministratori (AUM)</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Dashboard di condivisione - Autorizzazioni</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="18">Dashboard - Visualizza (Apri dashboard condivisa con le autorizzazioni specificate)</td>
    <td rowspan="2">Condividere un dashboard condiviso</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Filtro data (senza flag di funzione EDIT TIME Options)</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Filtro data (con flag di funzione EDIT TIME Options)</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">Filtro store (senza flag di funzione EDIT TIME Options)</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Filtro store (con flag di funzione EDIT TIME Options)</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Dati dashboard: filtrare i dati dei rapporti in base alla mappatura dei gruppi di utenti (AUM)</td>
    <td>Modifica</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">Report - Modifica</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td></td>
    <td></td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td rowspan="2">Esportazione rapporto (CSV, XLSX)</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
    <td>✓</td>
  </tr>
  <tr>
    <td rowspan="2">Rapporto - Esportazione non elaborata</td>
    <td>Modifica</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td>✓</td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Visualizza</td>
    <td>✓</td>
    <td>✓</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody></table>

## Controllo amministratore

Gli utenti amministratori possono gestire le seguenti attività:

- Configurazione dei gruppi di utenti
- Assegna ruolo e gruppo di utenti a singoli utenti
- Condividere dashboard con gruppi di utenti o altri amministratori con autorizzazioni a livello di dashboard
- Pianificare i riepiloghi e-mail con il filtro dei dati a livello di gruppo dell’utente

### Configurare gruppi di utenti

I gruppi di utenti sono raggruppamenti logici di aree mappate a filtri di archivio specifici (ad esempio, gruppi di utenti creati in base ai nomi di continenti, paesi e aree geografiche).

Per configurare i gruppi di utenti:

1. Vai a [!UICONTROL **Gestisci utenti**] > [!UICONTROL **User Groups]** per visualizzare i gruppi di utenti esistenti.

   ![Configurare i gruppi di utenti](../../assets/configure-user-groups.png)

1. [!UICONTROL **Aggiungi gruppo**] consente agli amministratori di creare un nuovo gruppo di utenti:

   - Immettere un nome per il gruppo, ad esempio &quot;Americhe&quot;.

   - Seleziona archivi o filtri rilevanti per il gruppo di utenti.

   - Salva la configurazione.

     ![Aggiungi gruppi di utenti](../../assets/add-group.png)

1. Gli amministratori possono:

   - Modifica i gruppi di utenti per aggiornare le mappature archivio o rinominarle per maggiore chiarezza.

   - Elimina i gruppi di utenti quando non sono più necessari. Gli amministratori devono riassegnare manualmente gli utenti esistenti mappati al gruppo di utenti eliminato.

1. Gruppi predefiniti:

   - [!UICONTROL **None]**: gruppo di fallback per utenti non ancora mappati a un gruppo specifico. Questi utenti non vedranno alcun dato finché non saranno assegnati a un gruppo appropriato.

   - [!UICONTROL **All**]: consente l&#39;accesso illimitato a tutti i dati (in genere riservati agli utenti amministratori).

### Assegnare utenti a gruppi di utenti

Gli amministratori possono mappare nuovi utenti a gruppi rilevanti durante il loro onboarding utilizzando [!UICONTROL **Invita un utente**]. Gli utenti esistenti possono essere rimappati ai gruppi di utenti in base ai requisiti aziendali.

![Assegna utenti a gruppi di utenti](../../assets/assign-users-to-groups.png)

>[!TIP]
>
>- Fino a quando un utente [!UICONTROL **Standard**] o [!UICONTROL **Read-Only**] non sarà assegnato a un gruppo di utenti rilevante, è possibile assegnarlo a [!UICONTROL **None**] per assicurarsi che non acceda erroneamente ai dati del dashboard.
>
>- Durante l’assegnazione delle autorizzazioni a un utente, in base ai requisiti aziendali, è possibile limitare archivi specifici all’interno di un gruppo per un controllo avanzato.

Per impostazione predefinita, gli utenti amministratori sono sempre mappati a [!UICONTROL **Tutti**] archivi, il che consente loro di visualizzare i dashboard con la visualizzazione completa dell&#39;archivio.

### Condividere dashboard

[!DNL Advanced User Management] offre opzioni potenti per la condivisione delle dashboard mantenendo al contempo la sicurezza dei dati.

- Gli amministratori possono condividere le dashboard con i gruppi di utenti e con altri utenti amministratori per collaborare. Ciò consente la gestione centralizzata delle dashboard e semplifica la gestione per le grandi organizzazioni.

  ![Condividi dashboard](../../assets/share-dashboards.png)

- Le autorizzazioni di condivisione del dashboard includono:

   - [!UICONTROL **Modifica**]: disponibile solo per gli utenti amministratori che possono modificare dashboard, filtrare dati, modificare report o esportare dati.

   - [!UICONTROL **Visualizzazione**]: disponibile per gli utenti in tutti i ruoli con (alcune limitazioni).

   - [!UICONTROL **Nessuno**]: revoca l&#39;accesso al dashboard per determinati gruppi di utenti o amministratori.

  >[!NOTE]
  >
  >Per informazioni sulle varie combinazioni, consulta la [matrice delle funzionalità](#feature-matrix) per informazioni sull&#39;usabilità delle varie funzionalità di Commerce Intelligence in base alle autorizzazioni della regola e del dashboard.

#### Visualizzazioni del dashboard

Gli utenti amministratori possono visualizzare i dati del dashboard con accesso a tutti gli store.

![Visualizza amministratore dashboard](../../assets/view-dashboard-admin.png)

Tuttavia, gli utenti possono visualizzare i dati del dashboard filtrati in base agli store mappati a loro durante la configurazione utente.

![Visualizza amministratore dashboard](../../assets/view-dashboard-user.png)

>[!TIP]
>
>Gli amministratori possono abilitare i filtri delle date per le dashboard condivise, consentendo agli utenti di visualizzare i dati su intervalli di date diversi invece dell’intervallo di tempo predefinito impostato durante la creazione del rapporto. Questa funzione può essere attivata o disattivata in base alle esigenze aziendali.

### Pianificare i riepiloghi delle e-mail

[!DNL Advanced User Management] estende le funzionalità di filtro dei dati ai riepiloghi delle e-mail. A seconda del pubblico, gli utenti amministratori possono specificare i gruppi di utenti per i quali devono essere filtrati i rapporti selezionati.

![Riepilogo e-mail pianificato](../../assets/schedule-email-summary.png)
