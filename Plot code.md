# Plots from my thesis. Note that these may be updated from the exact ones used! 
```
R version 3.4.4 (2018-03-15) -- "Someone to Lean On"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-w64-mingw32/x64 (64-bit)
#Note, replotted the first plot in new R version 3.6.2 

library(ggplot2)
setwd("//cfsg01.campus.gla.ac.uk/SSD_Dept_Data_D/MVL/MVLPublic/VET/DevaneyLab/Team/J McIntyre/Back up May 2016/Back up/Thesis/Thesis/Thesis in progress/chp 1 - R in field")

sp<-read.table("Copy of Ewe and Lamb speciation R_sept_avg.txt", header=T)
summary(sp)
sp$dates<-as.Date(sp$Date, "%d/%m/%Y")

sp_nouk<-subset(sp, sp$Species != "Unkown_Strongyle")

sp<-sp_nouk

ewe<-subset(sp, sp$Age == "Ewe")
lamb<-subset(sp, sp$Age == "Lamb")

#Plot species data over time by percentage:

x<-ggplot(data=sp)+
coord_cartesian(ylim=c(0,1)) + labs(y="Species by proportion of total Strongyles identified", x="Date") +
scale_x_date(date_breaks = "1 month", date_labels="%b")+
geom_bar(mapping=aes(x=dates, y=Percentage, fill=Species), stat="identity", width=10)+
facet_wrap(~ Age, nrow = 2)+
scale_fill_manual(name="Species", values=c("grey64", "#FF00FF", "yellow", "green3", "grey20", "darkorange2", "#3366FF", "pink2"), labels=c("Cooperia curticei","Chabertia ovina", "Nematodirus battus", "Oesophagostomum venulosum", "Trichostrongylus axei", "Teladorsagia circumcincta", "Trichostrongylus vitrinus"))+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14), legend.title=element_text(size=12), legend.text = element_text(face="italic", size=12))
x
```
![image](https://user-images.githubusercontent.com/55552826/219421304-1523d624-9e53-4cb7-afc7-4da12ad1686f.png)
```
#FEC over the year on farm 1:

library(ggplot2)
setwd("//cfsg01.campus.gla.ac.uk/SSD_Dept_Data_D/MVL/MVLPublic/VET/DevaneyLab/Team/J McIntyre/Back up May 2016/Back up/Thesis/Thesis/Thesis in progress/chp 1 - R in field")

fec<-read.table("Ewe and Lamb FEC for R 2.txt", header=T)
summary(fec)
fec$dates<-as.Date(fec$Date, "%d/%m/%Y")

ewe<-subset(fec, fec$Age == "Ewe")
lamb<-subset(fec, fec$Age == "Lamb")

fec<-subset(fec, fec$Sample.name != "L_13")


#Plot of Strongyle FEC:

x<-ggplot(data=fec)+
labs(y="Strongyle faecal egg count (epg)", x="Date") +
scale_x_date(date_breaks = "1 month", date_labels="%b")+
geom_boxplot(mapping=aes(x=dates, y=Strongyle.epg, group=dates), width=5, outlier.shape=NA, fill="white", colour="#3366FF")+
geom_jitter(mapping=aes(x=dates, y=Strongyle.epg), width=0.3)+
facet_wrap(~ Age, nrow = 2)+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14))
x
```
![image](https://user-images.githubusercontent.com/55552826/219421434-e3b15c9f-da3b-47b9-8b91-8cbe8bc33726.png)
```
dat_text<-data.frame(label=c("MOX", "BZ", "BZ", "BZ", "LEV"), Age = c("Ewe", "Lamb", "Lamb", "Lamb", "Lamb"), x=c("07/04/2016", "23/05/2016", "14/06/2016", "06/07/2016", "20/09/2016"), y=c(2600, 2600,2600,2600,2600)) 
dat_text$x<-as.Date(dat_text$x, "%d/%m/%Y")

dat_man<-data.frame(Age = c("Ewe", "Ewe", "Ewe", "Ewe", "Ewe", "Lamb", "Lamb", "Lamb", "Lamb", "Lamb"), xmin=c("01/03/2016", "21/03/2016", "28/10/2016", "15/01/2017", "16/08/2016", "23/05/2016", "14/06/2016", "06/07/2016", "20/09/2016", "16/08/2016"), xmax=c("21/03/2016", "30/04/2016", "30/11/2016", "30/03/2017", "18/08/2016", "25/05/2016", "16/06/2016", "08/07/2016", "22/09/2016", "18/08/2016"), ymin=c(0,0,0,0,0,0,0,0,0,0), ymax=c(2500,2500,2500,2500,2500,2500,2500,2500,2500,2500), colour=c("light blue", "light green", "purple", "light blue","dark green","white","white","white","yellow","dark green"), alpha=c(0.3,0.3,0.3,0.3,0.6,0.8,0.8,0.8,0.5,0.6))
dat_man$xmin<-as.Date(dat_man$xmin, "%d/%m/%Y")
dat_man$xmax<-as.Date(dat_man$xmax, "%d/%m/%Y")

x2<-x+geom_text(data=dat_text, mapping=aes(x=x,y=y,label=label))+
geom_rect(data =dat_man, mapping=aes(xmin=xmin, ymin=ymin, xmax=xmax, ymax=ymax), fill=dat_man$colour, alpha=dat_man$alpha)+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14))
x2
```
![image](https://user-images.githubusercontent.com/55552826/219421485-9a62529e-759a-4a27-b67f-913905b4265b.png)
```
#Plot of nematodirus FEC:

x<-ggplot(data=fec)+
labs(y="Nematodirus faecal egg count (epg)", x="Date") +
scale_x_date(date_breaks = "1 month", date_labels="%b")+
geom_boxplot(mapping=aes(x=dates, y=Nematodirus.epg, group=dates), width=5, outlier.shape=NA, fill="white", colour="#3366FF")+
geom_jitter(mapping=aes(x=dates, y=Nematodirus.epg), width=0.3)+
facet_wrap(~ Age, nrow = 2)
x
```
![image](https://user-images.githubusercontent.com/55552826/219421544-c1a476fc-ae2d-4e80-8d0d-cf9d78f8fad3.png)
```
dat_text<-data.frame(label=c("MOX", "BZ", "BZ", "BZ", "LEV"), Age = c("Ewe", "Lamb", "Lamb", "Lamb", "Lamb"), x=c("07/04/2016", "23/05/2016", "14/06/2016", "06/07/2016", "20/09/2016"), y=c(400, 400,400,400,400)) 
dat_text$x<-as.Date(dat_text$x, "%d/%m/%Y")

dat_man<-data.frame(Age = c("Ewe", "Ewe", "Ewe", "Ewe", "Ewe", "Lamb", "Lamb", "Lamb", "Lamb", "Lamb"), xmin=c("01/03/2016", "21/03/2016", "28/10/2016", "15/01/2017", "16/08/2016", "23/05/2016", "14/06/2016", "06/07/2016", "20/09/2016", "16/08/2016"), xmax=c("21/03/2016", "30/04/2016", "30/11/2016", "30/03/2017", "18/08/2016", "25/05/2016", "16/06/2016", "08/07/2016", "22/09/2016", "18/08/2016"), ymin=c(0,0,0,0,0,0,0,0,0,0), ymax=c(380,380,380,380,380,380,380,380,380,380), colour=c("light blue", "light green", "purple", "light blue","dark green","white","white","white","yellow","dark green"), alpha=c(0.3,0.3,0.3,0.3,0.6,0.8,0.8,0.8,0.5,0.6))
dat_man$xmin<-as.Date(dat_man$xmin, "%d/%m/%Y")
dat_man$xmax<-as.Date(dat_man$xmax, "%d/%m/%Y")

x2<-x+geom_text(data=dat_text, mapping=aes(x=x,y=y,label=label))+
geom_rect(data =dat_man, mapping=aes(xmin=xmin, ymin=ymin, xmax=xmax, ymax=ymax), fill=dat_man$colour, alpha=dat_man$alpha)+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14))
x2
```
![image](https://user-images.githubusercontent.com/55552826/219421606-38ff987c-da3c-45a1-857c-7eb863682f4a.png)
```

## Lamb speciation data for FECRT in September 2016:

library(ggplot2)
setwd("//cfsg01.campus.gla.ac.uk/SSD_Dept_Data_D/MVL/MVLPublic/VET/DevaneyLab/Team/J McIntyre/Back up May 2016/Back up/Thesis/Thesis/Thesis in progress/chp 1 - R in field")

sp<-read.table("Lamb FECRT speciation R.txt", header=T)
summary(sp)
sp$dates<-as.Date(sp$Date, "%d/%m/%Y")

sp<-subset(sp, sp$Ant != "LEV")

#Plot species data over time by proportion:
x<-ggplot(data=sp)+
coord_cartesian(ylim=c(0,1)) + labs(y="Species by proportion of total Strongyles identified", x="Date") +
scale_x_date(date_breaks = "2 days", date_minor_breaks = "1 day", date_labels="%d %b")+
geom_bar(mapping=aes(x=dates, y=Percentage, fill=Species), stat="identity", width=1)+
facet_wrap(~ Ant, nrow = 2)+
scale_fill_manual(values=c("grey64", "#FF00FF", "yellow", "green3", "grey20", "darkorange2", "#3366FF", "pink2"))+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14))
x
```
![image](https://user-images.githubusercontent.com/55552826/219424438-a2a1384d-f410-4860-8d21-2f150b21d457.png)
```
sp<-subset(sp, sp$Species != "Unkown_Strongyle")
sp<-subset(sp, sp$Species != "N._battus")

#Plot species data over time by proportion of eggs:
x<-ggplot(data=sp)+
coord_cartesian(ylim=c(0,160)) + labs(y="Strongyle epg", x="Date") +
scale_x_date(date_breaks = "2 days", date_minor_breaks = "1 day", date_labels="%d %b")+
geom_line(mapping=aes(x=dates, y=Strongyle.epg, colour=Species), size=3)+
facet_wrap(~ Ant, nrow = 2)+
scale_fill_manual(values=c("grey64", "#FF00FF", "yellow", "green3", "grey20", "darkorange2", "#3366FF", "pink2"))+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14))
x
```
![image](https://user-images.githubusercontent.com/55552826/219424499-a0f09ff1-f236-4fab-a08c-918ef3fd1b9d.png)

```
###LAMB FECRT SEPTEMBER 2016. To plot a line plot with error bars of the SEM. 

library(ggplot2)
setwd("//cfsg01.campus.gla.ac.uk/SSD_Dept_Data_D/MVL/MVLPublic/VET/DevaneyLab/Team/J McIntyre/Back up May 2016/Back up/Thesis/Thesis/Thesis in progress/chp 1 - R in field")


fecrt<-read.table("Lamb FECRT speciation_byEPG_R.txt", header = T)
summary(fecrt)
fecrt$dates<-as.Date(fecrt$Date, "%d/%m/%Y")

#Plot epg by species proportion over time with error bars (using SEM):

x<-ggplot(fecrt, aes(x=dates, y=Strongyle.epg, group=Species, color=Species)) + 
geom_line(size=1) +
geom_point(size=3)+
geom_errorbar(aes(ymin=Strongyle.epg-SEM, ymax=Strongyle.epg+SEM), width=.5, position=position_dodge(0.05))+
coord_cartesian(ylim=c(0,200)) + labs(y="Strongyle epg", x="Date") +
scale_x_date(date_breaks = "2 days", date_minor_breaks = "1 day", date_labels="%d %b")+
facet_wrap(~ Ant, nrow = 2)+
scale_colour_manual(values=c("grey64", "#FF00FF", "green3", "grey20", "darkorange2", "#3366FF"))+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14))
x
```
![image](https://user-images.githubusercontent.com/55552826/219424542-dffc383b-8471-4184-96ca-fc828a341ae4.png)





```
kruskal.test(x=fec$Strongyle.epg, g=fec$dates)

#####
	Kruskal-Wallis rank sum	test

data:  fec$Strongyle.epg and fec$dates
Kruskal-Wallis chi-squared = 170.56, df = 19, p-value < 2.2e-16

####

#Subset to allow to perform the wilcoxon test (independent two-sample Mann-Whitney U for nonparametric data):
lamb<-subset(fec, fec$Age == "Lamb")


pairwise.wilcox.test(x=ewe$Strongyle.epg, g=ewe$dates, p.adjust.method="none")

m<-glm(Strongyle.epg ~ dates, data=fec)

#Updated R from 3.4.0 to 3.6.0
library(glmm)
#Will use Date, rather than dates, as the former is a FACTOR.
#fec has three factors (Age, Sample.name, Date)
#fec has two poisson response vectors - Strongyle.epg and Nematodirus.epg

#A glmm requires the RESPONSE vector and a random effect vector. It can also have fixed effect vectors too. 
#I'm going to ask for 2 clusters to run the model quicker, and I'm going to set a seed so that it will always produce the same values each time it's run: 

m<-glmm(Strongyle.epg ~ Date, random = list(~ 0 + Age, ~ 0 + Sample.name, ~ 0 + Management_event), varcomps.names=c("Age", "Sample_Name", "Management_event"),  data = fec, family.glmm = poisson.glmm, m = 10^3)

summary(m)


m<-glmm(Strongyle.epg ~ Date, random = list(~ 0 + Sample.name, ~ 0 + Management_event), varcomps.names=c("Sample_Name", "Management_event"),  data = ewe, family.glmm = poisson.glmm, m = 10^3)

summary(m)

m<-glmm(Strongyle.epg ~ Date, random = list(~ 0 + Sample.name, ~ 0 + Management_event), varcomps.names=c("Sample_Name", "Management_event"),  data = lamb, family.glmm = poisson.glmm, m = 10^3)

summary(m)

#Removed 'housed'

fec<-read.table("Ewe and Lamb FEC for R 2.txt", header=T)
summary(fec)
fec$dates<-as.Date(fec$Date, "%d/%m/%Y")

ewe<-subset(fec, fec$Age == "Ewe")
lamb<-subset(fec, fec$Age == "Lamb")

m<-glmm(Strongyle.epg ~ Date, random = list(~ 0 + Sample.name, ~ 0 + Management_event), varcomps.names=c("Sample_Name", "Management_event"),  data = ewe, family.glmm = poisson.glmm, m = 10^3)

summary(m)
```

```
# 21.01.21
# New plot for IVM vs MOX from PhD

library(ggplot2)
library(reshape2)
setwd("C:/Users/jenni/OneDrive - University of Glasgow/Working from home Mar 2020/BSAS project WORMSS/Files January 2021")

sp<-read.table("ivm_mox_epg_phd_farm_1.txt", header=T)
sp$Date<-as.factor(sp$Date)
sp$Sample<-paste(sp$fig, sp$Sample, sep=". ")
sp$Date<-paste(sp$Day, sp$Date, sep=" ")
head(sp)
summary(sp)
sp<-sp[,c(2,4:10)]
new<-melt(data = sp, id.vars = c("Sample", "Date"))
new$variable<-as.character(new$variable)

#Plot epg by species proportion over time with error bars (using SEM):

x<-ggplot(new, aes(x=Date, y=value, group=variable, color=variable)) + 
geom_line(size=1) +
geom_point(size=3)+
#geom_errorbar(aes(ymin=value-SEM, ymax=value+SEM), width=.5, position=position_dodge(0.05))+
#coord_cartesian(ylim=c(0,400)) + 
labs(y="Strongyle epg", x="Sample time point", colour="Species") +
facet_wrap(~ Sample, nrow = 1, scales='free_y')+
scale_colour_manual(values=c("grey64", "#FF00FF", "green3", "grey20", "darkorange2", "#3366FF"))+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14), legend.title=element_text(size=12), legend.text = element_text(face="italic", size=12))
x




# New plot for those colourblind:

setwd("C:/Users/jenni/Documents")
library(ggplot2)
library(reshape2)

sp<-read.table("JMPhD Farm 2 FECRT species epg .txt", header=T)
head(sp)
summary(sp)
new<-melt(data = sp, id.vars = c("Species"))
new$variable<-as.character(new$variable)
new

#Plot epg by species proportion over time with error bars (using SEM):

x<-ggplot(new, aes(x=variable, y=value, group = Species, color=Species)) + 
geom_line(aes(linetype = Species), size=1) +
geom_point(aes(shape=Species), size=3)+
labs(y="Strongyle epg", x="Sample time point", colour="Species") +
scale_colour_manual(values=c("grey64", "#FF00FF", "green3", "grey20", "darkorange2", "#3366FF"))+
theme(axis.title.x = element_text(size=14), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14), legend.title=element_text(size=12), legend.text = element_text(face="italic", size=12))
x

#Without different colours:
x<-ggplot(new, aes(x=variable, y=value, group = Species)) + 
geom_line(aes(linetype = Species), size=1) +
geom_point(aes(shape=Species), size=4, stroke = 2)+
labs(y="epg", colour="Species") +
scale_shape_manual(values=c(6, 17, 2, 3, 7))+
scale_x_discrete(labels=c("A.Pre" = "Pre-Treatment (d0)", "B.Post" = "Post-Treatment (d14)"))+   
theme(axis.title.x = element_blank(), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14), legend.title=element_text(size=12), legend.text = element_text(face="italic", size=12), legend.key.size = unit(0.75, "cm"), legend.key.width = unit(1.5,"cm"))
x

#Without different colours - with JITTER - LOL this is pointless for this particular plot!!! :
x<-ggplot(new, aes(x=variable, y=value, group = Species)) + 
geom_line(aes(linetype = Species), size=1) +
geom_point(aes(shape=Species), size=4, stroke = 2, position=position_jitter(h=0.01, w=0.01))+
labs(y="epg", colour="Species") +
scale_shape_manual(values=c(6, 17, 2, 3, 7))+
scale_x_discrete(labels=c("A.Pre" = "Pre-Treatment (d0)", "B.Post" = "Post-Treatment (d14)"))+   
theme(axis.title.x = element_blank(), axis.text.x = element_text(size=12), axis.title.y = element_text(size=14), axis.text.y = element_text(size=12), strip.text.x = element_text(size = 14), legend.title=element_text(size=12), legend.text = element_text(face="italic", size=12), legend.key.size = unit(0.75, "cm"), legend.key.width = unit(1.5,"cm"))
x
```
