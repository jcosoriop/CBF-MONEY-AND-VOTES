# CBF MONEY AND VOTES
 
 library(tidyverse)
library(janitor)
library(readxl)

CFB_2021_Mayoral <- read_excel("CFB 2021 Mayoral.xlsx")
View(CFB_2021_Mayoral)

MayoralData <- CFB_2021_Mayoral %>% 
  clean_names() %>% 
  group_by(recipname) %>% 
  summarize(Total = sum(amnt))

only_candidates <- MayoralData[-c(1,3,4,5,6,7,9,10,11,12,13,14,15,17,18,19,20,21,22,24,25,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,43,44,45,47),]

#this eliminted all the candidates that recieved donation but did not fit into the criertia we are studying and eliminated the unnecessary columns that had information that was not necessary for this research 

Election_Results_2021_Mayoral_Democratic_Primary <- read_excel("Election Results 2021 Mayoral Democratic Primary.xlsx")
View(Election_Results_2021_Mayoral_Democratic_Primary)

ElectionResults <- Election_Results_2021_Mayoral_Democratic_Primary
only_results <- ElectionResults[-c(9,10,11,12,13,14),]

#this eliminated all the candidates that had less than 1% of the vote

only_candidates %>% ggplot(aes(x = recipname)) +
  geom_bar()

hist(only_candidates$Total, breaks =100)

full_join(only_candidates, only_results, by ="Candidate")
