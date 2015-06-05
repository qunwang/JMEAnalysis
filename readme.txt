Hi Qiang,

in fact we didn't have our chat yet, but now also the MET group seems interested in similar jet algorithm validations, so we'd be very happy if you could help out with this service task.

The larger project is to put useful jet plots (to be done for example for the BOOST conference in summer) into the JMEValidator:
https://twiki.cern.ch/twiki/bin/view/CMS/JMEValidator
On the list are RECO-GEN charged hadron fraction (like figure 4 in AN-14-153 v4).
The first step to make this possible is to adapt the GenJet fraction definitions in CMSSW which are outdated and still correspond to CaloJets instead of PFJets.

1) If I look 
http://cmslxr.fnal.gov/source/RecoJets/JetProducers/src/JetSpecific.cc#0404
http://cmslxr.fnal.gov/source/DataFormats/JetReco/interface/GenJet.h?v=CMSSW_7_2_3#0061
The invisible fraction is estimated summing over muon and neutrino.
The muon are visible in PF.

2) Need to add a way to get the muonFraction standalone

3) Need to add a way to get separately the charged and neutral Hadronic fraction
Here seems that we have only one method
http://cmslxr.fnal.gov/source/RecoJets/JetProducers/src/JetSpecific.cc#0403
http://cmslxr.fnal.gov/source/DataFormats/JetReco/interface/GenJet.h?v=CMSSW_7_2_3#005900

4) also how the ks enter in the game. We see some of the genParticle as kS but we cannot understand where are entered in the fraction sum

In order to study this on MiniAOD, one needs to recluster the GenJets with something like the following:
from RecoJets.Configuration.GenJetParticles_cff import genParticlesForJetsNoNu
genParticlesForJetsNoNuMiniAOD = ak4GenJets.clone( src = cms.InputTag("packedGenParticles") )
from RecoJets.JetProducers.ak4GenJets_cfi import ak4GenJets
ak4GenJetsNoNuMiniAOD = ak4GenJets.clone( src = cms.InputTag("genParticlesForJetsNoNuMiniAOD") )

Since both MET and JMAR would like to have this fixed on a rather shortish time scale, would someone from your group be able to work on it? Jim+me can help with a recipes to get started.

Best,
Andreas
