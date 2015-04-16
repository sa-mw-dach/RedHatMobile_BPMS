# RedHatMobile_BPMS
Trigger BPMS process from mobile app via Red Hat mobile platform.

BPM travel agency process is deployed on Openshift online. The process is triggered via an App developed with Red Hat Mobile, server side mobile component either hosted on Red Hat Mobile or any node.js instance.

## Setup
__Note:__ the original BPM on OSE Demo is described at [jbossdemocentral](https://github.com/jbossdemocentral/bpms-travel-agency-demo), but there was some modification necessary therefore the code is taken from Niraj Patel's github.

Setup the BPM Demo on Openshift Online:

1. Create a new JBoss BPM Suite application, as simple as clicking [here](https://openshift.redhat.com/app/console/application_type/custom?&cartridges%5B%5D=https://raw.githubusercontent.com/npatel2012/cartridge-bpmPaaS-travel-agency-demo/master/metadata/manifest.yml&name=travelagency&gear_profile=medium&initial_git_url=)
2. Login to the BPM Suite ( u:erics p: bpmsuite (admin) ) and start the travel agency process
3. Make sure that the Business Process is working by starting a process instance via the input form provided at http://yourBPMApplicationOSEDomain/external-client-ui-form-1.0

Setup Node.js Application on Red Hat Mobile (FeedHenry):

1. Create a new node.js app (Cloud Code Apps > Import existing app):</br>
    Type: node.js<br/>
    Name: whatever you like</br>
    git repos: https://github.com/eberlec/RedHatMobile_BPM_CloudApp.git</br>
    finish
2. After importing the application, define an environment variable ‘OSE_BPM_DOMAIN’ pointing to the domain of your BPM application on Openshift.
3. Deploy the Cloud Code App

Setup Cordova mobile client application:

1. Create a new Cordova Light app (Apps > Import existing app):</br>
    Type: Cordova Light</br>
    Name: whatever you like</br>
    git repos: https://github.com/eberlec/RedHatMobile_BPMS_CordovaClient.git</br>
    finish
2. Now we just need to specify what type of client application to build (iOS, Android, Windows) and link it to the right Cloud App
3. Build</br>
    Platform: your choice</br>
    Cloud App: select the one just created before</br>
    press build</br>

Once the application is built, a QR code is displayed letting you install the app directly on your phone. After installation, open it, fill the form appropriately and press "Book It".

You will get the confirmation, that the process was successfully started:
```
Process started: [11]
```
In the log files of your Cloud App you should see the corresponding request received from the mobile app and the one sent off towards Openshift:
```
Thu Apr 16 2015 15:21:49 GMT+0000 (UTC) 'In hello route POST / req.body=' { applicantName: 'chris',
  emailAddress: 'ceb@gg.ch',
  numberOfTravelers: '2',
  fromDestination: 'zrh',
  toDestination: 'dub',
  dateOfArrival: '2015-03-03',
  dateOfDeparture: '2015-03-05',
  __fh: 
   { cuid: '4d6f8faa50467a8b',
     cuidMap: null,
     destination: 'android',
     device: 
      { available: true,
        platform: 'Android',
        version: '4.4.2',
        uuid: 'xxx',
        cordova: '3.5.1',
        model: 'xxx' },
     sdk_version: 'FH_PHONEGAP_SDK/2.6.0+21',
     appid: 'xxx',
     appkey: 'xxx',
     projectid: 'xxx',
     connectiontag: '0.0.7',
     init: { trackId: 'xxx' } } }
calling url: http://xxx.rhcloud.com/external-client-ui-form-1.0/SimpleServlet?applicantName=chris&emailAddress=ceb@gg.ch&numberOfTravelers=2&fromDestination=zrh&toDestination=dub&preferredDateOfArrival=2015-03-03&preferredDateOfDeparture=2015-03-05&otherDetails=N%252FA
```
