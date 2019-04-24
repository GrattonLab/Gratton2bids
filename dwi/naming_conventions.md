## Diffusion imaging

  1) sub-<participant_label>[_ses-<session_label>][_acq-<label>][_run-<index>]_dwi.nii[.gz]
  
  2) sub-<participant_label>[_ses-<session_label>][_acq-<label>][_run-<index>]_dwi.bval
  
  3) sub-<participant_label>[_ses-<session_label>][_acq-<label>][_run-<index>]_dwi.bvec
  
  4)sub-<participant_label>[_ses-<session_label>][_acq-<label>][_run-<index>]_dwi.json

Diffusion-weighted imaging data acquired for that participant. The optional “acq-<label>” key/value pair
corresponds to a custom label the user may use to distinguish different set of parameters. For example this should
be used when a study includes two diffusion images - one single band and one multiband. In such case two files
could have the following names: sub-01_acq-singleband_dwi.nii.gz and sub-01_acq-multiband_dwi.nii.gz, however the user is free to choose any other label than “singleband” and “multiband” as long as they are consistent across subjects and sessions.

For multiband acquisitions, one can also save the single-band reference image as type “sbre” (e.g. dwi/sub-control01_sbref.nii[.gz]).

The bvec and bval files are in the FSL format : The bvec files contain 3 rows with n space-delimited floating-point 5 numbers (corresponding to the n volumes in the relevant NIfTI file). The first row contains the x elements, the second row contains the y elements and third row contains the z elements of a unit vector in the direction of the applied diffusion gradient, where the i-th elements in each row correspond together to the i-th volume with [0,0,0] for non-diffusion-weighted volumes. Inherent to the FSL format for bvec specification is the fact that the coordinate system of the bvecs is with respect to the participant (i.e., defined by the axes of the corresponding dwi.nii file) and not the magnet’s coordinate system, which means that any rotations applied to dwi.nii also need to be applied to the corresponding bvec file.


### bvec example: 

0 0 0.021828 -0.015425 -0.70918 -0.2465

0 0 0.80242 0.22098 -0.00063106 0.1043

0 0 -0.59636 0.97516 -0.70503 -0.96351

The bval file contains the b-values (in s/mm2) corresponding to the volumes in the relevant NIfTI file), with 0designating non-diffusion-weighted volumes, space-delimited.

### bval example: 

0 0 2000 2000 1000 1000

.bval and .bvec files can be saved on any level of the directory structure and thus define those values for all sessions
and/or subjects in one place (see Inheritance principle).

### Json Example

{"PhaseEncodingDirection": "j-",
"TotalReadoutTime": 0.095
}

