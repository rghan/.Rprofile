#——————————————————————————----------------------------------------------------
## .Rprofile -  my Rprofile
#
# Inspired by the following:
# http://www.r-bloggers.com/fun-with-rprofile-and-customizing-r-startup/
# http://www.statmethods.net/interface/customizing.html
# http://www.gettinggeneticsdone.com/2013/07/customize-rprofile.html
# http://kevinushey.github.io/blog/2015/02/02/rprofile-essentials/
#——————————————————————————----------------------------------------------------
# local package library
#R_LIBS = "~/lib/R"
.libPaths("~/lib/R/")
#R_LIBS_USER=/Users/ryan/lib/R/
#R_LIBS_SITE

## assign a CRAN mirror
local({r <- getOption("repos")
      r["CRAN"] <- "https://cran.cnr.berkeley.edu/"
      options(repos=r)})

## Mimic the Python REPL to change continuation prompt to the wider ‘…’
options(prompt="> ")
options(continue="... ")

## Don’t Let R Blow Up your Console
options(max.print=100)
options(width = 80)

# fancy quotes are annoying and lead to
# 'copy + paste' bugs / frustrations
options(useFancyQuotes = FALSE)

# warn on partial matches
options(warnPartialMatchAttr = TRUE,
        warnPartialMatchDollar = TRUE,
        warnPartialMatchArgs = TRUE)

# warnings are errors
options(warn = 2)

## change default quit() to not save the workspace
#q <- function (save="no", ...) {
#  quit(save=save, ...)
#}

## Print Library Paths on Startup
if (length(.libPaths()) > 1) {
  msg <- "Using libraries at paths:\n"
} else {
  msg <- "Using library at path:\n"
}
libs <- paste("-", .libPaths(), collapse = "\n")
message(msg, libs, sep = "")

## Allow tab-complete of package names in “library()” or “require()”
utils::rc.settings(ipck=TRUE)

## Save every command run in the console into a history file
## Instruct R to, before anything else, echo a timestamp to the console and to 
## my R history file. The timestamp greatly improves my ability to search 
## through my history for relevant commands.
.First <- function(){
  if(interactive()){
    library(utils)
    cat("\nWelcome to R, ", Sys.getenv("LOGNAME"), "!\n",sep="")
    cat("-------------------\n",sep="")
    timestamp(,prefix=paste("##------ [",getwd(),"] ",sep=""))
  }
}

## Before exiting session, write all commands I used in that session to my R 
## command history file. I usually have this set in an environment variable 
## called “R_HISTFILE” on most of my systems, but in case I don’t have this 
## defined, I write it to a file in my home directory called .Rhistory.
.Last <- function(){
  if(interactive()){
    hist_file <- Sys.getenv("R_HISTFILE")
    if(hist_file=="") hist_file <- "~/.RHistory"
    savehistory(hist_file)
  }
  cat("\nGoodbye,", Sys.getenv("LOGNAME"), "!", date(), "\n")
}

if(Sys.getenv("TERM") == "xterm-256color")
  library("colorout")

sshhh <- function(a.package){
  suppressWarnings(suppressPackageStartupMessages(
    library(a.package, character.only=TRUE)))
}

auto.loads <-c("dplyr", "ggplot2")
 
if(interactive()){
  invisible(sapply(auto.loads, sshhh))
}
 
.env <- new.env()
attach(.env)
 
.env$unrowname <- function(x) {
  rownames(x) <- NULL
  x
}


message("n*** Successfully loaded .Rprofile ***n")