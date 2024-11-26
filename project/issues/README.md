## Issue Summary

Had unsupported lines when ALLOW_ZENITHANGLE is not defined in data.exf

## MITgcm Message

```
(PID.TID 0000.0001) *** ERROR *** EXF_CHECK: unsupported option when ALLOW_ZENITHANGLE is not defined
(PID.TID 0000.0001) *** ERROR *** EXF_CHECK: detected  1 fatal error(s)
(PID.TID 0000.0001) *** ERROR *** S/R ALL_PROC_DIE: ending the run
```

## Issue Remedy

Commented out the following lines in data.exf
```
# useExfZenIncoming = .TRUE., 
# select_ZenAlbedo  = 1,
```
