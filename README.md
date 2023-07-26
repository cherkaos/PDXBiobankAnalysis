# PDXBiobankAnalysis
 Scripts to analyze the gene expression profiles of PDXs from the MAPYYACTS cohort. Results are published in the following paper: 

Title: [A biobank of pediatric patient-derived-xenograft models in cancer precision
medicine trial MAPPYACTS for relapsed and refractory tumors](https://www.researchsquare.com/article/rs-2542996/v1)

Maria Eugénia Marques Da Costa<sup>1,20</sup>, Sakina Zaidi<sup>2</sup>, Jean-Yves Scoazec<sup>3</sup>, Robin Droit<sup>1,4</sup>,Wan Ching Lim<sup>1,5</sup>, Antonin Marchais<sup>1,20</sup>, Jerome Salmon<sup>1</sup>, Sarah Cherkaoui<sup>1,6</sup>, Raphael J. Morscher<sup>1,6</sup>, Anouchka Laurent<sup>7</sup>, Sébastien Malinge<sup>7,8</sup>, Thomas Mercher<sup>7</sup>, Séverine Tabone-Eglinger<sup>9</sup>, Isabelle Goddard<sup>10</sup>, Francoise Pflumio<sup>11</sup>, Julien Calvo<sup>11</sup>, Francoise Redini<sup>12</sup>, Natacha Entz-Werlé<sup>13</sup>, Aroa Soriano<sup>14</sup>, Alberto Villanueva<sup>15</sup>, Stefano Cairo<sup>16</sup>, Pascal Chastagner<sup>17</sup>, Massimo Moro<sup>18</sup>, Cormac Owens<sup>19</sup>, Michela Casanova<sup>18</sup>, Raquel Hladun-Alvaro<sup>14</sup>, Pablo Berlanga<sup>20</sup>, Estelle Daudigeos-Dubus<sup>1</sup>, Philippe Dessen<sup>1,4</sup>, Laurence Zitvogel<sup>1</sup>, Ludovic Lacroix<sup>3</sup>, Gaelle Pierron<sup>21</sup>, Olivier Delattre<sup>2,21,22</sup>, Gudrun Schleiermacher<sup>2,22</sup>, Didier Surdez<sup>2**#</sup>, Birgit Geoerger<sup>1,20#*</sup>.

#The authors jointly supervised this work 

1 INSERM U1015, Gustave Roussy Cancer Campus, Université Paris-Saclay, Villejuif, France

2 INSERM U830, Equipe Labellisée LNCC, Diversity and Plasticity of Childhood Tumors Lab, PSL Research University, SIREDO Oncology Centre, Institut Curie Research Centre, Paris, France

3 Department of Pathology and Laboratory Medicine, Translational Research Laboratory and Biobank, AMMICA, INSERM US23/CNRS UMS3655, Gustave Roussy Cancer Campus, Université Paris-Saclay, Villejuif, France

4 Gustave Roussy Cancer Campus, Bioinformatics Platform, AMMICA, INSERM US23/CNRS UAR3655, Villejuif, France

5 School of Data Sciences, Perdana University, Kuala Lumpur, Malaysia

6 Division of Oncology and Children's Research Center, University Children's Hospital Zurich, University of Zurich, Zurich, Switzerland

7 Gustave Roussy Cancer Campus, INSERM U1170, Université Paris-Saclay, Equipe labellisée Ligue Nationale Contre le Cancer, PEDIAC program, Villejuif, France

8 Telethon Kids Institute – Cancer Centre, Perth Children`s Hospital, Nedlands, WA, Australia

9 Biological Ressources Center, Centre Léon Bérard, Lyon, France

10 Small Animal Platform, Cancer Research Center of Lyon, INSERM U1052, CNRS UMR 5286, Centre Léon Bérard, Claude Bernard Université Lyon 1, Lyon, France

11 UMR-E008 Stabilité Génétique, Cellules Souches et Radiations, Commissariat à l'Energie Atomique et aux Energies Alternatives (CEA), Université de Paris-Université
Paris-Saclay, Fontenay-aux-Roses, 92260, France

12 INSERM UMR 1238, Université Nantes, Nantes, France

13 Pediatric Onco-Hematology Unit, University Hospital of Strasbourg, Strasbourg, UMR CNRS 7021, team tumoral signalling and therapeutic targets, University of Strasbourg, Faculty of Pharmacy, Illkirch, France

14 Vall d'Hebron Research Institute (VHIR), Childhood Cancer and Blood Disorders Research Group, Division of Pediatric Hematology and Oncology, Vall d'Hebron Barcelona Hospital Campus, Barcelona, Spain

15 Chemoresistance and Predictive Factors Group, Program Against Cancer Therapeutic Resistance (ProCURE), Catalan Institute of Oncology (ICO), Oncobell Program, Bellvitge 2 Biomedical Research Institute (IDIBELL), L’Hospitalet del Llobregat, Xenopat SL, Parc Cientific de Barcelona (PCB), Barcelona, Spain.

16 XenTech, Evry, France

17 Children University Hospital, Vandoeuvre‐lès‐Nancy, University of Nancy, Nancy, France

18 Fondazione IRCCS Istituto Nazionale dei Tumori, Milan, Italy

19 Paediatric Haematology/Oncology, Children’s Health Ireland, Crumlin, Dublin, Republic of Ireland

20 Department of Pediatric and Adolescent Oncology, Gustave Roussy Cancer Campus, Villejuif, France

21 Unité de Génétique Somatique, Service d’oncogénétique, Institut Curie, Paris, France

22 SiRIC RTOP (Recherche Translationnelle en Oncologie Pédiatrique); Translational Research Department, Institut Curie Research Center, PSL Research University, Institut Curie, Paris, France.

** Current address: Balgrist University Hospital, University of Zurich, Zurich, Switzerland

*Corresponding author: Birgit Geoerger, MD, PhD, Gustave Roussy Cancer Campus, INSERM U1015, Université Paris-Saclay, Department of Pediatric and Adolescent Oncology, 114 Rue Edouard Vaillant, 94805 Villejuif, France; Tel: +33 1 42 11 46 61, Fax: +33 1 42 11 52 45, Email: [birgit.geoerger@gustaveroussy.fr](mailto:birgit.geoerger@gustaveroussy.fr)


# Description
Scripts to perform metabolic task analysis. The analysis is performed using [Cellfie](https://github.com/LewisLabUCSD/CellFie), a computational framework to quantity a cell's metabolic functions. 

Steps:

1. Run Cellfie in Matlab using transcriptomics from PDX and patients. Script: runCellFie_PDX.m
2. Display results in R. Script: plottingCellfie_PDX.Rmd

