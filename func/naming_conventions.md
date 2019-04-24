## Task imaging data

Task based fmri require a corresponding task events file (similar to the behavioral events file). These files are generated using the dcm2bids conversion, you will need to however open the .json files and include the TaskName by hand. 

  1) sub-<participant_label>[_ses-<session_label>]_task-<task_label>[_acq-<label>][_rec-<label>][_run-<index>][_echo-<index>]_bold.nii[.gz]
  
  2) sub-<participant_label>[_ses-<session_label>]_task-<task_label>[_acq-<label>][_rec-<label>][_run-<index>][_echo-<index>]_bold.json
  
  
Common types of imaging our lab does:



| Name  | Label | Description |
| ------------- | ------------- |------------- |
|                |   rec           |    Key/value used to distinguish different reconstruction algorithms           |
|                |  acq            |    key/value pair corresponds to custom label to distinguish different set of parameters used for acquiring the same task |
|                |     echo         |     Number/index, multi echo data must be split into one file per echo; each file shares the same name          |





Some meta information about the acquisition MUST be provided in an additional JSON file.
**Required fields:**


● RepetitionTime: The time in seconds between the beginning of an acquisition of one volume and the
beginning of acquisition of the volume following it (TR). Please note that this definition includes time
between scans (when no data has been acquired) in case of sparse acquisition schemes. This value needs
to be consistent with the ‘pixdim[4]’ field (after accounting for units stored in ‘xyzt_units’ field) in the
NIfTI header. This field is mutually exclusive with VolumeTiming and is derived from DICOM Tag 0018,
0080 and converted to seconds.

● VolumeTiming: The time at which each volume was acquired during the acquisition. It is described
using a list of times (in JSON format) referring to the onset of each volume in the BOLD series. The list must
have the same length as the BOLD series, and the values must be non-negative and monotonically
increasing. This field is mutually exclusive with RepetitionTime and DelayTime. If defined, this
requires acquisition time (TA) be defined via either SliceTiming or AcquisitionDuration be
defined.

● TaskName: Name of the task. No two tasks should have the same name. Task label (
“task-<task_label>”) included in the file name is derived from this field by removing all non
alphanumeric ([a-zA-Z0-9]) characters. For example task name “faces n-back” will corresponds to task
label “facesnback”. An optional but recommended convention is to name resting state task using labels
beginning with "rest".


For the fields described above, the term “Volume” refers to a reconstruction of the
object being imaged (e.g., brain or part of a brain). In case of multiple channels in a coil, the term “Volume” refers to
a combined image rather than an image from each coil.
