### NavkitSDKTutorial

#### NavApp

How to run it?

* Follow Release note.txt
* adb shell mkdir /mnt/sdcard/ttndata

* adb push /Users/junwang/baiducloud/telenav/project/tt/TomTom_2019-08-02_Leban_AndroidNavUI-19.3/res/mnt/sdcard/ttndata/* //mnt/sdcard/ttndata



* ReflectionListenerRegistry: 

* ReferenceReflectionContextImpl: 

* ReferenceReflectionContextService： The ReferenceReflectionContextService is an Android wrapper for the ReferenceReflectionContext. This allows the ReferenceReflectionContext to continue to exists after the application has moved to the background.

* ReflectionConnector: connects to Reflection. It assumes that NavKit is already started and running.

* NavKitLifeLineServiceConnector:  The NavKitLifeLineServiceConnector will start NavKit using the NavKitLifeLineService running as a background service.

* NavKitManager: The NavKitManager connects NavKit and Reflection. It will first start with connecting to NavKit using the navKitConnector, when successfully connected it will connect Reflection.

* AbstractProxyReflectionHandler： 具体的业务都派生自他，Reflection handler interface activated. 

* Task_FtsGetPOIs:  onInterfaceActivated(),  make POI request via the reflection handler

  * iFreeTextSearchFemale.FtsRequest()
* ReflectionFramework.sendMessage
  
* ProxyFreeTextSearchMale.FtsDone

  * iFreeTextSearchMale.FtsDone() (在 MainActivity的looper中)
* SearchPlacesPresenter.searchResultClicked()
  * MainAcitivity.onAcitivityResult

* NavkitService: 

  * package: com.tomtom.navkit

  * Class: com.tomtom.navkit.NavKitLifeline

  * iLocationInfoFemale

  * iLocationInfoMale

