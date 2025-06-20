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
Reumatoïde artritis(RA) staat bekend als een chronische inflammatoire auto-immuunziekte[(Grassi et al. (1998))](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/The%20clinical%20features%20of%20rheumatoid%20arthritis.pdf), het afweersysteem keert tegen het lichaam. Normaliter worden ziekteverwekkers afgevoerd en afgebroken met het afweersysteem. De onderliggende oorzaak is onbekend, echter meespelende factoren wel. Tumornecrosefactor (TNF-α)  en interleukine 6(IL-6) zijn cytokines(onderdeel van het immuunsysteem) die zorgen voor de communicatie tussen immuun cellen.  TNF-α en IL-6 treden op  wanneer er sprake is van ontsteking door RA.[(Tornero Molina et al., 2020)](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/Reumatologia-Clinica.pdf)[(Idriss & Naismith, 2000)](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/TNF-a_and%20the%20TNF%20Receptor%20Superfamily%3B%20Structure-Function%20Relationship(s).pdf) Bij RA  verstijven en zwellen de gewrichten op wat kan leidden tot ontstekingen, hierdoor ontstaan pijnklachten. Mettertijd kunnen de botten en het kraakbeen beschadigen.[(Grassi et al. (1998))](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/The%20clinical%20features%20of%20rheumatoid%20arthritis.pdf) Met gebruik van RNA-sequencing wordt data vergeleken met klachten en ziektemechanismen voor een vroege diagnose, vroege diagnose voorkomt lange termijn klachten. Het onderzoek omvat data van een eerder uitgevoerd onderzoek(Platzer et al., 2019). De 8 samples van het weefsel van het gewrichtsslijmvlies, waaronder 4 gezonde patiënten en 4 samples van patiënten met vastgestelde RA van minimaal 12 maanden. Met deze data wordt bepaald welke gen-functies verschillen tussen gezonde en RA-patiënten, en hoe zijn deze ontstaan. Waaruit zal blijken of er doormiddel van transcriptomics een diagnose gesteld kan worden.

# Methode
![Flowchart transcriptomics](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Assets/Flowchart-%20transcriptomics.png)

*Figuur 1: Flowchart van de transcriptonomics analyse voor het vergelijken van datasets van gezonde patiënten en het humane genoom.* 

Doormiddel van transcriptomics in R-studio met(R 4.5.0) met gebruik van [script](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Scripts/casus%20transcriptomics%20r%20script.R) , wordt RA vroegtijdig aangetoond. Het humane genoom werd als vergelijkingsdata gebruikt, deze data is uit het sequence read archive  van NCBI gehaald. (bron). Door het genoom te indexeren(bioconducter(3.21), BiocManager(1.30.25) packages) kon het align-programma specifiek zoeken in deze data. Deze reads werden gemapt tegen het referentie genoom , waar gesorteerde Binary alignment/map (BAM) bestanden uit kwamen, waaruit genexpressie tellingen kwamen, waarmee de count matrix is gemaakt(readr(2.1.5), dplyr(1.1.4),Rsamtools(2.24.0),Rsubread(2.23.1) packages). In een count matrix staat per gen hoeveel reads er op dat gen zijn gemapt. Met gebruik van een GTF-bestand werd deze matrix bewerkt(DESeq2(1.48.1), KEGGREST(1.40.0)packages), zodat er verschil gemaakt werd tussen de RA en gezonde patiënten data.  Waarna een DESeqDataSet object  werd aangemaakt, wat de ruwe counts normaliseert en een differentiële expressie-analyse uitvoert, waaruit de significante resultaten gesorteerd werden. Deze data werd gevisualiseerd (EnhancedVolcano(1.26.0) package) in een vulkaanplot. Met een bias-analyse werd de gen-lengte beperkt(goseq(1.60.0), geneLenDataBase(1.44.0), org.Dm.eg.db(3.21.0) packages), waardoor er een gespecificeerde Go-analyse werd uitgevoerd(org.Hs.eg.db(3.21.0), ggplot2(3.5.2), tidyverse packages(2.0.0). Uit de go-analyse zijn significante functies van de genen te bepalen. Door middel van KEGG-analyse (pathview(1.48.0)package) is er visueel te laten zien welke cellulaire veranderingen plaatsvinden die tot de significante verandering leidden, en zo invloed hebben op de functies en het ziektebeeld. 

# Resultaten
Om een diagnose te stellen zijn resultaten vereist, doormiddel van visualisatie zijn verschillen duidelijker zichtbaar.

![Vulcanoplot](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/Vulcanoplot.png)

*Figuur 2: Een vulkaanplot met op de x-as de mate van verandering in expressie, en op de y-as de significantie van deze verandering. Groen betekent dat er een statistische significante verandering in genexpressie is aangetoond.* 

In figuur 2 is gevisualiseerd hoeveel de genexpressie van specifieke genen significant zijn verandert. ANKRD30BL en SLC9A3R2 in het groen zijn een van de significante genen met veranderingen. Van deze samenhang is een bias-analyse uitgevoerd in differentieel geëxprimeerde(DE) data.

![Bias-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/bias-analyse.png)

*Figuur 3: Bias-analyse waarin in één oogopslag het verband te zien is hoevaak genen worden gedecteerd als DE met een groene trendlijn. Met op de x-as eigenschappen van de genen gebundeld in bins van 300, en op de y-as het aantal differentieel geëxprimeerde genen per bin. * 

In figuur 3 is te zien dat de trendlijn oploopt, en later uitvlakt. Het is van belang dat de significante functies worden onderzocht, deze informatie kan bepaald worden met een GO-analyse.

![Go-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/go-analyse.png)

*Figuur 4: Dotplot van een GO-analyse waarbij op de y-as de biologische functies staan en op de x-as de hoeveelheid genen die geassocieerd zijn met deze functie, hoe groter een punt, hoe meer genen er bijdragen aan deze functie. De kleur van deze punten toont de significantie. Een hogere x-as waarde betekent meer gekoppelde genen uit de eigen data-set specifiek voor de geselecteerde data, aan deze functie.*

Er is in figuur 4 te zien dat de antigen binding functie verrijkt is, wat een significant verschil is. Het proces en de presentatie van deze functie is te visualiseren met een KEGG-analyse.

![KEGG-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/KEGG-analyse-hsa04612.pathview.png)

*Figuur 5: Een KEGG-analyse van hsa04612 waarbij de controlegroep is vergeleken tov de RA-groep. Veranderingen in het proces van deze antigen binding functie,is te zien aan kleuren. Rood betekent dat de celsoort meer expressie en groen een lagere expressie toont.* 

 In deze pathview (figuur 5) is te zien dat bij gezonde patiënten MHCI, PA28 en HSP70/90, in tegenstelling tot MHCII en IFNƴ , een hogere expressie is aangetoond dan bij patiënten met RA.

# Conclusie
In de [vulcanoplot](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/Vulcanoplot.png) is te zien dat ANKRD30BL een van de significant veranderde genen is.  Bij de [Bias-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/bias-analyse.png) is te zien dat de data biased is, aangezien de detectie als DE is toegenomen, wat een represntatieve diagnose tegen houdt. Na het corrigeren van deze data is in de [go-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/go-analyse.png) geconstateerd dat het aantal gekoppelde genen aan het antigen binding proces significant verschilt bij RA-patiënten. Met de [KEGG-analyse](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Resultaten/KEGG-analyse-hsa04612.pathview.png) is aangetoond dat dit verschil inhoudt dat gezonde patiënten een immuunsysteem hebben met een hogere eiwitafbraak en antigeenbewerking. [(Wolfe et al. (2013))](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/HSP70%20%26%2090%20onderdrukken%20proteotoxiciteit.pdf) 
[(Krüger et al. (2019))](https://github.com/savvdzwld/casus-transcriptomics/blob/main/Bronnen/Role%20of%20heat%20shock%20proteins%2070%20%26%2090%20in%20exercise%20physiology.pdf)Door deze verhogingen wordt de MHC presentatie verhoogd, en lichaamseigen eiwitten afgebroken, wat voorkomt bij RA-patiënten. Waaruit te concluderen is dat met transcriptomics, een diagnose te stellen is. Voor vervolg onderzoek zullen er meerdere functies onderzocht worden.
