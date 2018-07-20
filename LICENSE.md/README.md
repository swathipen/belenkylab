# belenkylab

# Relative Abundance Plots
#Change directory!

library(plyr)
library(dplyr)
library(ggplot2)
library(plotly)

# data frame of cvs
sciencelit <- read.csv("gen_otu_del.csv")
as.data.frame(sciencelit)

#deleterows and subset
df <- sciencelit[c(33, 34, 35, 36, 37, 38), ]
df <- sciencelit[-c(31, 32, 33, 34, 35, 36, 37, 38), ]

#choose first 30 columns
df1 <- sciencelit[1:31]


cbPalette <- c("#999999", "#6666CC", "#56B4E9", "#009E73", "#F0E442", "#CCCCFF", "#3366FF", "#6633CC", "#3399FF", "#9999CC", "#66CC99", "#009999", "#CC99FF", "#FFFFCC", "#66CC66", "#333399")



library(reshape2)
df_long <- melt(df, id.vars = "X", variable.name = "Genera")
p <- ggplot(df_long, aes(x = X, y = value, fill = Genera)) + 
geom_bar(stat = "identity") +
xlab("Condition") +
ylab("Relative Abundance") +
scale_fill_manual(values=cbPalette)

ggplotly(p)


#Subsetting Data
Ctrl <- df1[1:6, ]
Ctrl_CA <- df1[7:8, ]
Pur <- df1[9:14, ]
Pur_CA <- df1[15:20, ]
AB <- df1[21:26, ]  
AB_CA <- df1[27:32, ]

plot_ly(df1, x = ~Sample, y = ~Proteobacteria, type = 'bar', name = 'Proteobacteria') %>% 
  add_trace(y = ~Bacteroidetes, name = 'Bacteroidetes') %>% 
  add_trace(y = ~Deferribacteres, name = 'Deferribacteres') %>% 
  add_trace(y = ~Cyanobacteria.Chloroplast, name = 'Cyanobacteria.Chloroplast') %>% 
  add_trace(y = ~Spirochaetes, name = 'Spirochaetes') %>% 
  add_trace(y = ~Fusobacteria, name = 'Fusobacteria') %>% 
  add_trace(y = ~Fibrobacteres, name = 'Fibrobacteres') %>% 
  add_trace(y = ~Firmicutes, name = 'Firmicutes') %>% 
  add_trace(y = ~Verrucomicrobia, name = 'Verrucomicrobia') %>% 
  add_trace(y = ~Tenericutes, name = 'Tenericutes') %>%
  add_trace(y = ~Actinobacteria, name = 'Actinobacteria') %>% 
  add_trace(y = ~Deinococcus.Thermus, name = 'Deinococcus.Thermus') %>% 
  add_trace(y = ~Chloroflexi, name = 'Chloroflexi') %>% 
  add_trace(y = ~Candidatus_Saccharibacteria, name = 'Candidatus_Saccharibacteria') %>% 
  add_trace(y = ~Planctomycetes, name = 'Planctomycetes') %>% 
  layout(title = "Phyla", yaxis = list(title = 'RA'), barmode = 'stack')
