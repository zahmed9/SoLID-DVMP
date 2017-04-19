# Work-Flow to perform DVMP Simualtion with SoLID
## -- Zhihong Ye 04/19/2017

## Generate DVMP Simulated Events -- by Zafar Ahmed
### There are few different version of the MC events

  * Clean events w/o any effects
  * Add Fermi-Motion of neutrons in th etarget
  * Add Final-State-Interaction of outgoing pion
  * Add Energy-Loss and Multiple-Scattering effects of incoming and outgoing electrons, pion and proton

### Generated events with target polarization UP and DOWN separately
### Calculate total cross sections (dXS=dXS_UU+dXS_UT), where six different UT terms based on different angular modules are also given
### Every quantity is save in the lab frame


## Add SoLID Acceptance, Resolution and Missing Mass info in the rootfile
### The code "AddBranch.C" does this job and it also only saves events with Q2>4 GeV^2

 * SoLID Acceptance is given in histograms which were generated by runing GEMC simulation
 * SoLID detector resolutions are added by giveing the resolution of momenta, scattered angles and azimuthal angles for all three final state particles
 * Note to use the "corrected" quantities(p, theta,phi) in the lab frame to obtain the acceptances
 * When reconstructing missing mass, use the "corrected"+"resolution smeared" quantities

## Perform Binning
### The code "./makebin/makebin.C" does the job
### Use the code "./makebin/skim.C" to dvidie the root files into small files for individual -t bins

 * Define 7 -t bins, t_cut = [0.05, 0.15, 0.25, 0.35, 0.45, 0.55, 0.75, 1.2]
 * Define histograms for important quantties
 * Fill histograms with weights ( =dXS x Lumi x PSF x Acc). Note that all six asymmetries are built in in weights
 * In each -t bin, futher bin phi_S and phi_h into a 2D histogram with 12x12 bins
 * Calcualted numbers of counts in each (phi_S, phi_h) bin for each -t bin.
 * Do this excersice for the target with UP and DOWN polarizations, separately

## Reconstruct "Experimental" Asymmetry and perform fitting to extract angular modulations.
### The code "./roofit_extr/asym_extr.C" does the job with the RooFit package.
 * Currently it is a binned Maximin-Likelihood Minuit method
  