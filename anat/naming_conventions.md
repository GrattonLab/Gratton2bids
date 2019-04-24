## Anatomical Data Labeling: 

Dependent on what kinds of scans you do; typically for fMRI you'll collect T1w and T2w in which case you'll need a .nii.gz file and an additional .json holding parameter information. Using dcm2bids conversion will provide you with a bids appropriate json sidecar. 

  1)sub-<participant_label>[_ses-<session_label>][_acq-<label>][_ce-<label>][_rec-<label>][_run-<index>]_<modality_label>.nii[.gz]
  
  2)sub-<participant_label>[_ses-<session_label>][_acq-<label>][_ce-<label>][_rec-<label>][_run-<index>]_<modality_label>.json
 
dcm2bids is great because you just need to create the appropriate config file so that it can appropriately label all of your data. 

  
| Name  | modality_label | Description     |
| ------------- | ------------- |------------- |
| T1 weighted  | T1w  |                       |
| T2 weighted  | T2w  |                       |
| T1 Tho map  | T1rho  | Quantitative T1rho brain imaging     |
| T1 map | T1map  | Quantitative T1 map                      |
| T2 map | T2map  | Quantitative T2 map                      |
| T2* | T2star  |High resolution T2* image                    |
| FLAIR | FLAIR  |                       |
| FLASH | FLASH  |                       |
| Proton density | PD  |                       |
| Proton density map | PDmap  |                       |
| Combined PD/T2 | PDT2  |                       |
| Inplace T1 | inplaneT1  | T1-weighted anatomical image matched to functional acquisition   |
| Inplace T2 | inplaneT2  | T2-weighted anatomical image matched to functional acquisition   |
| Angiography | angio  |    |


If several scans of the same modality are acquired they MUST be indexed with a suffix: **_run-1, _run-2, _run-3**
etc. (only integers are allowed as run labels). When there is only one scan of a given type the suffix MAY be omitted.

Please note that diffusion imaging data is stored elsewhere (see below).

The OPTIONAL “acq-<label>” key/value pair corresponds to a custom label the user MAY use to distinguish a
different set of parameters used for acquiring the same modality. For example this should be used when a study
includes two T1w images - one full brain low resolution and and one restricted field of view but high resolution. In
such case two files could have the following names: sub-01_acq-highres_T1w.nii.gz and
sub-01_acq-lowres_T1w.nii.gz,however the user is free to choose any other label than “highres” and
“lowres” as long as they are consistent across subjects and sessions. In case different sequences are used to record
the same modality (e.g. RARE and FLASH for T1w) this field can also be used to make that distinction. At what level
of detail to make the distinction (e.g. just between RARE and FLASH, or between RARE, FLASH, and
FLASHsubsampled) remains at the discretion of the researcher.

Similarly the OPTIONAL “ce-<label>” key/value can be used to distinguish sequences using different contrast
enhanced images. The label is the name of the contrast agent. The key “ContrastBolusIngredient” MAY be
also be added in the JSON file, with the same label.

Similarly the OPTIONAL “rec-<label>” key/value can be used to distinguish different reconstruction algorithms
(for example ones using motion correction).

If the structural images included in the dataset were defaced (to protect identity of participants) one CAN provide
the binary mask that was used to remove facial features in the form of _defacemask files. In such cases the
OPTIONAL “mod-<label>” key/value pair corresponds to modality label for eg: T1w, inplaneT1, referenced by
a defacemask image. E.g., sub-01_mod-T1w_defacemask.nii.gz.
Some meta information about the acquisition MAY be provided in an additional JSON file. See Common MR 
metadata fields for a list of terms and their definitions. There are also some OPTIONAL JSON fields specific to
anatomical scans:


● ContrastBolusIngredient: Active ingredient of agent. Values MUST be one of: 

IODINE, GADOLINIUM, CARBON DIOXIDE, BARIUM, XENON Corresponds to DICOM Tag 0018,1048.
