Template:
sub-<participant_label>/
sub-<participant_label>_sessions.tsv
Optional: Yes
In case of multiple sessions there is an option of adding an additional participant key files describing variables
changing between sessions. In such case one file per participant should be added. These files need to include
compulsory “session_id” column and describe each session by one and only one row. Column names in per
participant key files have to be different from group level participant key column names.


example 
|session_id| acq_time| systolic_blood_pressure|
| ---------| --------|------------------------|
|ses-predrug| 2009-06-15T13:45:30 |120|
|ses-postdrug |2009-06-16T13:45:30 |100|
|ses-followup |2009-06-17T13:45:30 |110|
