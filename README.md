# Reumatoïde Artritis RNA-sequencing

![RNA_sequencing_voorpagina](https://github.com/user-attachments/assets/23f3beed-82b0-4c4d-8ba2-09fd2fb2538e)

# Inleiding
Reumatoïde artritis(RA) staat bekend als een chronische inflammatoire  multisystemische auto-immuunziekte, het afweersysteem keert tegen het lichaam. Normaliter breekt en voert ziekteverwekkers af met dit afweer systeem, beschermt het lichaam. De onderliggende oorzaak is onbekend, echter een deel van de meespelende factoren wel. Tumornecrosefactor (TNF-α)  en interleukine 6(IL-6) zijn cytokines(onderdeel van het immuunsysteem) wat zorgt voor de communicatie tussen de cellen. (https://pubmed.ncbi.nlm.nih.gov/39894627/) TNF-α en IL-6 onder houden gewrichten en* treden op  wanneer er sprake is van ontsteking door RA.(https://pubmed.ncbi.nlm.nih.gov/30098882/) Bij RA  verstijven en zwellen de gewrichten op wat kan leidden tot ontstekingen. hierdoor ontstaan pijnklachten en mettertijd kunnen de botten en het kraakbeen beschadigen. ((https://pubmed.ncbi.nlm.nih.gov/39894627/) Vroege diagnose voorkomt lange termijn klachten. (https://pubmed.ncbi.nlm.nih.gov/37567824/). Met gebruik van RNA-sequencing kan data worden vergeleken met klachten en ziektemechanismen voor een vroege diagnose. Het onderzoek omvat data van een eerder uitgevoerd onderzoek(Platzer et al., 2019). De 8 sampels van het weefsel van het gewrichtsslijmvlies, waaronder 4 gezonde patiënten en 4 samples van patiënten met vastgestelde RA van minimaal 12 maanden. 

# Inhoud
hier komt nog een inhoudsopgave
# Methode
![Flowchart transcriptomics](https://github.com/user-attachments/assets/78a4b920-9831-4a8c-9164-b5b19c814288)
script verwijzing?
Doormiddel van transcriptomics, RNA-sequencing, wordt RA vroegtijdig aangetoond. Het humane genoom werd als vergelijkingsdata gebruikt, deze data is uit het sequence read archive  van NCBI gehaald. (bron). De "bioconducter" package is specifiek ontwikkeld voor analyses van biologische data, RNA-seq. Om deze verschillende functies te  gebruiken is de "BiocManager"(versienummer) package nog nodig. Door het genoom te indexeren kon het align-programma specifiek zoeken in deze data. Deze reads werden gemapt tegen het referentie genoom , waar gesorteerde BAM bestanden uit komen.  Deze bestanden worden gebruikt om de genexpressie te tellen. BAM staat voor Binary alignment/map. Waarna de count matrix is gemaakt doormiddel van de "readr, dplyr,Rsamtools,Rsubread"(versienummers)packages. In een count matrix staat per gen hoeveel reads er op dat gen zijn gemapt. GFF? De matrix wordt bewekrt? Met een bewerkte matrix wordt er verschil gemaakt tussen de RA en gezonde patiënten data("DESeq2, KREGGEST"packages)(versienummers). DESeqDataSet object aangemaakt met deze data, wat de ruwe counts normaliseert en een differentiele expressie-analyse uitvoert, waaruit de significante resultaten gesorteerd wordt. Deze data werd gevisualiseerd(EnhancedVolcano package) in een vulkaanplot. Met een bias-analyse wordt de genlengte beperkt, waarmee een Go-analyse wordt uitgevoerd. Uit de go-analyse zijn significante functies van de genen te bepalen. Bij deze RA-casus is de antigen binding functie (hsa04612), waarmee een Kegg-(pathaway)analyse is uitgevoerd, om te concluderen waar en hoe deze functies invloed hebben op het ziektebeeld.
kegg analyse verwijzing?

# Resultaten
Om een diagnose te stellen zijn resultaten vereist, doormiddel van visualisatie zijn verschillen duidelijker zichtbaar.
[Vulkaanplot](https://github.com/savvdzwld/casus-transcriptomics/blob/main/resultaten/Vulkaanplot.png)
Met een vulkaanplot wordt gevisualiseerd hoeveel de genexpressie van specifieke genen significant verandert. Op de x-as de mate van verandering in expressie, en op de y-as de significantie van deze verandering. Hoe hoger de waarde,blauw gekleurd, des te significanter. ANKRD30BL in het groen is een van  de significante genen met veranderingen van beide, deze functies kunnen samenhangen. Van deze samenhang is een bias-analyse uitgevoerd in differentieel geëxprimeerd(DE) data.
[Bias-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/resultaten/pwf.png)
Hierin is in één oogopslag het verband te zien hoevaak deze genen worden gedecteerd als DE met een groene trendlijn. Met op de x-as eigenschappen van de genen gebundeld in bins van 300, en op de y-as het aantal differentieel geëxprimeerde genen per bin. 
Het is van belang om de significante functies worden onderzocht, deze informatie kan bepaald worden met een GO-analyse.
[Go-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/resultaten/go-analyse.png)
Deze dotplot is een vorm van een go-analyse. Op de y-as staan de biologische functies en op de x-as de hoeveelheid genen die geassocieerd zijn met deze functie, hoe groter een punt, hoe meer genen er bijdragen aan deze functie. De kleur van deze punten toont de significantie. Er is te zien welke biologische functies verrijkt zijn in een set van genen. Door te weten welke invloed de functie antigen binding heeft kan er diagnose gesteld worden, en kan deze informatie worden gebruikt in nader onderzoek. 
[KEGG-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/resultaten/hsa04612.pathview.png)
Het proces en de presentatie van deze functie is te visualiseren met een KEGG-analyse. Antigen binding wijst op het immuunsysteem, waaronder MHC klasse 1 en 2 vallen. *Specifiek de T-cell receptoren(TCR) zijn afhankelijk van de antigen binding receptoren.*

# Conclusie
In de [Vulkaanplot](https://github.com/savvdzwld/casus-transcriptomics/blob/main/resultaten/Vulkaanplot.png) is te zien dat ANKRD30BL een van e significant veranderde genen is, kijkende naar het verschil tussen het humane genoom en de RA patiënten data. Bij de [Bias-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/resultaten/pwf.png) is te zien dat de data mogelijk biased is.
 Wanneer de kans op detectie als DE toeneemt.
 Interpretatie:
•	Als de kans op detectie als DE toeneemt met bijvoorbeeld hogere expressie, dan is je data biased en moet je dat mogelijk corrigeren in downstream analyses zoals gene set enrichment.
