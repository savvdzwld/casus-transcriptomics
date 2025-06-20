# Reumatoïde Artritis Transcriptomics

![RNA_sequencing_voorpagina](https://github.com/user-attachments/assets/23f3beed-82b0-4c4d-8ba2-09fd2fb2538e)

# Inhoud
- `Assets/`- de bronnen van de niet zelf-gegenereerde gebruikte plaatjes in het readme file
- `Data/raw/`- dataset van reumapatiënten
- `Data/processed`- verwerkte data van deze dataset
- `Data_stewardship`- toepassing en gebruik van de github pagina voor de data-steward
- `Scripts/`- het gebruikte script om de data te verwerken
- `Bronnen/`- de gebruikte bronnen met het literatuuronderzoek, voor de achtergrondinformatie
- `Resultaten/`- de grafieken en figuren van de verwerkte data set, gevisualiseerde resultaten
- `README.md`- de geschreven informatie van dit onderzoek


# Inleiding
Reumatoïde artritis(RA) staat bekend als een chronische inflammatoire auto-immuunziekte[(Bron,(Grassi et al. (1998)))](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/The%20clinical%20features%20of%20rheumatoid%20arthritis.pdf), het afweersysteem keert tegen het lichaam. Normaliter breekt en voert ziekteverwekkers af met dit afweer systeem, beschermt het lichaam. De onderliggende oorzaak is onbekend, echter een deel van de meespelende factoren wel. Tumornecrosefactor (TNF-α)  en interleukine 6(IL-6) zijn cytokines(onderdeel van het immuunsysteem) wat zorgt voor de communicatie tussen de cellen.  TNF-α en IL-6 onder houden gewrichten en* treden op  wanneer er sprake is van ontsteking door RA.[(Bron)](https://github.com/savvdzwld/casus-transcriptomics/blob/main/bronnen/Reumatologia-Clinica.pdf)[(Bron)](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/TNF-a_and%20the%20TNF%20Receptor%20Superfamily%3B%20Structure-Function%20Relationship(s).pdf) Bij RA  verstijven en zwellen de gewrichten op wat kan leidden tot ontstekingen. hierdoor ontstaan pijnklachten en mettertijd kunnen de botten en het kraakbeen beschadigen.[(Bron,(Grassi et al. (1998)))](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/The%20clinical%20features%20of%20rheumatoid%20arthritis.pdf) *behandeling/diagnose informatie* Vroege diagnose voorkomt lange termijn klachten. Met gebruik van RNA-sequencing kan data worden vergeleken met klachten en ziektemechanismen voor een vroege diagnose. Het onderzoek omvat data van een eerder uitgevoerd onderzoek(Platzer et al., 2019). De 8 sampels van het weefsel van het gewrichtsslijmvlies, waaronder 4 gezonde patiënten en 4 samples van patiënten met vastgestelde RA van minimaal 12 maanden. Welke genfuncties zijn verschillend tussen gezonde en RA-patiënten, en hoe zijn deze ontstaan?

# Methode
![Flowchart transcriptomics](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Assets/Flowchart-%20transcriptomics.png)

*Figuur 1: Flowchart methode* 

Doormiddel van transcriptomics, wordt RA vroegtijdig aangetoond. De RNA-sequencing wordt uitgevoerd in R-studio met *versie van R* met gebruik van [script](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Scripts/casus%20transcriptomics%20r%20script.R) om verschillende analyses uit te voeren. Het humane genoom werd als vergelijkingsdata gebruikt, deze data is uit het sequence read archive  van NCBI gehaald. (bron). De "bioconducter" package is specifiek ontwikkeld voor analyses van biologische data, RNA-seq. Om deze verschillende functies te  gebruiken is de "BiocManager"(versienummer) package nog nodig. Door het genoom te indexeren kon het align-programma specifiek zoeken in deze data. Deze reads werden gemapt tegen het referentie genoom , waar gesorteerde BAM bestanden uit komen.  Deze bestanden worden gebruikt om de genexpressie te tellen. BAM staat voor Binary alignment/map. Waarna de count matrix is gemaakt doormiddel van de "readr, dplyr,Rsamtools,Rsubread"(versienummers)packages. In een count matrix staat per gen hoeveel reads er op dat gen zijn gemapt. Met gebruik van een GTF-bestand werd de matrix bewerkt("DESeq2, KREGGEST"packages)(versienummers), zodat er verschil gemaakt werd tussen de RA en gezonde patiënten data. DESeqDataSet object aangemaakt met deze data, wat de ruwe counts normaliseert en een differentiele expressie-analyse uitvoert, waaruit de significante resultaten gesorteerd wordt. Deze data werd gevisualiseerd (EnhancedVolcano package) in een vulkaanplot. Met een bias-analyse wordt de genlengte beperkt, waardoor er een gespecificeerde Go-analyse wordt uitgevoerd. Uit de go-analyse zijn significante functies van de genen te bepalen. Door middel van KEGG-analyse met een significant veranderde functie, is er visueel te laten zien welke cellulaire veranderingen plaatsvinden die tot de significante verandering leidden, en zo invloed hebben op de functies en het ziektebeeld. 

# Resultaten
Om een diagnose te stellen zijn resultaten vereist, doormiddel van visualisatie zijn verschillen duidelijker zichtbaar.

![Vulcanoplot](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/Vulcanoplot.png)

*Figuur 2: Een vulkaanplot* 

Met een vulkaanplot wordt gevisualiseerd hoeveel de genexpressie van specifieke genen significant verandert. Op de x-as de mate van verandering in expressie, en op de y-as de significantie van deze verandering. Hoe hoger de waarde,blauw gekleurd, des te significanter. ANKRD30BL in het groen is een van  de significante genen met veranderingen van beide, deze functies kunnen samenhangen. Van deze samenhang is een bias-analyse uitgevoerd in differentieel geëxprimeerd(DE) data.

![Bias-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/bias-analyse.png)

*Figuur 3: Bias-analyse* 

Hierin is in één oogopslag het verband te zien hoevaak deze genen worden gedecteerd als DE met een groene trendlijn. Met op de x-as eigenschappen van de genen gebundeld in bins van 300, en op de y-as het aantal differentieel geëxprimeerde genen per bin. 
Het is van belang om de significante functies worden onderzocht, deze informatie kan bepaald worden met een GO-analyse.

![Go-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/go-analyse.png)

*Figuur 4: GO-analyse, hogere x-as waarde betekent meer gekoppelde genen uit de eigen data-set(lijst) dus specifiek voor mijn data, aan deze functie. grootte van de stip houdt in hoeveel genen van het hele genoom in deze biologisceh processen zijn betrokken* 

Deze dotplot is een vorm van een go-analyse. Op de y-as staan de biologische functies en op de x-as de hoeveelheid genen die geassocieerd zijn met deze functie, hoe groter een punt, hoe meer genen er bijdragen aan deze functie. De kleur van deze punten toont de significantie. Er is te zien welke biologische functies verrijkt zijn in een set van genen. Door te weten welke invloed de functie antigen binding heeft kan er diagnose gesteld worden, en kan deze informatie worden gebruikt in nader onderzoek. 

![KEGG-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/KEGG-analyse-hsa04612.pathview.png)

*Figuur 5: KEGG-analyse, waarbij controle tov RA, (hsa04612)* 

Het proces en de presentatie van deze functie is te visualiseren met een KEGG-analyse. Antigen binding wijst op het immuunsysteem, waaronder MHC klasse 1 en 2 vallen. In deze pathview (figuur 5) is te zien dat bij gezonde patiënten MHCI, PA28 en HSP70/90, in tegenstelling tot MHCII en IFNƴ , een hogere expressie tonen dan patiënten met RA.*Specifiek de T-cell receptoren(TCR) zijn afhankelijk van de antigen binding receptoren.*

# Conclusie
In de [vulcanoplot](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/Vulcanoplot.png) is te zien dat ANKRD30BL een van de significant veranderde genen is, kijkende naar het verschil tussen het humane genoom en de RA patiënten data. Bij de [Bias-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/bias-analyse.png) is te zien dat de data biased is, aangezien de detectie als DE is toegenomen.*wat betekent dit dan, wat gebeurt er als de data biased is* Na het corrigeren van deze data is in de [go-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/go-analyse.png) geconstateerd dat het aantal gekoppelde genen aan het antigen binding proces significant verschilt bij RA-patiënten. Met de [KEGG-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/KEGG-analyse-hsa04612.pathview.png) is aangetoond dat dit verschil inhoudt dat gezonde patiënten een imuunsysteem hebben met een hogere eiwitafbraak en antigeenbewerking. (https://pubmed.ncbi.nlm.nih.gov/15770419/,https://pubmed.ncbi.nlm.nih.gov/15770419/)
