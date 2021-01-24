# miRNA_Target_Finder
A tool to identify strongly supported miRNA targets using databases of validated or predicted interactions.

## To run:
1 Open file in RStudio\
2. Knit > Knit with Parameter\
3. Select input file OR input miRNA name(s) (in hsa-miR-##-#p format)\
4. Select options:
- **Validated interactions:** output validated results in .html file
- **Predicted interactions:** output validated results in .html file
- **How many targets to return?:** number of results in .html file
- **Save output file of all data:** save validated, predicted results to .xlsx file
- **Minimum prediction databases per query:** to prevent bias from strong predictions from a single database when performing cotargeting analysis, select a minimum number of databases that must predict an interaction with each query. 4 databases minimum is recommended
- **Beep when finished:** audio beep once results are ready

### Validated Interactions:
- Pulls from validated databases (mirecords, mirtarbase, tarbase)
- Cleans data, removes duplicate pubmedIDs per target to avoid redundancy in counting
- Removes both validated and predicted results of confounding miRNA(s)
-- Note: Alternative confounding filters available in excel output
- Ranks results by number of supporting publications ("records")

A higher number of records indicates more studies have validated the interaction, providing more confidence that the interaction is legitimate, but easily biased by popular genes being studied more.


### Predicted Interactions:
- Pulls from prediction databases (diana_microt, elmmo, microcosm, miranda, mirdb, pictar, pita, targetscan)
- Cleans data, removes duplicated rows to avoid redundancy in counting
- Removes validated results for the query miRNA(s) from predicted results
- Removes both validated and predicted results of confounding miRNA(s)
- Ranks according to database count, then mean rank across databases

A higher number of predicting databases indicates more reliability for the interaction, as it is predicted by more distinct algorithms. A lower mean rank further indicates confidence within those predictions, though this is emphasized less than presence of additional predicting databases.

## Excel Output
**Val_Filtered_Targs:** Validated targets shared by all queries, filtered to remove validated + predicted results of confounding miRNA(s)
- **Target_symbol:** identifier of target gene
- **Reports:** number of publications supporting targeting by query miRNA(s) (if multiple queries, total across both)

**Pred_Filtered_Targs:** Predicted targets shared by all queries, filtered to remove validated + predicted results of confounding miRNA(s), ranked by number of databases, then mean of prediction rank across databases
- **Target_symbol:** identifier of target gene
- **database_count:** number of databases supporting targeting by query miRNA(s) (if multiple queries, total across both)
- **mean_rank:** the mean of all per-database ranks (best = 1, 2nd best = 2, etc) calculated according to the scoring system of each database
- **Remaining columns:** number of query miRNAs predicted by each database

**Val_All_Targs:** Additional data for validated targets
- **Unfiltered:** Targets shared by all queries, without filtering for confounding miRNAs
- **No_Conf_P:** Targets shared by all queries, filtered to remove predicted results for confounding miRNA(s)
- **No_Conf_V:** Targets shared by all queries, filtered to remove validated results for confounding miRNA(s)

**Pred_All_Targs:** Additional data for predicted targets, filtered to remove validated results
- **Unfiltered:** Targets shared by all queries, without filtering for confounding miRNAs
- **No_Conf_P:** Targets shared by all queries, filtered to remove predicted results for confounding miRNA(s)
- **No_Conf_V:** Targets shared by all queries, filtered to remove validated results for confounding miRNA(s)

**Val_Confounding_Targs:** Validated targets of all confounding miRNA(s), used for filtering

**Pred_Confounding_Targs:** Predicted targets of all confounding miRNA(s), used for filtering
