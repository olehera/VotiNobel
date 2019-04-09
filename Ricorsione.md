INPUT: Set di Esame PARTENZA

INPUT: Numero di crediti "m"

OUTPUT: Set di Esame, sottoinsieme di quello di partenza, per cui

	- somma Esame.crediti == m
	- media Esame.voto MAX

Strategia: generare tutti i possibili sottoinsiemi dell'insieme di partenza

# Approccio 1: genero l'insieme decidendo, corso per corso, se esso fa parte dell'insieme

Livello L della ricorsione -> quale corso sto decidendo se includere o meno nell'insieme soluzione

Soluzione parziale -> Un sottoinsieme composto dai corsi tra 0 e L-1.

ESEMPIO: L=4

	soluzione parziale: { 0, 3} 
	soluzione parziale: { 0, 1, 2, 3 }
	soluzione parziale: { }

Generazione del sotto-problema: decidere se inserire Esame[L] oppure no.

	1. Sotto-problema = soluzione parziale (non aggiungo)
	2. Sotto-problema = soluzione parziale + { L }

Casi terminali:

    1. L=max -> non ci sono pi� corsi
       - somma crediti == m => calcola media 
       - somma crediti != m => niente
 	
 	
    2. somma crediti == m
       - valuta la media
       - non genera sotto-problemi
 	
 	
    3. somma crediti > m
       - esce, non genera sotto-problemi
 	
 	
Cosa faccio nel caso terminale?

    1. se somma crediti != m => return ;
    2. se somma crediti == m, valuta media
 
La media � migliore della miglior media conosciuta?

    - s�: soluzione corrente diventa il 'best'
    - no: niente
 		
Complessit�: 2^N

# Approccio 2: ad ogni livello, aggiungo un corso. Devo decidere quale.

Soluzione parziale al livello L: un insieme di L corsi.

Generazione del sotto-problema: aggiungere un nuovo corso all'insieme esistente.
	Per tutti i corsi (i) possibili (non ancora nell'insieme)
	
		- Sotto-problema = parziale + corso(i)

Casi terminali: vedi sopra

Complessit�: N!

ACCORTEZZA: permettere solo sequenze CRESCENTI di esami nella soluzione parziale

Complessit�: 2^N