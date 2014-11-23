rCourseraTidydata
=================

containing the run_analysis.R

## run_analysis.R
This script contains a single function (run_analysis) that computes a tidy data set from the raw data provided in the getting and cleaning data course.

The function run_analysis computes averages of all variables that contain the strings mean and std for all subjects and all activity conditions. Since the task was to give out a single table, the first column contains all the subjects followed by all the conditions. The other (many) columns contain the average values of the corresponding variables, each named after the original information contained in the data provided in the course.

Remember to set the working directory on the folder in which you store the data for testing.

See also the code book for the variable names and (minimal) info.
