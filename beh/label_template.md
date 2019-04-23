## Behavioral Data Labeling: 


  1)Events file 
    sub-##[_ses-<sesion_label>]_task-<task_name>_events.tsv
    
    Example: *sub-0006_ses-1_task-Prostop_events.tsv*
    
  2) Metadata 
  
  
    sub-##[_ses-<sesion_label>]_task-<task_name>_events.json 
    
    Example: *sub-0006_ses-1_task-Prostop_events.json*
    
  3) Physio
  
  
    sub-##[_ses-<sesion_label>]_task-<task_name>_physio.tsv.gz
    
    Example: *sub-0006_ses-1_task-Prostop_physio.tsv.gz*
    
    sub-##[_ses-<sesion_label>]_task-<task_name>_physio.json
    
    Example: *sub-0006_ses-1_task-Prostop_physio.json*
    
    
    
Files that don't include onset and duration columns should be in a separate file named _beh.tsv instead of _events.tsv
