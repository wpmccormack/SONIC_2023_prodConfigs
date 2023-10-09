# Configs for Fall 2023 SONIC Production Tests at Purdue

This config works for cmssw release CMSSW_13_3_0_pre3.

It runs the SONIC-ized algorithms that are currently in the main branch of CMSSW:
* ParticleNet
* DeepMET
* The ECAL DRN

It currently runs on some files from the sample cms:/TTJets_TuneCP5_13TeV-amcatnloFXFX-pythia8/RunIISummer20UL18RECO-106X_upgrade2018_realistic_v11_L1v1-v1/AODSIM.  These are hard-coded right now, but this can be changed later.

You can run directly with
```
cmsRun step2_PAT_SONIC_Production_Workflow.py
```
That command uses default, hard-coded settings.

You can also run with something like
```
cmsRun run_workflow.py maxEvents=1000
```
Though the run file, you can adjust parameters on the command line.


## Notes

* Right now, the triton image is not specified explicitly in the config.  Using the default image for this release seems to work for fallback servers on LPC at least.  This might need to be specified at some point, and that will require editing the configs.
* The default number of events to run on is 100.  Please use the run file to set this manually.
* Please also use the run file to specify an address for the server if there is one (and e.g. port can be specified this way as well).