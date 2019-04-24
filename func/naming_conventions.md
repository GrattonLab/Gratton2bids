## Task imaging data

Task based fmri require a corresponding task events file (similar to the behavioral events file). These files are generated using the dcm2bids conversion, you will need to however open the .json files and include the TaskName by hand. 

  1) sub-<participant_label>[_ses-<session_label>]_task-<task_label>[_acq-<label>][_rec-<label>][_run-<index>][_echo-<index>]_bold.nii[.gz]
  
  2) sub-<participant_label>[_ses-<session_label>]_task-<task_label>[_acq-<label>][_rec-<label>][_run-<index>][_echo-<index>]_bold.json
  
  
Common types of imaging our lab does:



| Name  | Label | Description |
| ------------- | ------------- |------------- |
|                |   rec           |    Key/value used to distinguish different reconstruction algorithms           |
|                |  acq            |    key/value pair corresponds to custom label to distinguish diefferent set of parameters used for acquiring the same task |
|                |     echo         |     Number/index, multi echo data must be split into one file per echo; each file shares the same name          |
