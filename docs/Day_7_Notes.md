---
marp: true
---
# Day 7 : Volcano Plots in R
![Rstudio IDE](./assets/images/ambu_v.png)
## Ambu Vijayan
### Bioinformatician
### BioLit, Thiruvananthapuram
---

## A volcano plot is a type of scatter plot represents differential expression of features (genes for example): on the x-axis we typically find the fold change and on the y-axis the p-value..

---
# R packages and data

### Import data
`data <- read_tsv("https://raw.githubusercontent.com/sdgamboa/misc_datasets/master/L0_vs_L20.tsv")`

`dim(data)`

---

# A simple volcano plot

`p1 <- ggplot(data, aes(logFC, -log(FDR,10))) + # -log10 conversion  
  geom_point(size = 2/5) +
  xlab(expression("log"[2]*"FC")) + 
  ylab(expression("-log"[10]*"FDR"))`

`p1`

---

The dispersion of the points (representing genes) in the plot is similar to, you guessed, a volcano (that’s why they’re called volcano plots). Since the FDR values were transformed to their -log10, the higher the position of a point, the more significant its value is (y axis). Points with positive fold change values (to the right) are up-regulated and points with negative fold change values (to the left) are down-regulated (x axis).

---

# Adding color to differentially expressed genes (DEGs)

Differentially expressed genes (DEGs) are usally considered as those with an absolute fold change greater or equal to 2 and a FDR value of 0.05 or less.

So, we can make our volcano plot a bit more informative if we add some color to the DEGs in the plot.

To do so, we’ll add an additional column, named ‘Expression’, indicating whether the expression of a gene is up-regulated, down-regulated, or unchanged:

---

`data <- data %>% 
  mutate(
    Expression = case_when(logFC >= log(2) & FDR <= 0.05 ~ "Up-regulated",
                           logFC <= -log(2) & FDR <= 0.05 ~ "Down-regulated",
                           TRUE ~ "Unchanged")
    )`


`head(data)`

---
We can now map the column ´Expression’ to the color aesthetic of geom_point() and color the points according to their expression classification:

`p2 <- ggplot(data, aes(logFC, -log(FDR,10))) +
  geom_point(aes(color = Expression), size = 2/5) +
  xlab(expression("log"[2]*"FC")) + 
  ylab(expression("-log"[10]*"FDR")) +
  scale_color_manual(values = c("dodgerblue3", "gray50", "firebrick3")) +
  guides(colour = guide_legend(override.aes = list(size=1.5))) `

`p2`

---

If we want to know how many genes are up- or down-regulated, or unchanged, we can use dplyr’s count() function.

data %>% 
  count(Expression)

---

Since we already know that the genes towards the right are up-regulated and the genes towards the left are down-regulated, it would be more informative if we colored the points according to their significance level instead. Let’s create another column, named ‘Significance’, and classify the genes according to significance thresholds (0.05, 0.01, and 0.001):

    data <- data %>% 
    mutate(
        Significance = case_when(
        abs(logFC) >= log(2) & FDR <= 0.05 & FDR > 0.01 ~ "FDR 0.05", 
        abs(logFC) >= log(2) & FDR <= 0.01 & FDR > 0.001 ~ "FDR 0.01",
        abs(logFC) >= log(2) & FDR <= 0.001 ~ "FDR 0.001", 
        TRUE ~ "Unchanged")
    )

`head(data)`

---
Again, we can use the color aesthetic to map the color of the points to their corresponding significance thresholds:

`p3 <- ggplot(data, aes(logFC, -log(FDR,10))) +
  geom_point(aes(color = Significance), size = 2/5) +
  xlab(expression("log"[2]*"FC")) + 
  ylab(expression("-log"[10]*"FDR")) +
  scale_color_viridis_d() +
  guides(colour = guide_legend(override.aes = list(size=1.5)))` 

`p3`

---

And we can count how many genes are up- or down-regulated according to the different significance thresholds with count():

`data %>% 
  count(Expression, Significance)`

---

## Adding labels to selected genes

`top <- 10`

`top_genes <- bind_rows(
  data %>% 
    filter(Expression == 'Up-regulated') %>% 
    arrange(FDR, desc(abs(logFC))) %>% 
    head(top),
  data %>% 
    filter(Expression == 'Down-regulated') %>% 
    arrange(FDR, desc(abs(logFC))) %>% 
    head(top)
)`

`top_genes`

`p3 <-  p3 +
  geom_label_repel(data = top_genes,
                   mapping = aes(logFC, -log(FDR,10), label = Genes),
                   size = 2)`

`p3`

So, only the top 10 up- and down-regulated genes are labeled, avoiding overcrowding.

---

