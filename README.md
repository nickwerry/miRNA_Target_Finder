# miRNA_Target_Finder
A tool to identify strongly supported miRNA targets using databases of validated or predicted interactions.

## To run:
1 Open file in RStudio/
2. Knit > Knit with Parameter/
3. Input miRNA name (in hsa-miR-##-#p format)/
4. Select options (see below)/

### Validated Interactions:
- Pulls from validated databases (mirecords, mirtarbase, tarbase)
- Cleans data, removes duplicated target/pubmedID to avoid redundancy
- Ranks results by number of supporting publications

### Predicted Interactions:
- Pulls from prediction databases (diana_microt, elmmo, microcosm, miranda, mirdb, pictar, pita, targetscan)
- Cleans data, removes duplicated target/database to avoid redundancy
- Ranks results by score in each database
- Mean_rank averages rank across databases, used for final ordering.*
* Mean_rank favours targets which score highly in a single database and are not predicted by others. Adjust "Minimum number of predicting databases" to account for this (min. value of 4 recommended). 
