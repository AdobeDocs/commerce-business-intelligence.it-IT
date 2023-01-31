---
title: Creazione di un dashboard per gli investitori
description: Scopri come creare un dashboard per gli investitori.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Crea dashboard investitori

Molti dei nostri clienti lavorano con gli investitori e hanno bisogno di condividere informazioni da piattaforma con loro, ma i dashboard che si creano per prendere decisioni aziendali quotidiane potrebbero non essere ciò che un investitore cerca. Qui vengono illustrate alcune best practice per la creazione di un dashboard completo ma semplice, ideale per la condivisione con investitori attivi e potenziali.

È necessario creare rapporti per il dashboard dell’investitore:

## Rapporti scalari

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Rapporti visivi

* **[!UICONTROL Revenue by quarter]**
   * Metrica - Ricavi
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Metrica - Ricavo primo ordine
   * Filtro: il numero dell&#39;ordine dell&#39;utente è uguale a 1
   * Metrica 2 - Ricavi da ordine ripetuto
      * Filtro: il numero dell&#39;ordine dell&#39;utente è maggiore di 1
   * Deseleziona la casella per più assi Y
   * Passa a un grafico a colonne sovrapposte
* **[!UICONTROL AOV by quarter]**
   * Metrica 1 - Entrate
      * Nascondi questa metrica
   * Metrica 2 - Numero di ordini
      * Nascondi questa metrica
   * Formula - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Metrica - Ricavi
   * Raggruppa per cliente `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * Metrica - Entrate prodotto
      * Nascondere il grafico
      * Raggruppa per nome del prodotto. Seleziona tutti i prodotti.
      * Imposta l&#39;intervallo di tempo su All-Time
      * Imposta l&#39;intervallo di tempo su Nessuno
      * In &quot;Show top/bottom&quot;, mostra solo i primi 10 ordinati per profitto di prodotto
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Metrica - Acquirenti distinti
      * Prospettiva - Cumulativa
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sessioni

Con un [!DNL Google Analytics] integrazione, puoi includere rapporti su:

* Visite in loco
* Tasso di conversione

Con la [Servizi di arricchimento dei dati di Commerce](https://business.adobe.com/products/magento/magento-commerce.html), puoi includere rapporti su:

* Clienti unici per stato/regione, età, genere.

## Altri suggerimenti

* Utilizzare un linguaggio chiaro e conciso [convenzione di denominazione](../best-practices/naming-elements.md)
* Condividere il dashboard con gli utenti investitori
* Oppure invialo tramite **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Crea un solo dashboard. Questo renderà il contenuto più facile da mantenere, e saprete esattamente cosa stanno guardando i vostri investitori.

Organizza i tuoi report con attenzione e fai attenzione ai dettagli. Una volta completato, il dashboard sarà simile al seguente:

![](../../mbi/assets/investor-dboard-example.png)
