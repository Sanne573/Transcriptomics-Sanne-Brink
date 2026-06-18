# Titel
## Structuur
AANVULLEN
- `Data_RA_raw` – Hierin staat de ruwe data waarmee deze transcriptomics analyse is gedaan
- `FLowschema` - Hierin staat het flowschema wat gebruikt is in de methode
-  `Resultaten` - Hierin staan de figuren die zijn gebruikt in de resultaten
- `Bronnen` - Hierin staan de bronnen die gebruikt zijn over het gehele verslag
- `script` – Hierin staat het script hoe de transcriptomics analyse is uitgevoerd
- `README.md` - Het document met het verslag er in

## Introductie
1 BRON TOEVOEGEN EN LOPEND VERHAAL VAN MAKEN
Reumatoïde artritis (RA) is een chronische auto-immuunziekte. Het afweersysteem ziet de gewrichten als lichaamsvreemd en valt ze aan. Hierdoor ontstaan ontstekingen in en rond de gewrichten. Vaak ontstaan deze ontstekingen in de pezen, slijmbeurzen of spieren, maar kunnen ook voorkomen in organen of andere weefsels buiten het gewricht (Reumatoïde Artritis (RA) | ReumaNederland, z.d.). De oorzaak van deze auto-immuunziekte is nog onbekend en hier wordt veel onderzoek naar gedaan. Momenteel is er bekend dat het geen erfelijke ziekte is. Wel zijn omgevingsfactoren belangrijk bij eht ontstaan van RA. Vooral roken is een belangrijk risicofactor (UMC Utrecht, z.d.). Er is verder bekend dat bij Reumatoïde artritis er een ontregeling is in immuungerelateerde genen en pathways (Zhang et al., 2019). Ondanks deze resultaten is er naar Reumatoïde artritis nog veel onderzoek nodig. In dit onderzoek wordt, met behulp van transcriptomics, gekeken naar de expressie van genen bij personen met Reumatoïde artritis. Hierbij is het doel de ziektemechanismen met de betrokken genen en pathways beter te analyseren en in kaart te brengen. 

## Methode
DOORLEZEN EN GOED LOPOEND MAKEN

<p align="center">
  <img src="Flowschema/Flowschema.png" alt="Flowschema" width="800"/>
</p>

*Figuur 1. Flowschema.*

### Data verkrijgen
In dit onderzoek zijn 236 RNA sequencing synoviale biopten uit artikelen van Walsh et al. en Guo et al. gecombineerd tot 1 dataset. Voor het sequencen van het RNA is in beide artikelen Illumina gebruikt. De reads zijn geanalyseerd in R (R 4.5.3) doormiddel van een transcriptomics analyse en opgeslagen in een [script](..). 
### Primaire verwerking
Als eerst is BioManager versie 1.30.27 geïnstalleerd. Daarna zijn de reads gemapped tegen het [humane referentiegenoom versie hg38 (GRCh38)](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000001405.40/ ) met Rsubread versie 2.24.0. Hiervoor is eerst een index van het referentiegenoom gemaakt. De gemapte reads zijn opgeslagen in BAM-files. 
Daarna is er met behulp van een annotatiebestand in Gene Transfer Format (GTF) een read-telling uitgevoerd. Voor het referentiegenoom werd gebruikt gemaakt van hetzelfde humane referentiegenoom versie hg38 (GRCh38). Vervolgens is er met Rsubread versie 2.24.0 een Count matrix gemaakt door de BAM-files te vergelijken met het annotatiebestand. 
Daarna is hiervan een differentiële expressie-analyse uitgevoerd met DESeq2 versie 1.50.2. 
### Gene Ontrology analyse
De Gene Ontrology (GO) analyse is gedaan op basis van een script op [MetwareBio](https://www.metwarebio.com/go-enrichment-analysis-clusterprofiler-guide/). Aanpassingen zijn gedaan met behulp van ChatGPT. Als eerst is er een GO-enrichment analyse gedaan met clusterProfiler versie 4.18.4. Hierbij is de P-waarde gecorrigeerd met de Benjamini-Hochenberg procedure. Genen werden als statistische significant beschouwd bij een gecorrigeerde P-waarde van < 0.05 en een q-waarde, False Discovery Rate gecorrigeerde P-waarde, van < 0.02. De top 10 hiervan is weergegeven in een dotplot met enrichplot versie 1.30.5. 
### Data visualiseren
Uit het dotplot zijn KEGG-pathways gekozen die zijn geanalyseerd met KEGGREST versie 1.50.0 en gevisualiseerd met pathview versie 1.50.0. 
Tot slot is er een Volcanoplot gemaakt waarin de uitgezochte genen uit de verschillende pathways zijn gelabeld met EnhancedVolcano versie 1.28.2. 

## Resultaten
In dit onderzoek is gekeken naar 236 RNA seq biopten van personen met en zonder reuma. Deze data is geanalyseerd doormiddel van een transcriptomics analyse. Hierbij is een differentiële expressie-analyse uitgevoerd. Dit is gevisualiseerd met een volcano plot. Daarna is een GO-analyse gedaan waaruit een dotplot is gemaakt. Tot slot zijn er KEGG pathways gekozen en gevisualiseerd. Hieruit zijn een aantal differentieel tot expressie gekomen genen gekozen en uitgelicht. 

In het figuur 2 is een volcano plot te zien. De rode punten zijn genen die binnen de beide grenswaarden vallen; een -log10 p van > 5 en een log2 fold change van -2 tot 2. Dit zijn dus de genen die statistisch significant zijn veranderd. GELABELDE GENEN UITLEGGEN, HOEVEEL VERANDERD EN HOE ZEKER IS DIT. 

VULCANO PLOT
*Figuur 2. Volcano plot van differentiële expressie-analyse van patiënten met Reumatoïde artiritis ten opzichte van gezonde personen. Op de x-as is de log2 fold change weergegeven en op de y-as de -log10 P. De stippellijnen zijn de gestelde grenzen; een log2 fold change van -2 tot 2 en een -log10 p van > 5. De rode punten vallen binnen deze grenswaarden. De groene punten vallen alleen binnen de grenswaarden van de log2 fold change. De grijze punten vallen binnen geen van beide grenswaarden. De gelabelde genen worden in dit onderzoek verder besproken en dieper op in gegeaan.*



<p align="center">
  <img src="Resultaten/GO_dotplot1.png" alt="Dotplot" width="500"/>
</p>

*Figuur 3. Dotplot van de top 10 meest significante 
biologische processen uit de GO-analyse. Op de y-as staan de biologische processen en op de x-as het gen ratio, of wel het aandeel genen dat bij het proces betrokken is. De kleur overgang geeft de p.adjust waarde weer, p-waarde gecorrigeerd met Benjamini-Hochenberg procedure. De grote van de bolletjes geeft het aantal genen weer dat binnen het biologische proces vallen.*

<p align="center">
  <img src="Resultaten/hsa04660.pathview.png" alt="Pathway T-cel" width="500"/>
</p>

*Figuur 4. KEGG pathway kaart van "T cell signaling pathway". De rood gekleurde genen zijn opgereguleerd en de groen gekleurde genen zijn neerwaarts gereguleerd ten opzichte van de controle groep.* 

<p align="center">
  <img src="Resultaten/hsa04662.pathview.png" alt="Pathway B-cel" width="500"/>
</p>

*Figuur 5. KEGG pathway kaart van "B cell signaling pathway". De rood gekleurde genen zijn opgereguleerd en de groen gekleurde genen zijn neerwaarts gereguleerd ten opzichte van de controle groep.* 


## Conclusies
