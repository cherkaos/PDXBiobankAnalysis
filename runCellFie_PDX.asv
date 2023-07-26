%% Running Cellfie on the PDX
% Use new transcriptomics to find metabolic similairy between PDX and original tumor

% add path of Cellfie 
addpath(genpath('PanPedCan/Cellfie_Analysis/CellFie'))
% load data
load 'test/suite/dataTest.mat'

% Load table with TPM - store in structure expressionPDX2
expressionPDX = readtable('/PanPedCan/PDX/PDXCellfie/MAPPYACTS_PDX_NCBI_Complete.csv','ReadVariableNames',true,'HeaderLines',0,'ReadRowNames',true);
expressionPDX_ID = readtable('/PanPedCan/PDX/PDXCellfie/MAPPYACTS_PDX_NCBI_ID.csv');

expressionPDX2.gene=table2cell(expressionPDX_ID)
expressionPDX2.gene = cellfun(@num2str, expressionPDX2.gene, 'UniformOutput', false)

expressionPDX2.Tissue = expressionPDX.Properties.VariableNames;
expressionPDX2.value = table2array(expressionPDX);

% Number of samples (PDX)
sizePDX=size(expressionPDX)
numPDX=sizePDX(2)


%% Define the type parameters of the method

param_local.ThreshType='local';
param_local.LocalThresholdType='minmaxmean';
param_local.percentile_or_value='percentile';
param_local.percentile_low=25;
param_local.percentile_high=75;
ref='MT_recon_2_2_entrez.mat';

[score, score_binary ,taskInfos, detailScoring]=CellFie(expressionPDX2,numPDX,ref,param_local);

[score, score_binary ,taskInfos, detailScoring]=CellFie(data,length(data.Tissue),ref,param_local);

%% Run cellfie


param_local.ThreshType='local';
param_local.LocalThresholdType='minmaxmean';
param_local.percentile_or_value='percentile';
param_local.percentile_low=25;
param_local.percentile_high=75;
ref='MT_recon_2_2_entrez.mat';

expressionPDX = readtable('/PanPedCan/PDX/PDXCellfie/MAPPYACTS_PDX_Patients.csv','ReadVariableNames',true,'HeaderLines',0,'ReadRowNames',true,'VariableNamingRule','preserve');
expressionPDX_ID = readtable('/PanPedCan/PDX/PDXCellfie/MAPPYACTS_PDX_Patients_ID.csv');

expressionPDX2.gene=table2cell(expressionPDX_ID)
expressionPDX2.gene = cellfun(@num2str, expressionPDX2.gene, 'UniformOutput', false)

expressionPDX2.Tissue = expressionPDX.Properties.VariableNames;
expressionPDX2.value = table2array(expressionPDX);

% Number of samples (PDX)
sizePDX=size(expressionPDX)
numPDX=sizePDX(2)

[score_mean, score_binary_mean ,taskInfos, detailScoring]=CellFie(expressionPDX2,numPDX,ref,param_local);



%% Metadata
% Load models information
tmp = readtable('/PanPedCan/tINIT_Analysis/data/2021_05_05_RNA_Expression_Patient_Matrix_final_9.csv','Delimiter',',');
tmp_xeno = readtable('/PanPedCan/tINIT_Analysis/data/Xenograft_Annotation_08_07_2021.csv','Delimiter',',');

% Merging the 2 table - Mappy and pdx
tmpmerged = [tmp(:,[5,16,10,11]);tmp_xeno(:,[1,4,5,6])];

% Exception for PDX-MAP016 MAP016 P6 PDX CEL-T1 - Will consider it like MAP016
%tmpmerged.RNASeq_Matrix_ID=regexprep(tmpmerged.RNASeq_Matrix_ID,'_.*','')

PDX_Patient_Names=expressionPDX.Properties.VariableNames
PDX_Patient_Names=replace(PDX_Patient_Names,'PDX_','')
PDX_Patient_Names=replace(PDX_Patient_Names,'Patient_','')


[~,ind] = ismember(PDX_Patient_Names,tmpmerged.RNASeq_Matrix_ID); % if doesnt work, name of samples is incorrect
tumorType = tmpmerged.Disease_group(ind);
tumorSubType = tmpmerged.Histologygrouplevel1abbr(ind);
tumorHistoType = tmpmerged.Histologygrouplevel2VF(ind);
tumorHistoType(ismissing(tumorHistoType))={'NA'}

tumorType=replace(tumorType,'_',' ')

% Finding duplicates
[uniqueA i j] = unique(PDX_Patient_Names,'first');
indexToDupes = find(not(ismember(1:numel(PDX_Patient_Names),i)))
allduppos=find(ismember(PDX_Patient_Names,PDX_Patient_Names(indexToDupes)))
PDX_Patient_Names(allduppos)
expressionPDX.Properties.VariableNames(allduppos)

TumorTypeOrder= readtable('/PanPedCan/tINIT_Analysis/data/TumorType_Order.csv')


matched_PDX_Patient=replace(expressionPDX.Properties.VariableNames(allduppos),'_',' ')

%% Plotting on UMAP

addpath('/Users/sarahcherkaoui/Library/Mobile Documents/com~apple~CloudDocs/Morscher_Lab/Labmembers/Sarah_C/Matlab_Libraries/umap')
umap_coord=run_umap(double(score_mean'),'metric','euclidean','n_components',2,'n_neighbors',10,'marker_size',5)

figure;
hold on
gscatter(umap_coord(:,1),umap_coord(:,2),tumorSubType)
text(umap_coord(allduppos,1),umap_coord(allduppos,2),matched_PDX_Patient)
xlabel('UMAP 1');ylabel('UMAP 2');title('Tumour Type-perp10');set(gca,'FontSize',12,'LineWidth',1);

writematrix(double(umap_coord),'umap_coord_mean_perp10.csv')


%% Distance between match pdx and matient

compStruct_all = corrcoef(score_binary_mean);

distanceMatched=[]
distanceNotMatched=[]

% to compute the distance between match
for i=1:length(allduppos)
    
    posMatch=ismember(PDX_Patient_Names(allduppos),PDX_Patient_Names(allduppos(i)))
    posMatch(i)=0 % remove distance with itself
    posNotMatch=~ismember(PDX_Patient_Names,PDX_Patient_Names(allduppos(i)));
    distanceNotMatched=[distanceNotMatched compStruct_all(allduppos(i),posNotMatch)];
    distanceMatched=[distanceMatched compStruct_all(allduppos(i),allduppos(posMatch))];
end

figure
hold all
histogram(distanceNotMatched,10,'normalization', 'pdf','FaceColor','#0072BD')
histogram(distanceMatched,10,'normalization', 'pdf','FaceColor','#7E2F8E')

% Labels
xlabel('Pearson Correlation')
ylabel('Probability Density Function (%)')
legend({'Not Macthed', 'Matched'})
title('Similarity - Patient and PDX')
[h,p,ci,stats] = ttest2(distanceNotMatched,distanceMatched)

text(0.6,5,['pval = '  num2str(p)])



%% Export for plotting in R

1)
csvwrite('score_cellfie_local_mean.csv',score_mean)
csvwrite('score_binary_cellfie_local_mean.csv',score_binary_mean)


% Convert cell to a table and use first row as variable names
taskInfos_T = cell2table(taskInfos);
writetable(taskInfos_T,'taskInfos_cellfie.csv')

patient_T = cell2table(expressionPDX.Properties.VariableNames);
writetable(patient_T,'patient_ID.csv')

tumorSubType_T = cell2table(tumorSubType);
writetable(tumorSubType_T,'tumorSubtype_cellfie.csv')

tumorType_T = cell2table(tumorType);
writetable(tumorType_T,'tumorType_cellfie.csv')



