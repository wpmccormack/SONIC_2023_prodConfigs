# Configs for Fall 2023 SONIC Production Tests at Purdue

## Version as of October 13, 2023

This version
* Reverts to a 2017 MiniAOD workflow, which contains particlenet (which is not included in the workflow below).  DeepMET, ParticleNet, and ECAL DRN
* Includes Simon's updates to the DRN for determinism
* Should work on GPU-enabled nodes at Purdue if instructions are followed
* Currently, this works on purdue with a file that Patrick copied in: /depot/cms/users/mccormp/7BED16E5-4FAC-4149-A69D-14140582F6EF.root.  I don't think this file exists on the grid anymore, so I'm not sure if it can be retrieved with xrootd.

The setup instructions:
First, do standard CMS setup:
```
source /cvmfs/cms.cern.ch/cmsset_default.sh
```

Now we pull a recent cmssw release.  Eventually, we would like this to be CMSSW_13_3_0_pre4, but for now
```
cmsrel CMSSW_13_3_X_2023-10-13-1100
cd CMSSW_13_3_X_2023-10-13-1100/src
cmsenv
git cms-init
git cms-addpkg PhysicsTools/PatAlgos
```
Then you will need to edit PhysicsTools/PatAlgos/python/slimming/patPhotonDRNCorrector_cfi.py.  Set the timeout line to something like timeout = 100.
Then recompile with
```
scram b -j 4
```
Then clone this repo.
In the cloned directory, you can run with something like:
```
cmsRun run_files.py maxEvents=100 device="cpu"
```


## Original Version

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