# RedHatMobile_BPMS
Triggers BPMS process via red hat mobile.

BPM travel agency process is deployed on Openshift online. The process is triggered via an App developed in Red Hat Mobile, server side mobile component either hosted on Red Hat Mobile or any node.js instance.

## Setup
__Note:__ the original BPM on OSE Demo is described at [jbossdemocentral](https://github.com/jbossdemocentral/bpms-travel-agency-demo), but there was some modification necessary therefore the code is taken from Niraj Patel's github.

Setup the BPM Demo on Openshift Online:

1. Create a new JBoss BPM Suite application, as simple as clicking [here](https://openshift.redhat.com/app/console/application_type/custom?&cartridges%5B%5D=https://raw.githubusercontent.com/npatel2012/cartridge-bpmPaaS-travel-agency-demo/master/metadata/manifest.yml&name=travelagency&gear_profile=medium&initial_git_url=)
2. Login to the BPM Suite ( u:erics p: bpmsuite (admin) ) and start the travel agency process
3. Make sure that the Business Process is working by starting a process instance via the input form provided at http://<<yourBPMApplicationDomain>>/external-client-ui-form-1.0

Setup Node.js Application on Red Hat Mobile (FeedHenry):
1. Create a new node.js project


