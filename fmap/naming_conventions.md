## Fieldmaps 

  1) sub-<label>[_ses-<session_label>][_acq-<label>][_run-<run_index>]_phasediff.nii[.gz]
  2) sub-<label>[_ses-<session_label>][_acq-<label>][_run-<run_index>]_phasediff.json
  3) sub-<label>[_ses-<session_label>][_acq-<label>][_run-<run_index>]_magnitude1.nii[.gz]

Data acquired to correct for B0 inhomogeneities can come in different forms. The current version of this standard
considers four different scenarios. Please note that in all cases fieldmap data can be linked to a specific scan(s) it
was acquired for by filling the IntendedFor field in the corresponding JSON file. For example:

{
"IntendedFor": "func/sub-01_task-motor_bold.nii.gz"
}

The IntendedFor field may contain one or more filenames with paths relative to the subject subfolder. The path
needs to use forward slashes instead of backward slashes. Here’s an example with multiple target scans:

{
"IntendedFor": ["ses-pre/func/sub-01_task-motor_run-1_bold.nii.gz",
"ses-post/func/sub-01_task-motor_run-1_bold.nii.gz"]
}

The IntendedFor field is optional and in case the fieldmaps do not correspond to any particular scans it does not
have to be filled.

Multiple fieldmaps can be stored. In such case the “_run-1”, “_run-2” should be used. The optional
“acq-<label>” key/value pair corresponds to a custom label the user may use to distinguish different set of
parameters.

Common fieldmaps our lab uses 

| Name | Label | Description |
|------|------|--------------|
|      | acq     |            |
| .     | phasediff |         |
| phase encoding polarity| dir- | The phase-encoding polarity (PEpolar) technique combines two or more Spin Echo EPI scans with different phase encoding directions to estimate the underlying inhomogeneity/deformation map. Examples of tools using this kind of images are FSL TOPUP, AFNI 3dqwarp and SPM . In such a case, the phase encoding direction is specified in the corresponding JSON file as one of: “i”, “j”, “k”, “i-”, “j-, “k-”. For these differentially phase encoded sequences, one also needs to specify the Total Readout Time defined as the time (in seconds) from the center of the first echo to the center of the last echo (aka “FSL definition” - see here and here how to calculate it). Our lab lists out the direction of the phase so an example would be dir-AP|
| B0 inhomogeneity     | fieldmap | In some cases (for example GE) the scanner software will output a precomputed fieldmap denoting the B0 inhomogeneities along with a magnitude image used for coregistration. In this case the sidecar JSON file needs to include the units of the fieldmap. The possible options are: “Hz”, “rad/s”, or “Tesla”.  |
| .      | phase2       | two separate phase images are presented. The two sidecar JSON file need to specify corresponding EchoTime values.    |
|    |  magnitude2      | This is a common output for build in fieldmap sequence on Siemens scanners. In this particular case the sidecar JSON file has to define the Echo Times of the two phase images used to create the difference image. EchoTime1 corresponds to the shorter echo time and EchoTime2 to the longer echo time. Similarly _magnitude1 image corresponds to the shorter echo time and the OPTIONAL _magnitude2 image to the longer echo time.          |
