//log to lxplus

```
cd /tmp/login/
cmsrel CMSSW_10_2_0
cd CMSSW_10_2_0/src
cmsenv
git clone git@github.com:jandrea/IOV_Validation.git .
scramv1 b -j4
```

```
conddb_import -c sqlite_file:myNoise.db -f frontier://FrontierProd/CMS_CONDITIONS -t myTag -i SiStripNoise_GR10_v1_hlt -b 321493

sqlite3 myNoise.db
> select * from IOV;
> UPDATE IOV SET SINCE=1 WHERE SINCE=321493;
> select * from IOV;
> .exit
```

```
grid-proxy-init
 
cmsRun stepALCARECO_RAW2DIGI_RECO_ALCA.py newIOV=False inputFiles=root://cms-xrd-global.cern.ch//store/data/Run2018D/ZeroBias/RAW/v1/000/321/475/00000/FC884CAC-2AA4-E811-9216-FA163EBF0D83.root outputFile=histo_Old.root nevents=10
cmsRun stepALCARECO_RAW2DIGI_RECO_ALCA.py newIOV=True  inputFiles=root://cms-xrd-global.cern.ch//store/data/Run2018D/ZeroBias/RAW/v1/000/321/475/00000/FC884CAC-2AA4-E811-9216-FA163EBF0D83.root outputFile=histo_New.root nevents=10
```

```
root -l runScript.C+
```