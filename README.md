                                                          #Mini Database
                                                          
#Nume: Soare Ion-Alexandru
#Serie si grupa: CD 323
#Profesor coordonator: Tudor Berariu
#Tema 1: Mini Database (Racket)

Structura temei:

	Baza de date constituie o lista de tabele (care la randul lor sunt liste). Fiecare
tabela este si ea o lista, ce contine pe prima pozitie numele acesteia, iar pe urmatoarele
coloanele sale. De asemenea, fiecare coloana contine numele acesteia pe prima pozitie, fiind
urmata de elementele ce definesc campul respectiv. Valorile sunt puse pe categorii (coloane,
atribute), si nu pe membru. Exemplu: o coloana va stoca numele tuturor participantilor
'("Nume" "Ion" "Danut" "Petru") si nu atributele unei singure inregistrari.

Ex 1:

	init-database -> lista nula;
	create-table -> functia create-columns creeaza o lista cu toate coloanele (numele lor),
					urmand sa ii fie adaugat numele la inceput in create-table;
	get-name -> primul element din tabela;
	get-columns -> returneaza numele tuturor coloanelor dintr-o tabela;
	get-tables -> initial gandita sa intoarca doar numele tabelelor, checker-ul a fortat-o
				  sa returneze chiar baza de date, db, intrucat ea este multimea tabelelor;
	get-table -> verifica prin toate tabelele si-l returneaza pe cel cu numele bun;
	add-table -> append la baza de date tabela data;
	remove-table -> intrucat nu poate exista stergere propriu-zisa, se va pastra in acumulator
					tot in afara de tabela pe care o vrem stearsa;

	*am folosit pe cat de mult posibil recursivitate pe coada si cons in loc de append, atat
	in prima parte a temei (Ex 1), cat si mai departe (de aceea prezenta multor functii auxi-
	liare, pentru folosirea acumulatorilor*

Ex 2:

	*stiu ca numele nu sunt chiar sugestive most of the time, dar le-am folosit in mai multe
	locuri si voi detalia input-urile si output-urile detaliat mai jos*

	ret-coloana-buna -> primeste o pereche de tipul (nume coloana . valoare) si o tabela si
						va returna coloana din tabel cu numele indicat de pereche (nu se folo-
						seste valoarea, insa a fost mai usor sa fie dat ca parametru direct
						perechea);
	splash-record -> primeste lista de perechi (record) si un acumulator (setat pe null initial),
					 pentru ulterioarele stocari, si returneaza o lista cu numele tuturor coloanelor;

	*fiecare acumulator de tip acc va fi initializat cu null, iar fiecare acumulator de tip acc-number
	va fi initializat cu 0, pentru a scuti de explicarea fiecaruia in cadrul functiilor auxiliar*

	col-cu-null -> primeste record si tabela fara nume, si returneaza o lista cu coloanele care
				   nu isi regasesc numele in lista record, carora li se adauga deja null la final;
				   practic, coloanele pe care trebuie sa adaugam null;
	column-preluc -> primeste record si tabela fara nume si returneaza o lista cu toate coloanele
					 prelucrate deja; practic, se creeaza iar tabela, fara sa i se puna numele
					 la inceput, bazandu-ne pe functiile discutate mai sus;

	*in column-preluc-aux, precum si in alte functii la alte cerinte, s-au facut verificari daca
	perechile au fost date de tipul '(a . b) sau (a . b), intrucat reactionau diferit in functie
	de situatie; astfel, se putea returna dupa o serie de comenzi cdr/car in loc de primul element
	din pereche, simbolul 'quote si de aceea au fost facute verificarile cu equal? 'quote*

	table-finder -> strict de modularizare si de observare a codului mai bine, doar pune numele
					la inceputul a ceea ce a facut deja column-preluc;
	insert -> va avea baza de date din carte sterge tabela si va adauga in ea prelucrarea facuta
			prin functiile explicate mai sus;

Ex 3:

	ret-coloana-buna2 -> primeste o tabela fara numele ei si un nume de coloana si va returna
						 coloana cu numele dat ca parametru; a fost denumita asa intrucat
						 functionalitatea seamana cu cea de la ret-coloana-buna, insa e mai
						 generala;
	simple-select -> recursiv pe coada, ca pana acum, cu mici specificatii adaugate prin comentarii
					 in cod;

Ex 4:

	min, avg... -> functiile definite datorita necesitatii de utilizare in tema; acestea vor fi uti-
				   lizate cu quote ('min) prin intermediul unui cond intr-o functie posterioara;
	return-right-column -> aplica functia data pe coloana sau, daca nu exista, o returneaza fara nume;
	return-all-right-columns -> un return-right-column pentru fiecare coloana;
	keep-right-table -> primeste tabela si conditiile si va returna o tabela ce contine doar ce satis-
						face conditiile date, ca pe urma sa fie aplicate operatiile pe ele;
	keep-right -> pastreaza doar dintr-o coloana pe care o specificam, pastreaza pozitiile tale din
				  lista positions;
	return-position -> returneaza pozitiile dintr-o tabela care satisfac conditiile date (toate condi-
						tiile trebuie satisfacute pentru a fi introdus in tabela);

Ex 5:

	update-all-columns -> updateaza toate coloanele dintr-o baza de date;
	return-position-list -> returneaza lista de pozitii dintr-o dabela care se respecta in urma conditiilor
							date;
	return-common-dual -> returneaza pozitiile comune dintre doua lista de pozitii, practic intersectia a 2
						  multimi;
	return-common-full -> returneaza pozitiile comune dintre toate listele returnate la position-list;
						  intersectia a n multimi;
	update-helper -> imbina update-all-columns cu pozitiile returnate din return-common-full de return-position-
					 list;
	missing-columns -> alatura coloanele updatate si pe cele care nu dispun de update laolalta;
	update -> merge ca pe mecanismul de pana acum, intrucat nu putem sterge propriu-zis ceva din baza de date,
			  vom returna o baza de date fara tabela pe care vrem sa o prelucram, la care adaugam tabela pre-
			  lucrata.

Ex 6:

	delete-column -> returneaza coloana cu pozitiile care nu apar in lista positions; astfel, daca lista positions
					 contine elementele (1 2) dintr-un total de (0 1 2 3 4), se vor pastra doar elementele (0 3 4)
					 din lista/coloana;
	delete-all-columns -> aplica acelasi procedeu de mai sus, insa pe o intreaga tabela, aplicand pe fiecare coloana;
	keep-right-table -> pastreaza din tabela doar inregistrarile ce satisfac conditiile;


