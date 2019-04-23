Place .Rmd files of analyses here.
devtools::install_github("waldronlab/bugSigSimple")
library(bugSigSimple)
dat <- readCurationSheet("C:/Users/stath/Downloads/Microbial signatures curation - signatures (6).tsv")
dim(dat)
dat[1:5,1:5]

# print the column names of mydata2
names(dat)
names(dat)[23] <- "contrast"


# #my.contrasts<-c("taxons associated with BMI", "obese vs. controls",
"obese adolescent vs. control adolescent", "obese adolescent vs. control adult",
"obese adult vs. control adolescent","obese adult vs. control adult")

unique(dat$contrast)
my.contrasts <- unique(dat$contrast)[c(72, 109, 122, 123, 124, 125, 142, 144,
                                       146, 147, 188, 189, 199, 200, 230, 232,
                                       148)]

my.pubmed.ids<-c("21829158", "302574444", "28628112", "30867711", "27499582",
                 "30568265", "25764541", "23032991", "23526699", "30669548",
                 "29388394", "29988340", "29950689", "30054529", "26230509",
                 "27007700", "27450202", "29922272", " 26261039", "27228093",
                 "29576948")


# writing the condition for filtering by contrast
# ind1<-dat[,"contrast..list.control.group.last."] %in%
#   my.contrasts

# filtering by contrast
# my.dat<-dat[ind1 ,]

# FILTER BY constrast
my.dat <- subset(dat, contrast %in% my.contrasts)
# now, my.dat is a subset of dat 

# FILTER BY PMID 

# writing the condition for filtering by pmid
# ind2<-dat[, "PMID"]%in%
#   my.pubmed.ids
# 
# my.dat<-dat[ind1 & ind2,]

my.dat1 <- subset(my.dat, PMID %in% my.pubmed.ids)
# now, my.dat1 is a subset of my.dat


# FILTER BY condition
# my.dat <- subsetByCondition(dat, condition="obesity")

my.dat2 <- subset(my.dat1, condition %in% "obesity")


getMostFrequentTaxa(my.dat2, n=25)
getMostFrequentTaxa(my.dat2, sig.type="UP", n=10)
getMostFrequentTaxa(my.dat2, sig.type="DOWN", n=10)


my.dat2 <- subsetByCurator(my.dat, curator="Marianthi Thomatos")
dim(my.dat2)





