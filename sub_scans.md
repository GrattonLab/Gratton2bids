Template
sub-<participant_label>/[ses-<session_label>/]
sub-<participant_label>[_ses-<session_label>]_scans.tsv

The purpose of this file is to describe timing and other properties of each imaging acquisition sequence (each run
.nii[.gz] file) within one session. Each .nii[.gz] file should be described by at most one row. Relative paths
to files should be used under a compulsory “filename” header.
If acquisition time is included it should be under “acq_time” header. Datetime should be expressed in the
following format 2009-06-15T13:45:30 (year, month, day, hour (24h), minute, second; this is equivalent to
the RFC3339 “date-time” format, time zone is always assumed as local time). For anonymization purposes all
dates within one subject should be shifted by a randomly chosen (but common across all runs etc.) number of days.
This way relative timing would be preserved, but chances of identifying a person based on the date and time of
their scan would be decreased. Dates that are shifted for anonymization purposes should be set to a year 1900 or
earlier to clearly distinguish them from unmodified data. Shifting dates is recommended, but not required.
Additional fields can include external behavioural measures relevant to the scan. For example vigilance
questionnaire score administered after a resting state scan.


an example of this would look like
|filename | acq_time |
| ------------- | ------------- |
|func/sub-control01_task-nback_bold.nii.gz | 1877-06-15T13:45:30 |
