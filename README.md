# EC331
###Output my data set###
#Huihan Zhang

# Load and install packages, note the new packages
installation_needed  <- TRUE
loading_needed <- TRUE
package_list <- c('foreign', 'xtable', 'plm','gmm', 'AER','stargazer','readstata13', 'ggplot2',
                  'boot', 'arm', 'lmtest', 'sem', 'bdynsys', 'ivpack', 'mfx', 'glm2','plyr')
if(installation_needed){install.packages(package_list, repos='http://cran.us.r-project.org')}
if(loading_needed){lapply(package_list, require, character.only = TRUE)}

# clear the global workspace
rm(list=ls())

# set working directory (only works on my computer)
# uncomment this before running the codes
setwd("/Users/apple/Documents/LSE 3RD YEAR/EC331/data/MasterData")

# load raw data -- Chinese Household Income Project urban survey 2002
# downloaded from "https://www.icpsr.umich.edu/icpsrweb/ICPSR/series/243"
mydata <- read.dta13("/Users/apple/Documents/LSE 3RD YEAR/EC331/data/Raw Data.dta") 

# select variables of interest
mydata <- mydata[c("CITY","PCODE","CODE_P","P103","P104","P105","P106","P108","P113","PROVINCE")]

# rename variables 
mydata <- rename(mydata, c("PCODE"="HHID","CODE_P"="INDID","P103"="relationship", "P104"="hukou", "P105"="female", "P106"="age", "P108"="ethnicity", "P113"="schooling"))

# I'm going to restrict my data to age >= 22, so that most of them have completed university education
mydata <- mydata[mydata$age >= 22,]
