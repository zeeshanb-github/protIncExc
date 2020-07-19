# protIncExc
list of differentially regulated genes
**uploading packages**
```{r}
library(ggplot2)
library(tidyverse)
```
**This just shows how i set working directory on desktop**
```{r}
setwd("~/Desktop")
```
# coding for a scatter plot with gradient colors about a threshold value

```{r}
filename <- "HW03/protIncExcList.txt" #filename
my_data <- read.delim(filename, header=TRUE) # reading data as .txt
phb <- subset(my_data, Genes == "PHB3") # subsetting data to color a spefic gene
ggplot(my_data, aes(x=Genes, y=Log2_Mut_vs_WT, color = ifelse( Log2_Mut_vs_WT < -0.33, "Fail", "Pass"))) + #gradient color of differentially regulated genes
  geom_point(alpha=0.5)+   # this is the base plot
  geom_point(phb,mapping = aes(color="green")) +  # this adds a green point
  geom_text(phb, mapping=aes(label="PHB3", hjust=0.5, vjust=-0.5))+ # this adds a label for the green point
  theme_classic()+
  theme(axis.text.x=element_blank(), axis.ticks.x=element_blank())+
  theme(legend.position="none")+ geom_hline(yintercept=-0.33, linetype="dashed", color = "red")
```