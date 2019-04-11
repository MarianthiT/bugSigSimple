Place .Rmd files of analyses here.


devtools::install_github("waldronlab/bugSigSimple")
library(bugSigSimple)
dat <- readCurationSheet("C:/Users/stath/Downloads/Microbial signatures curation - signatures (4).tsv")
dim(dat)
dat[1:5,1:5]

# print the column names of mydata2
names(dat)
names(dat)[23] <- "contrast"


# #my.contrasts<-c("obese adolescent vs. control 1", "obese adolescent vs. control adolescent 1", 
#                 "obese adult vs. control adolescent 1", 
#                 "obese adult vs. control adult 1",
#                 "Bacterial taxa correlated with pediatric BMI", 
#                 "Korean obese adolescent vs. controls", 
#                 "obese vs. controls", "obese vs. controls 2")
unique(dat$contrast)
my.contrasts <- unique(dat$contrast)[c(72, 109, 189, 122, 123, 124, 125, 142, 144, 146,
                                       147, 149, 190, 197, 198, 199, 200, 201, 202)]

my.pubmed.ids<-c("27228093", "29922272", "27450202", "26230509", "29950689",
                 "29388394", "30669548", "23526699", "29388394", "29576948", 
                 "30054529", "26261039", "21829158", "27007700", "25710027", 
                 "27306058", "23032991")

my.pubmed.ids2<-c("23032991", "27306058", "25710027")


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
my.dat3 <- subset(my.dat, PMID %in% my.pubmed.ids2)
# now, my.dat1 is a subset of my.dat


# FILTER BY condition
# my.dat <- subsetByCondition(dat, condition="obesity")

my.dat2 <- subset(my.dat1, condition %in% "obesity")
mydat4<- subset(my.dat3, condition %in% "obesity")

getMostFrequentTaxa(my.dat2, n=25)
getMostFrequentTaxa(my.dat2, sig.type="UP", n=10)
getMostFrequentTaxa(my.dat2, sig.type="DOWN", n=10)


getMostFrequentTaxa(mydat4, n=10)
getMostFrequentTaxa(mydat4, sig.type="UP", n=5)
getMostFrequentTaxa(mydat4, sig.type="DOWN", n=5)

my.dat2 <- subsetByCurator(my.dat, curator="Marianthi Thomatos")
dim(my.dat2)




