## Judgement experiment script

The script below does three things:

1. Collects personal information of a given participant
2. Runs a judgement experiment ([`ExperimentMFC`](http://www.fon.hum.uva.nl/praat/manual/ExperimentMFC_3_1__A_simple_discrimination_experiment.html))
3. Reads a `csv` file containing the linguistic variables of interest
4. Combines personal info, linguistic variables, and experimental responses into a single `csv` table ready for analysis

Each participant will have a `csv` file, which you can later easily bind in R, for example.

### Requirements

To run this script you'll need:

A. An experiment file (`*.txt`) (see (2) above)    
B. A `csv` file with your linguistic variables

Finally, you'll probably want to change the paths in the script. The script assumes (A) and (B) above are in the same directory as the script itself. A folder (`output`) is also assumed to be present. The script does not use the `createDirectory` command on Praat, so you can run the exact same script for every participant.

**Important**: One of the fields in the questionnaire can be used to identify each participant (`username`). Note that if you repeat the `username`, Praat will **overwrite** the file. So just make sure to assign unique `username`s.

```

#====================================================
#
#	2017 Guilherme D. Garcia (McGill University)
#	www.guilherme.ca
#	guilherme.garcia@mail.mcgill.ca
#
#====================================================

### OBJECTIVE: collect data and running experiments

### OUTPUT: complete csv file with personal info, linguistic variables and responses

### REQUIREMENTS:

###### MFC Experiment file (txt) and associated files
###### csv file with lingustic variables (ling.csv); number of rows must match number of stimuli/trials


#==========================
#========================== QUESTIONNAIRE
#==========================


form Welcome!

	comment Thanks for participating in our study. Please, answer the following questions.
	comment IMPORTANT: Do not use punctuation in your answers.
	comment 
    sentence Name name
	sentence Email email
	optionmenu Native_language 1
		option English
		option French
		option Portuguese
		option Other
	sentence Username your ID
    natural Age 99
	optionmenu Gender 1
		option Female
		option Male
		option Other
	choice Do_you_speak_other_languages 1
		button No
    	button Yes
	optionmenu Level_of_education 2
		option High school
		option College
		option Bachelors Degree
		option Master's/PhD
	optionmenu Proficiency_in_English 1
		option Beginner
		option Intermediate
		option Advanced
		option Proficient
		option Native
	optionmenu Years_in_Montreal 1
		option 0-1
		option 1-2
		option 2-5
		option 5-10
		option 10-20

endform


#==========================
#========================== SHORTEN LONG VARIABLES
#==========================


lang$ = do_you_speak_other_languages$

english$ = proficiency_in_English$

montreal$ = years_in_Montreal$


#==========================
#========================== GATHER PERSONAL VARIABLES
#==========================


personal_variables$ = "ID name age email L1 gender education lang english years_montreal"


#==========================
#========================== READ EXPERIMENT FILE
#==========================


Read from file: "experiment_file.txt"


#==========================
#========================== RUN EXPERIMENT
#==========================


Run

beginPause: "For internal use only."


endPause: "Cancel", "Conclude experiment", 2, 1


#==========================
#========================== EXTRACT RESULTS
#==========================


Extract results

Collect to Table


#==========================
#========================== CREATE MAIN TABLE STARTING WITH PERSONAL INFORMATION
#==========================


selectObject: "Table allResults"
nrows_experiment = Get number of rows
ncols_experiment = Get number of columns

Create Table with column names: "output", nrows_experiment, personal_variables$

for i to nrows_experiment
	selectObject: "Table output"
	Set string value: i, "name", name$
	Set numeric value: i, "age", age
	Set string value: i, "email", email$
	Set string value: i, "L1", native_language$
	Set string value: i, "ID", username$
	Set string value: i, "gender", gender$
	Set string value: i, "education", level_of_education$
	Set string value: i, "lang", lang$
	Set string value: i, "english", english$
	Set string value: i, "years_montreal", montreal$
endfor


#==========================
#========================== READ CSV FILE CONTAINING LINGUISTIC INFORMATION
#==========================


Read Table from comma-separated file: "ling.csv"


#==========================
#========================== GET GENERAL INFO ON FILE (NUMBER OF ROWS ETC)
#==========================


selectObject: "Table ling"
nrows_ling = Get number of rows
ncols_ling = Get number of columns


#==========================
#========================== NOW FOR LOOP TO FILL COLUMNS WITH LING VARIABLES
#==========================


for col from 1 to ncols_ling
	
	selectObject: "Table ling"
	label$[col] = Get column label: col

	selectObject: "Table output"
	Append column: label$[col]

	for row from 1 to nrows_ling
		selectObject: "Table ling"
		temp$ = Get value: row, label$[col]
		selectObject: "Table output"
		Set string value: row, label$[col], temp$
	endfor

endfor


#==========================
#========================== NOW FOR LOOP TO ADD EXPERIMENTAL RESULTS
#==========================


### Looping begins at 2 to remove Subject column ('file name'), 
### which is redundant given ID and name variables
### To remove stimulus column as well, start from 3

for col from 2 to ncols_experiment
	
	selectObject: "Table allResults"
	label$[col] = Get column label: col

	selectObject: "Table output"
	Append column: label$[col]

	for row from 1 to nrows_experiment
		selectObject: "Table allResults"
		temp$ = Get value: row, label$[col]
		selectObject: "Table output"
		Set string value: row, label$[col], temp$
	endfor

endfor




#==========================
#========================== SAVE FINAL TABLE AND EXPORT IT AS CSV (FILE NAME = USER ID)
#==========================


Save as comma-separated file: "output/" + username$ + ".csv"


#==========================
#========================== CLEAN OBJECT WINDOW
#==========================


select all
Remove

```
