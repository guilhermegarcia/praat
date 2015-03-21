### Judgement/perception task on Praat


This was an experiment I developed for a [study](https://www.dropbox.com/s/57wtimqjvwzambw/OCP.pdf?dl=0) on neoclassical elements (with [Natália B. Guzzo](http://www.nataliaguzzo.wordpress.com), presented at OCP 12, 2015).
Basically, speakers hear a word and rate it on a 10-point scale. An 'OK' button was added so that accidental ratings wouldn't occur.
This script also allows subjects to press 'space' and hear the stimulus again (2 repetitions max). Since all participants were
Portuguese speakers, the instructions are in Portuguese, but the structure should be fairly straightforward.  
Originally, there were 202 stimuli (as you can see from the code below). If you're not familiar with Praat experiments, what follows ```202``` below are the stimuli pairs (each stimulus here had a file and a word that appeared on the screen). 


```


"ooTextFile"
"ExperimentMFC 6"
blankWhilePlaying? <no>
stimuliAreSounds? <yes>
stimulusFileNameHead = "sounds/"
stimulusFileNameTail = ".wav"
stimulusCarrierBefore = ""
stimulusCarrierAfter = ""
stimulusInitialSilenceDuration = 0.5 seconds
stimulusMedialSilenceDuration = 0
stimulusFinalSilenceDuration = 0.5 seconds
numberOfDifferentStimuli = 202
    "file_name"            "wordOnScreen"
    ...                 ...
numberOfReplicationsPerStimulus = 2
breakAfterEvery = 202
randomize = <CyclicNonRandom>
startText = "Este é um experimento de pronúncia. Queremos saber sua opinião 
sobre a pronúncia de diversas palavras. Após ouvir a palavra, dê uma nota 
de 1 (péssima) a 10 (ótima). Uma ótima pronúncia é uma pronúncia que você
ouve com frequência; uma péssima pronúncia é uma pronúncia 
que você nunca (ou quase nunca) ouve.

Você poderá ouvir cada palavra até 3 vezes: basta utilizar 
a barra de espaços para repetir a palavra desejada.

Natália B. Guzzo (UFRGS/CNPq)
Guilherme D. Garcia (McGill University)

Clique para iniciar."
runText = "Dê uma nota à pronúncia que você ouvir."
pauseText = "Você pode fazer um pequeno intervalo. Clique para prosseguir."
endText = "Obrigado."
maximumNumberOfReplays = 2
replayButton = 0.1 0.9 0.01 0.07 "Pressione a barra de espaço para ouvir novamente" " "
okButton = 0.45 0.55 0.7 0.8 "OK" "o"
oopsButton = 0 0 0 0 "" ""
responsesAreSounds? <no> "" "" "" "" 0 0 0
numberOfDifferentResponses = 10
    0.25 0.3 0.4 0.5 "1" 30 "1" "1"
    0.3 0.35 0.4 0.5 "2" 30 "2" "2"
    0.35 0.4 0.4 0.5 "3" 30 "3" "3"
    0.4 0.45 0.4 0.5 "4" 30 "4" "4"
    0.45 0.5 0.4 0.5 "5" 30 "5" "5"
    0.5 0.55 0.4 0.5 "6" 30 "6" "6"
    0.55 0.6 0.4 0.5 "7" 30 "7" "7"
    0.6 0.65 0.4 0.5 "8" 30 "8" "8"
    0.65 0.7 0.4 0.5 "9" 30 "9" "9"
    0.7 0.75 0.4 0.5 "10" 30 "0" "10"
numberOfGoodnessCategories = 0
    0.25 0.15 0.10 0.20 "1"
    0.35 0.25 0.10 0.20 "2"
    0.45 0.35 0.10 0.20 "3"
    0.55 0.45 0.10 0.20 "4"
    0.65 0.55 0.10 0.20 "5"
    0.75 0.65 0.10 0.20 "6"
    0.85 0.75 0.10 0.20 "7"

```
