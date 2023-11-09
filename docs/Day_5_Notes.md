---
marp: true
---
## Day 5 : Data Visualization Fundamentals in R

![Rstudio IDE](./assets/images/ambu_v.png)
## Ambu Vijayan
### Bioinformatician
### BioLit, Thiruvananthapuram
---

# ggplot2 and iris

`install.packages("ggplot2")`

`library(ggplot2)`

`data("iris")`

`head(iris)`

---

# ggplot2

`ggplot(data=iris)`

This outputs a blank canvas.

---

# geom_point

`ggplot(data=iris) +  geom_point(mapping=aes(x=Petal.Length,y=Petal.Width))`

---

# Multiple geoms

## add a regression line

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width)) + geom_point() + geom_smooth(method="lm")`

---

# Color

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width,color=Species)) + geom_point() + geom_smooth(method="lm")`

If we wanted to keep a common regression line while keeping the colors for the points, we could specify color aesthetic only for geom_point.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width)) + geom_point(aes(color=Species)) + geom_smooth(method="lm")`

---

# Aesthetic parameter

We can change the size of all points by a fixed amount by specifying size outside the aesthetic parameter.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species),size=3)+
  geom_smooth(method="lm")`

---

# Aesthetic mapping

We can map another variable as size of the points. This is done by specifying size inside the aesthetic mapping. Now the size of the points denote Sepal.Width. A new legend group is created to show this new aesthetic.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species,size=Sepal.Width))+
  geom_smooth(method="lm")`

---

# Discrete colors

We can change the default colors by specifying new values inside a scale.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species,size=Sepal.Width))+
  geom_smooth(method="lm")+
  scale_color_manual(values=c("red","blue","green"))`

---

# Continuous colors

We can also map the colors to a continuous variable. This creates a color bar legend item.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Sepal.Width))+
  geom_smooth(method="lm")`

---

# Add and modify Labels / Titles

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Sepal.Width))+
  geom_smooth(method="lm")+
  scale_color_continuous(name="New Legend Title")+
  labs(title="This Is A Title",subtitle="This is a subtitle",x=" Petal Length", 
       y="Petal Width", caption="This is a little caption.")`

---

# Axes modification

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Sepal.Width))+
  geom_smooth(method="lm")+
  scale_color_continuous(name="New Legend Title")+
  scale_x_continuous(breaks=1:8)+
  labs(title="This Is A Title",subtitle="This is a subtitle",x=" Petal Length", 
       y="Petal Width", caption="This is a little caption.")`

---
## Facetting

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Sepal.Width))+
  geom_smooth(method="lm")+
  scale_color_continuous(name="New Legend Title")+
  scale_x_continuous(breaks=1:8)+
  labs(title="This Is A Title",subtitle="This is a subtitle",x=" Petal Length", 
       y="Petal Width", caption="This is a little caption.")+
  facet_wrap(~Species)`

---

# Themes

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Sepal.Width))+
  geom_smooth(method="lm")+
  scale_color_continuous(name="New Legend Title")+
  scale_x_continuous(breaks=1:8)+
  labs(title="This Is A Title",subtitle="This is a subtitle",x=" Petal Length", 
       y="Petal Width", caption="This is a little caption.")+
  facet_wrap(~Species)+
  theme_bw()`

---

# Controlling legends
`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species,size=Sepal.Width))`

If we don’t want to have the extra legend, we can turn off legends individually by aesthetic.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species,size=Sepal.Width))+
  guides(size="none")`

---

We can also turn off legends by geom.

ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species,size=Sepal.Width),show.legend=FALSE)

Legends can be moved around using theme.

ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species,size=Sepal.Width))+
  theme(legend.position="top",
        legend.justification="right")

---

# Labelling

### Items on the plot can be labelled using the geom_text or geom_label geoms.

`ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species))+
  geom_text(aes(label=Species,hjust=0),nudge_x=0.5,size=3)`

`  ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species))+
  geom_label(aes(label=Species,hjust=0),nudge_x=0.5,size=3)`

`ggplot(data = birthdata, mapping = aes(x = birthweight, fill = smoker)) +
geom_density(alpha = 0.5) +
scale_fill_manual(values = smoking.palette) +
labs(x = "birth weight (kg)", fill = "Maternal smoking in pregnancy") +
theme_bw()`

---

# Annotations

ggplot(data=iris,mapping=aes(x=Petal.Length,y=Petal.Width))+
  geom_point(aes(color=Species))+
  annotate("text",x=2.5,y=2.1,label="There is a random line here")+
  annotate("segment",x=2,xend=4,y=1.5,yend=2)

---

# Error Bars

The mean and standard deviation is computed. This is used to create upper and lower bounds for the error bars.

`dfr <- iris %>% group_by(Species) %>% 
  summarise(mean=mean(Sepal.Length),sd=sd(Sepal.Length)) %>%
  mutate(high=mean+sd,low=mean-sd)`

`ggplot(data=dfr,mapping=aes(x=Species,y=mean,color=Species))+
  geom_point(size=4)+
  geom_errorbar(aes(ymax=high,ymin=low),width=0.2)`

---

# Exercise

### Covid data

https://nbisweden.github.io/workshop-r/2310/lab_ggplot2.html

---

# Tidyverse

---

# Pipes

library magrittr and dplyr

my_cars <- mtcars[, c(1:4, 7)]
my_cars <- my_cars[my_cars$disp > mean(my_cars$disp), ]
print(my_cars)
my_cars <- colMeans(my_cars)

Solution : 

my_cars <- mtcars %>%
  select(c(1:4, 7)) %>%
  filter(disp > mean(disp)) %T>%
  print() %>%
  colMeans()

---

cor(mtcars)

Solution : 

mtcars %>% cor()

---

cor(mtcars$ gear, mtcars$ mpg)

Solution : 

mtcars %$% cor(gear, mpg)

---

# RNA-seq

RNA-sequence gene expression experiments

How can I access common sequence data formats from R? 
How can I use information about gene models or gene annotations in my analysis? 
How do the properties of my data influence the statistical analyses I should perform? 
What common workflows can I perform with R and Bioconductor? 
How do I deal with very large data sets in R? 

---

## Installing Necessary Packages

`install.packages(c("BiocManager", "remotes"))
BiocManager::install(c("tidyverse", "SummarizedExperiment", "hexbin",
                       "patchwork", "gridExtra", "lubridate"))`

---

We are going to use part of the data published by Blackmore et al. (2017), The effect of upper-respiratory infection on transcriptomic changes in the CNS. The goal of the study was to determine the effect of an upper-respiratory infection on changes in RNA transcription occurring in the cerebellum and spinal cord post infection. Gender matched eight week old C57BL/6 mice were inoculated with saline or with Influenza A by intranasal route and transcriptomic changes in the cerebellum and spinal cord tissues were evaluated by RNA-seq at days 0 (non-infected), 4 and 8.

---

The dataset is stored as a comma-separated values (CSV) file. Each row holds information for a single RNA expression measurement, and the first eleven columns represent:

gene	The name of the gene that was measured
sample	The name of the sample the gene expression was measured in
expression	The value of the gene expression
organism	The organism/species - here all data stem from mice
age	The age of the mouse (all mice were 8 weeks here)
sex	The sex of the mouse
infection	The infection state of the mouse, i.e. infected with Influenza A or not infected.
strain	The Influenza A strain.
time	The duration of the infection (in days).
tissue	The tissue that was used for the gene expression experiment, i.e. cerebellum or spinal cord.
mouse	The mouse unique identifier.

---

## Downloading Data

https://carpentries-incubator.github.io/bioc-intro/30-dplyr.html

`download.file(url = "https://github.com/carpentries-incubator/bioc-intro/raw/main/episodes/data/rnaseq.csv",
              destfile = "data/rnaseq.csv")`

---

## Reading Data

`rna <- read.csv("data/rnaseq.csv")`

`rna`

`head(rna)`

`View(rna)`

---

## Reading Data as Table

rna <- read.table(file = "data/rnaseq.csv",
                  sep = ",",
                  header = TRUE)

---

## Validating Data

`str(rna)`

`dim(rna)`

`nrow(rna)`

`ncol(rna)`

`head(rna)`

`tail(rna)`

`names(rna)`

`rownames(rna)`

`summary(rna)`

---

## Exporting and saving tabular data

`write.csv(rna, file = "data_output/my_rna.csv")`

---

## Data manipulation

BiocManager::install("tidyverse")

library("tidyverse")

---

## Loading data with tidyverse

rna <- read_csv("data/rnaseq.csv")

rna

---

### We are now going to learn some of the most common dplyr functions:

select(): subset columns
filter(): subset rows on conditions
mutate(): create new columns by using information from other columns
group_by() and summarise(): create summary statistics on grouped data
arrange(): sort results
count(): count discrete values

---

## Selecting columns and filtering rows

`select(rna, gene, sample, tissue, expression)`

`select(rna, -tissue, -organism)`

`filter(rna, sex == "Male")`

`filter(rna, sex == "Male" & infection == "NonInfected")`

`genes <- select(rna, gene, hsapiens_homolog_associated_gene_name)`
`genes`

`filter(genes, is.na(hsapiens_homolog_associated_gene_name))`

`filter(genes, !is.na(hsapiens_homolog_associated_gene_name))`

---

## Pipes : select and filter at the same time

rna2 <- filter(rna, sex == "Male")
rna3 <- select(rna2, gene, sample, tissue, expression)
rna3

rna3 <- select(filter(rna, sex == "Male"), gene, sample, tissue, expression)
rna3

rna3 <- rna %>%
  filter(sex == "Male") %>%
  select(gene, sample, tissue, expression)

rna3

---

## Pipes : Mutate

rna %>%
  mutate(time_hours = time * 24) %>%
  select(time, time_hours)

rna %>%
  mutate(time_hours = time * 24,
         time_mn = time_hours * 60) %>%
  select(time, time_hours, time_mn)

---

## Split-apply-combine data analysis

rna %>%
  group_by(gene)

rna %>%
  group_by(sample)

---

## The summarise() function

rna %>%
  group_by(gene) %>%
  summarise(mean_expression = mean(expression))

rna %>%
  group_by(sample) %>%
  summarise(mean_expression = mean(expression))

rna %>%
  group_by(gene, infection, time) %>%
  summarise(mean_expression = mean(expression))

---

rna %>%
  group_by(gene, infection, time) %>%
  summarise(mean_expression = mean(expression),
            median_expression = median(expression))

---

## Counting

rna %>%
    count(infection)

rna %>%
    group_by(infection) %>%
    summarise(n = n())

rna %>%
    count(infection, time)

rna %>%
  group_by(infection, time) %>%
  summarise(n = n())

---

rna %>%
  count(infection, time) %>%
  arrange(time)

rna %>%
  count(infection, time) %>%
  arrange(n)

rna %>%
  count(infection, time) %>%
  arrange(desc(n))

---

## Reshaping data

rna %>%
  arrange(gene)

### Pivoting the data into a wider format

rna_exp <- rna %>%
  select(gene, sample, expression)
rna_exp

---

rna_wide <- rna_exp %>%
  pivot_wider(names_from = sample,
              values_from = expression)
rna_wide

rna_long <- rna_wide %>%
    pivot_longer(names_to = "sample",
                 values_to = "expression",
                 -gene)
rna_long

---

rna_wide %>%
    pivot_longer(names_to = "sample",
                 values_to = "expression",
                 cols = starts_with("GSM"))

rna_wide %>%
    pivot_longer(names_to = "sample",
                 values_to = "expression",
                 GSM2545336:GSM254538

rna_with_missing_values

---

wide_with_NA <- rna_with_missing_values %>%
  pivot_wider(names_from = sample,
              values_from = expression)
wide_with_NA

wide_with_NA %>%
    pivot_longer(names_to = "sample",
                 values_to = "expression",
                 -gene)

---

## Joining tables

rna_mini <- rna %>%
   select(gene, sample, expression) %>%
   head(10)
rna_mini

download.file(url = "https://carpentries-incubator.github.io/bioc-intro/data/annot1.csv",
              destfile = "data/annot1.csv")
annot1 <- read_csv(file = "data/annot1.csv")
annot1

---

full_join(rna_mini, annot1)

download.file(url = "https://carpentries-incubator.github.io/bioc-intro/data/annot2.csv",
              destfile = "data/annot2.csv")
annot2 <- read_csv(file = "data/annot2.csv")
annot2

---

full_join(rna_mini, annot2, by = c("gene" = "external_gene_name"))

---

## Exporting data

write_csv(rna_wide, file = "data_output/rna_wide.csv")

---

# Data Visualization

library("tidyverse")

rna <- read.csv("data/rnaseq.csv")

ggplot(data = <DATA>, mapping = aes(<MAPPINGS>)) +  <GEOM_FUNCTION>()

---

ggplot(data = rna)

ggplot(data = rna, mapping = aes(x = expression))

ggplot(data = rna, mapping = aes(x = expression)) +
  geom_histogram()

### Assign plot to a variable
rna_plot <- ggplot(data = rna,
                   mapping = aes(x = expression))

### Draw the plot
rna_plot + geom_histogram()

---

rna <- rna %>%
  mutate(expression_log = log2(expression + 1))

ggplot(rna, aes(x = expression_log)) + geom_histogram()

---

rna_fc <- rna %>% select(gene, time,
                         gene_biotype, expression_log) %>%
  group_by(gene, time, gene_biotype) %>%
  summarize(mean_exp = mean(expression_log)) %>%
  pivot_wider(names_from = time,
              values_from = mean_exp) %>%
  mutate(time_8_vs_0 = `8` - `0`, time_4_vs_0 = `4` - `0`)

---

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0)) +
  geom_point()

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0)) +
  geom_point(alpha = 0.3)

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0)) +
  geom_point(alpha = 0.3, color = "blue")

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0)) +
  geom_point(alpha = 0.3, aes(color = gene_biotype))

---

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0,
                                color = gene_biotype)) +
  geom_point(alpha = 0.3)

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0,
                                color = gene_biotype)) +
  geom_point(alpha = 0.3) +
  geom_abline(intercept = 0)

ggplot(data = rna_fc, mapping = aes(x = time_4_vs_0, y = time_8_vs_0,
                                color = gene_biotype)) +
  geom_jitter(alpha = 0.3) +
  geom_abline(intercept = 0)

---

ggplot(data = rna,
         mapping = aes(y = expression_log, x = sample)) +
  geom_boxplot()

ggplot(data = rna,
         mapping = aes(y = expression_log, x = sample)) +
  geom_jitter(alpha = 0.2, color = "tomato") +
  geom_boxplot(alpha = 0)

ggplot(data = rna,
         mapping = aes(y = expression_log, x = sample)) +
  geom_jitter(alpha = 0.2, color = "tomato") +
  geom_boxplot(alpha = 0) +
  theme(axis.text.x = element_text(angle = 90,  hjust = 0.5, vjust = 0.5))

---

## Line plots

rna_fc <- rna_fc %>% arrange(desc(time_8_vs_0))

genes_selected <- rna_fc$gene[1:10]

sub_rna <- rna %>%
    filter(gene %in% genes_selected)

mean_exp_by_time <- sub_rna %>%
  group_by(gene,time) %>%
    summarize(mean_exp = mean(expression_log))

---

mean_exp_by_time

ggplot(data = mean_exp_by_time, mapping = aes(x = time, y = mean_exp)) +
  geom_line()

ggplot(data = mean_exp_by_time,
       mapping = aes(x = time, y = mean_exp, group = gene)) +
  geom_line()

ggplot(data = mean_exp_by_time,
       mapping = aes(x = time, y = mean_exp, color = gene)) +
  geom_line()

---

## Faceting

ggplot(data = mean_exp_by_time,
       mapping = aes(x = time, y = mean_exp)) + geom_line() +
  facet_wrap(~ gene)

ggplot(data = mean_exp_by_time,
       mapping = aes(x = time, y = mean_exp)) +
  geom_line() +
  facet_wrap(~ gene, scales = "free_y")

mean_exp_by_time_sex <- sub_rna %>%
  group_by(gene, time, sex) %>%
    summarize(mean_exp = mean(expression_log))

---

mean_exp_by_time_sex

ggplot(data = mean_exp_by_time_sex,
       mapping = aes(x = time, y = mean_exp, color = sex)) +
  geom_line() +
  facet_wrap(~ gene, scales = "free_y")

ggplot(data = mean_exp_by_time_sex,
       mapping = aes(x = time, y = mean_exp, color = sex)) +
  geom_line() +
  facet_wrap(~ gene, scales = "free_y") +
  theme_bw() +
  theme(panel.grid = element_blank())

---

##  One column, facet by rows

ggplot(data = mean_exp_by_time_sex,
       mapping = aes(x = time, y = mean_exp, color = gene)) +
  geom_line() +
  facet_grid(sex ~ .)

---

## One row, facet by column
ggplot(data = mean_exp_by_time_sex,
       mapping = aes(x = time, y = mean_exp, color = gene)) +
  geom_line() +
  facet_grid(. ~ sex)

---

https://carpentries-incubator.github.io/bioc-intro/60-next-steps.html





