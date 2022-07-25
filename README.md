# CBF MONEY AND VOTES
 
 This research looks into the relationship between the Money the top 8 candidates in the 2021 Democratic Mayoral Primary raised and the actual election resuls. The main goal of this project was to answer how much each campaign spent per vote with the money they were able to raise in public and private funds.
 
 First thing I did was to download two datasets. 1) The NYC Campaign Finance Board "Follow the Money" data set and the NYS Board of Election certified election result from the 2021 Democratic Mayoral Primary. The first, in this code will be labeled as only_candidates and the second will be labeled only-results.
 
 I also downloaded R, which is what runs my code and the libraries below.
 
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

#this eliminated all the candidates that had less than 1% of the vote. The reason I did this was because I was only interested in looking at candidates that were competitive in the raise. There were over 20 candidates running for the nomination. In the database, there was also the write-in names on the ballot.

This meant that every person that people wrote on their ballot was in the database. This was a really tricky part because instead of filtiring out, I had to change my method an filter IN the candidates that I wanted, leaving everyone else behind

only_candidates %>% ggplot(aes(x = recipname)) +
  geom_bar()

hist(only_candidates$Total, breaks =100)

full_join(only_candidates, only_results, by ="Candidate")

The graphs that were created in R were helpful but they were not the best way to showcase my findings. Because of this, I was able to upload the data sets in tableau, which did not requeired code. 

I made4 separate graphs in tableau, which are located in my policy brief (linked at the end)

The first graph, I made solely with the only_candidate data set. It was a standard bar graph. The secondw as the same but with the only_results data set. Then for the 3rd, I made an union between those two graphs and got a graph that showed the proportions between the two.

The final graph I made was between the top 3 canidates to show how the winner of the election differed from the 2nd and 3rd place. 

 To have a better understadning of the data, I contacted someone at the New York City Campaign Finance who requested to remain anonymous.
 
Link to the Policy Brief: [https://docs.google.com/document/d/1EyqY9Gswn4kakbb0Abp_SRAFQZwoPRug2CFIXG_3OKE/edit]
