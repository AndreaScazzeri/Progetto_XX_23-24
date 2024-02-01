# Progetto_Stratified_Shuffle_Split_23-24
### Corso di Programmazione e Metodi Sperimentali per l'Intelligenza Artificiale.
Componenti del gruppo:
* Andrea Scazzeri
* Edoardo Giacometto
* Mattia Muraro

Si intende implementare un toolbox che mediante una pipeline permetta all'utente di utilizzare il ***k-Nearest-Neighbor***
(kNN) specificandone i parametri. La pipeline includerà i seguenti step:
1. *Lettura dei dati* - si eseguirà la lettura da un file .csv ma sarebbe opportuno estendere l'implementazione
anche ad altri tipi di file magari sfruttando il pattern strategy insieme al factory.
2. *Pre-Processing*
    + Gestione dei dati mancanti - vengono eliminati i record con almeno un valore mancante
    + Divisione delle feature - il dataset viene diviso in variabili indipendenti e predizioni
    + Feature scaling - si utilizza il pattern strategy per lasciare all'utente la possibilità 
    di usare la normalizzazione o la standardizzazione
3. *Splitting del dataset* - Le techiche di splitting che vengono implementate in questo progetto sono: **Holdout** e **Stratified Shuffle Split**. 
    Si utilizza il pattern factory insieme al pattern strategy per rendere il codice aperto all'ipotetica nuova aggiunta di altri metodi di splitting
4. *kNN* - è la classe cuore del progetto. Ricevendo in ingresso i data set di train e test fornisce la classificazione del test
5. *Calcolo delle metriche* - si utilizza il pattern strategy per calcolare le metriche, lasciando all'utente la possibilità di scegliere quale calcolare
6. *Mostrare i risultati* - la visualizzazione dei risultati dipende da come l'utente ha scelto di dividere il trainset e il testset:
   + Nel caso di **Holdout** sarà visualizzabile solo una tabella che contiene le performance del modello per quella scelta di train e test set
   + Nel caso di **Stratified Shuffle Split** sarà possibile visualizzare, oltre ad una tabella contenente le performance come nel caso di holdout,
    anche un grafico che mostra l'andamento delle performance per ogni ripetizione di splitting e un boxplot che mostra
    la distribuzione delle performance negli esperimenti.

## Come utilizzare il toolbox

Per utilizzare il toolbox è necessario importare la classe `KNNPipeline` e creare un'istanza della classe specificando i seguenti parametri:
* `path` - il percorso del file .csv contenente il dataset su cui fare il training e il testing
* `fs` - il tipo di feature scaling da utilizzare. Può essere `norm` (normalizzazione) o `stand` (standardizzazione - default)
* `splitting_type` - il tipo di splitting da utilizzare. Può essere `holdout` (default) o `sss` (Stratified Shuffle Split) 
* `parametro_splitting` - la percentuale di test set da utilizzare (default 0.2)
* `n_divisioni` - il numero di esperimenti da eseguire nel caso il metodo di splitting è lo Stratified Shuffle Split 
da eseguire (default 5)
* `k` - il numero di vicini da considerare per la classificazione (default 7)
* `ar` - indica se si vuole calcolare l'accuracy rate (default False)
* `er` - indica se si vuole calcolare l'error rate (default False)
* `sens` - indica se si vuole calcolare la sensitivity (default False)
* `spec` - indica se si vuole calcolare la specificity (default False)
* `gm` - indica se si vuole calcolare la geometric mean (default False)
* `all_metrics` - indica se si vogliono calcolare tutte le metriche (default True)
* `seed` - indica il seed da utilizzare per la divisione del dataset (default None)
* `show_boxplot` - indica se si vuole visualizzare il boxplot delle performance (default False)
* `show_lineplot` - indica se si vuole visualizzare il lineplot boxplot delle performance (default False)
* `show_table` - indica se si vuole visualizzare la tabella boxplot delle performance (default True)

*ATTENZIONE* - se si decide di visualizzare il boxplot, il lineplot o la teabella delle performance essi verrano anche 
salvati in una sottocartella della current directory chiamata `Plots` (che deve esistere)