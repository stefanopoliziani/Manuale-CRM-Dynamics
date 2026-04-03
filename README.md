flowchart TD
    %% Nodi di avvio
    Start(Avvio Processo Aziendale) --> Origine{Qual è l'origine della Trattativa?}
    
    %% Ramo Marketing / BDC
    Origine -->|Generata dal Marketing| PrimoContatto[BDC: Effettua primo contatto / Telemarketing]
    PrimoContatto --> Qualifica{Il Lead è Qualificato?}
    
    Qualifica -->|NO| ChiudiLead[BDC: Imposta Lead come 'Non Qualificato' e specifica il motivo]
    Qualifica -->|SI| CreaRecord[BDC: Converte Lead e crea Account, Contatto, Opportunità]
    CreaRecord --> Assegna[BDC: Assegna Trattativa al Venditore in base al CAP]
    Assegna --> Avviso[BDC: Invia E-mail al Venditore e al Responsabile]
    Avviso --> PresaInCarico[Venditore: Prende in carico la Trattativa]
    
    %% Ramo Autogenerato
    Origine -->|Autogenerata dal Venditore| CreaTrattativaVenditore[Venditore: Crea manualmente la Trattativa in CRM]
    CreaTrattativaVenditore --> PresaInCarico
    
    %% Gestione Trattativa
    PresaInCarico --> Esplora[Venditore: Chiama il cliente, fissa appuntamento ed esplora le esigenze]
    Esplora --> Registra[Venditore: Registra attività in CRM - Telefonata / Appuntamento]
    
    %% Gestione Permute
    Registra --> Permuta{Il cliente ha un usato da permutare?}
    
    Permuta -->|SI| AddPermuta[Venditore: Inserisce Permuta nella Trattativa]
    AddPermuta --> StatoUso[Venditore: Compila lo 'Stato d'Uso']
    StatoUso --> Valutazione[Responsabile Usato: Valuta la permuta]
    Valutazione --> Preventivo
    
    Permuta -->|NO| Preventivo[Venditore: Genera Preventivo via listino elettronico collegato]
    
    %% Follow-up e Chiusura
    Preventivo --> VerificaFollowUp{Origine della Trattativa?}
    
    VerificaFollowUp -->|Generata dal Marketing| RecallBDC[BDC: Avvia ciclo di Recall a 4gg, 1 mese e 2 mesi]
    RecallBDC --> Chiusura
    
    VerificaFollowUp -->|Autogenerata dal Venditore| FollowUpAutonomo[Venditore: Esegue il follow-up in autonomia]
    FollowUpAutonomo --> Chiusura
    
    Chiusura[Chiusura della Trattativa: Registra esito Vinta/Persa]
    
    %% Stili
    style Origine fill:#f9f,stroke:#333,stroke-width:2px
    style Qualifica fill:#f9f,stroke:#333,stroke-width:2px
    style Permuta fill:#f9f,stroke:#333,stroke-width:2px
    style VerificaFollowUp fill:#f9f,stroke:#333,stroke-width:2px
