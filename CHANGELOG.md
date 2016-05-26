# 5.0.6
### Additions and Improvements
* Internal support for the FairPlay plugin for Brightcove Player SDK for iOS. Please note that if you are using version 1.0.3 of the FairPlay plugin for Brightcove Player SDK for iOS, you must use version 5.0.6 or later of the Brightcove Player SDK.


# 5.0.5
### Additions and Improvements
* Introduced convenience methods for accessing optional soundtracks, subtitles and closed captions from the AVPlayerItem of the current `BCOVPlaybackSession`. Apple API documentation refers to soundtracks as
audible media options, while subtitles and closed captions are referred to as legible media options.


  `-[BCOVPlaybackSession audibleMediaSelectionGroup]`,  
  `-[BCOVPlaybackSession  selectedAudibleMediaOption]`,  
  `-[BCOVPlaybackSession legibleMediaSelectionGroup]`,  
  `-[BCOVPlaybackSession  selectedLegibleMediaOption]`,  
  `-[BCOVPlaybackSession selectAudibleMediaOptionAutomatically]`,  
  `-[BCOVPlaybackSession selectLegibleMediaOptionAutomatically]`,  
  `-[BCOVPlaybackSession displayNameFromAudibleMediaSelectionOption:]`, and  
  `-[BCOVPlaybackSession displayNameFromLegibleMediaSelectionOption:]`.

* DASH sources are ignored.

# 5.0.4
### Additions and Improvements
* When a OnceUX or FairPlay-encoded stream stalls due to network slowdowns or interruptions, it can now be restarted using ` [BCOVPlaybackController resumeVideoAtTime:withAutoPlay:]`. Previously, only streams without OnceUX or FairPlay could be restarted.
* New lifecycle events are available for detecting the various states of the playback buffer (see `BCOVPlaybackSession.h` for details on each event): `kBCOVPlaybackSessionLifecycleEventPlaybackStalled`, `kBCOVPlaybackSessionLifecycleEventPlaybackRecovered`,  `kBCOVPlaybackSessionLifecycleEventPlaybackBufferEmpty`, and `kBCOVPlaybackSessionLifecycleEventPlaybackLikelyToKeepUp`.  



# 5.0.3
### Additions and Improvements
* Added support for using Picture in Picture and background audio at the same time by setting the new `pictureInPictureActive` property of the `BCOVPlaybackController` to `YES`. Please see README.md for usage details.
* When the `BCOVPlaybackController` delivers a new `BCOVPlaybackSession` for a video, it calls the delegate method `-[BCOVPlaybackControllerDelegate playbackController:didAdvanceToPlaybackSession:]` method as usual. Now, however, the delegate method will not be called until the `currentItem` on the `AVPlayer` inside the `BCOVPlaybackSession` has been loaded. Previously the delegate method was called immediately while the `AVPlayer` was still loading the `AVPlayerItem`, and thus `currentItem` could still be `nil`. This makes it easier to work with the `AVPlayer` when each session is delivered.
* Internal improvements.


# 5.0.2
### Additions and Improvements
* Reformatted the framework's short version string to comply with App Store submission requirements.

# 5.0.1
### Additions and Improvements
* Playing video in the background is supported by setting the new `allowsBackgroundAudioPlayback` property of the `BCOVPlaybackController` to `YES`. Please see README.md for usage details. 
* Internal improvements.

# 5.0.0
### Breaking Changes
* Calls to `[AVPlayer play]`, `[AVPlayer pause]`, and `[AVPlayer seekToTime:]` must be changed to call the corresponding method on the `BCOVPlaybackController`. Failure to do so will cause undefined behavior.
* The static library distributable has been removed. If installed manually (not CocoaPods), you will need to remove libBCOVPlayerSDK.a and its headers from the Header Search Path. Please see README.md for new install options (including a static library framework).
* Header `BCOVPlayerSDK.h` has been removed. Please see README.md for new import options.

### Additions and Improvements
* tvOS support (including analytics). 
* Bitcode support.
* The SDK is now distributed as a static or dynamic framework.
* `BCOVPlaybackController` now offers play, pause, and seek methods.
* Internal improvements.

# 4.4.3
* Introduce `kBCOVPlaybackSessionLifecycleEventWillPauseForAd` event to be send on the lifecycle delegate by ad plugins.

# 4.4.2
### Additions and Improvements
* Fixed an issue where calling `-[BCOVPlaybackController setVideos:nil]` didn't clear out the player correctly.
* Fixed a crash in `BCOVAnalyticsSession`.
* Updated internal network calls to use NSURLSession instead of NSURLConnection.
* `BCOVPlaybackService` now allows you to override the NSURLSession used for requests, by setting the `sharedURLSession` property.

# 4.4.1
### Additions and Improvements
* Added `-[BCOVPlaybackService findPlaylistWithPlaylistID:completion:]` and `-[BCOVPlaybackService findPlaylistWithReferenceID:completion:]`.
* Added `+[BCOVBasicSourceSelectionPolicy sourceSelectionHLSWithScheme:]` to prefer HTTPs sources. Please see README.md for more information on HTTPs and source selection.

# 4.4.0
### Breaking Changes
* Player is now paused when entering the background and therefore no longer resumes automatically when entering the foreground. This was added to work around an AVPlayer play state corruption when becoming active. If you would like to regain the original functionality, you will need to call play on the player when entering the foreground.

### Additions and Improvements
* Added `-[BCOVPlaybackControllerAdsDelegate playbackController:didPauseAd:]` and `-[BCOVPlaybackControllerAdsDelegate playbackController:didResumeAd:]` to be implemented by ad session providers.
* Updated to Analytics API v2, including quality of service metrics.
* Updated internal ReactiveCocoa version from 2.3.1 to 2.5.
* Internal improvements to support BCOVPlayerUI.

# 4.3.5
### Additions and Improvements
* Fixes memory leaks introduced by v4.3.4.

# 4.3.4
### Additions and Improvements
* Added `- [BCOVPlaybackController resumeVideoAtTime:withAutoPlay:`. This API can be used to re-initialize the AVPlayer in case of a network disruption. Progress and lifecycle events will be suppressed during this action.  Lifecycle events `kBCOVPlaybackSessionLifecycleEventResumeBegin`, `kBCOVPlaybackSessionLifecycleEventResumeComplete`, and `kBCOVPlaybackSessionLifecycleEventResumeFail` were added to provide updates on this action.
* Added `kBCOVPlaybackSessionLifecycleEventFailedToPlayToEndTime`. This event will fire when the AVPlayer has given up trying to play content. This even can be used in conjunction with `- [BCOVPlaybackController resumeVideoAtTime:withAutoPlay:` to re-initialize the player once network conditions have improved.

# 4.3.3
### Breaking Changes
* Preloading of videos is now disabled by default. If you wish to turn preloading back on, please consult the README.md for more information about `BCOVBasicSessionLoadingPolicy`.

### Additions and Improvements
* Added new APIs for enabling preloading of videos called `BCOVBasicSessionLoadingPolicy`. Please see the README.md for more information.
* Fixed a bug in the default controls that could prevent seeks to the end of the video from completing.

# 4.3.2
### Additions and Improvements
* Added Playback Service classes: `BCOVPlaybackService` and `BCOVPlaybackServiceRequestFactory`. These APIs provide an alternative way to retrieve Brightcove video assets via the Brightcove CMS API with more rich meta information such as text tracks.

# 4.3.1
### Additions and Improvements
* The seek bar on the default controls is now disabled until the AVPlayer is capable of seeking.

# 4.3.0
### Additions and Improvements
* Added `BCOVAdvertising` APIs. These APIs introduce the concept of Ads to our core SDK. Playback controller delegate and session consumer apis have also been added to provide ad information. In the future, our advertising plugins will be updated to provide ad events through these apis.  For more information, please see the README.md.
* `BCOVPlaybackSession` protocol now includes a providerExtention property. In the future, some of our plugins will be updated to provide plugin specific functionality through this property.
* The default controls now include a closed caption button for testing.
* Internal bug fixes.

# 4.2.3
### Additions and Improvements
* Switch analytics to https.

# 4.2.2
### Additions and Improvements
* Fixes a bug where the default controls playhead label will show a the incorrect playhead at the end of a video when running on device.
* Fixes a bug where the default controls slider isn't reset to 0 after calling advanceToNext or using AutoAdvance.

# 4.2.1
### Breaking Changes
* iOS 6 is still deprecated in this release. We have not removed support yet.  iOS 6.x currently accounts for ~2% of global SDK traffic.
* This release has been built with Xcode 6. In Xcode 6, Apple removed armv7s from the list of standard architectures. This release no longer includes an armv7s architecture slice.
* Use of `BCOVDelegatingSessionConsumer` and `BCOVDelegatingSessionConsumerDelegate` has been deprecated. Delegate methods equivilent to those provided by `BCOVDelegatingSessionConsumerDelegate` have been added to the `BCOVPlaybackSessionConsumer` protocol. Objects should now implement `BCOVPlaybackSessionConsumer` protocol and its methods.

| Deprecated Method (BCOVDelegatingSessionConsumerDelegate)           | Replaced By (BCOVPlaybackSessionConsumer)          |
| ------------------------------------------------------------------- | -------------------------------------------------- |
| `playbackConsumer:didAdvanceToPlaybackSession:`                     | `didAdvanceToPlaybackSession:`                     |
| `playbackConsumer:playbackSession:didChangeDuration:`               | `playbackSession:didChangeDuration:`               |
| `playbackConsumer:playbackSession:didChangeExternalPlaybackActive:` | `playbackSession:didChangeExternalPlaybackActive:` |
| `playbackConsumer:playbackSession:didPassCuePoints:`                | `playbackSession:didPassCuePoints:`                |
| `playbackConsumer:playbackSession:didProgressTo:`                   | `playbackSession:didProgressTo:`                   |
| `playbackConsumer:playbackSession:didReceiveLifecycleEvent:`        | `playbackSession:didReceiveLifecycleEvent:`        |

* `[<BCOVPlaybackSessionConsumer> consumeSession:]` method has been deprecated.  Use `[<BCOVPlaybackSessionConsumer> didAdvanceToSession:]` instead.

### Additions and Improvements
* Fixed a bug that prevented plugins from cleaning up correctly.
* Fixed a bug where didProgressTo delegate methods weren't called after a seek if the player is paused.
* Performance and object allocation improvements.

# 4.2.0

### Breaking Changes
* iOS 6 is still deprecated in this release. We have not removed support yet.
* All deprecated symbols within the Player SDK for iOS have been removed from this release.
* Use of ReactiveCocoa in public APIs within the Player SDK for iOS has been removed from this release.
* If using Cocoapods, ReactiveCocoa will no longer be installed by including our library. Running `pod update` to update to 4.2 will remove it. If you wish to continue using ReactiveCocoa for your own use, you will need to declare ReactiveCocoa in your podfile.
* If you installed ReactiveCocoa manually in your project, it can be removed. To remove it, you will need to at least perform the following:
    * Remove any "Target Dependencies" on ReactiveCocoa.
    * Remove any ReactiveCocoa references from the "Header Search Paths".
    * Remove libReactiveCocoa-iOS.a from the "Link Binary With Libraries" phase.
    * Remove the ReactiveCocoa.xcodeproj from your project or workspace.

### Additions and Improvements
* Fixed a bug that could cause sessions to leak if a playback controller is deallocated immediately after calling `-setVideos:`.

# 4.1.9

### Additions and Improvements
* Internal bug fixes.

# 4.1.8

### Breaking Changes
* iOS 6 is deprecated in this release. Version 4.2 of the Brightcove Player SDK for iOS is not supported on versions of iOS below 7.1 .
* Use of ReactiveCocoa in public APIs within the Player SDK for iOS is deprecated in this release. Version 4.2 of the Brightcove Player SDK for iOS will not require clients to install any version of ReactiveCocoa, and properties or methods that return or expect RACSignal objects will be removed. See the header files for guidance on how to update deprecated functionality for compatibility with 4.2. The deprecations include the following:
  * `-[AVPlayer bcov_periodicTimeObserverSignalForInterval:]`
  * `-[AVPlayer bcov_periodicTimeObserverSignalForInterval:queue:]`
  * `-[BCOVCatalogService findPlaylistWithPlaylistID:parameters:]`
  * `-[BCOVCatalogService findPlaylistDictionaryWithPlaylistID:parameters:]`
  * `-[BCOVCatalogService findPlaylistWithReferenceID:parameters:]`
  * `-[BCOVCatalogService findPlaylistDictionaryWithReferenceID:parameters:]`
  * `-[BCOVCatalogService findVideoWithVideoID:parameters:]`
  * `-[BCOVCatalogService findVideoDictionaryWithVideoID:parameters:]`
  * `-[BCOVCatalogService findVideoWithReferenceID:parameters:]`
  * `-[BCOVCatalogService findVideoDictionaryWithReferenceID:parameters:]`
  * `-[BCOVCuePointProgressPolicy signalWithValue:]`
  * `-[BCOVPlaybackSession cuePoints]`
  * `-[BCOVPlaybackSession durationChanges]`
  * `-[BCOVPlaybackSession isExternalPlaybackActive]`
  * `-[BCOVPlaybackSession lifecycle]`
  * `-[BCOVPlaybackSession progress]`
* Duration changes reported by a BCOVPlaybackSession will no longer include the initial value of `kCMTimeNegativeInfinity`.
* A lifecycle event of type `kBCOVPlaybackSessionLifecycleEventProgress` will now be reported during a seek, even if the AVPlayer's rate is 0.0 (paused).

### Additions and Improvements
* Fixed a bug in which the AirPlay button could randomly appear in the default video playback controls.
* Added methods that return NSOperation objects to BCOVCatalogService. The operations replace similar (deprecated) RACSignal-returning methods.
* Fixed a bug that could cause repeated, immediate calls to `-[BCOVPlaybackController pause]` and `-[BCOVPlaybackController play]` to execute out of order.
* Return `instancetype` instead of `id` from methods that return instances of the current class type, in preparation for compatibility with Swift.
* Made refinements and enhancements to the information sent to Brightcove analytics, including the ability to programmatically specify the account ID, destination, and source properties to be included in all analytics reporting.
* Fixed an analytics bug that could prevent the sending of a video impression.
* Fixed an analytics bug in which video engagement was not being reported for live streams.
* Fixed an analytics bug in which video engagement could be reported when the seeking in reverse.
* Fixed an analytics bug in which one second of video engagement reporting could be dropped periodically.
* The underlying error is included in the event payload when a lifecycle event of type `kBCOVPlaybackSessionLifecycleEventFail` occurs.

# 4.1.7

### Breaking Changes
* The return type of `-[BCOVPlaylist count]` has been corrected to return a value of type `NSUInteger` (previously it returned a value of type `int`).

### Additions and Improvements
* Added an `arm-64` architecture slice to the static library, for applications that wish to target the 64-bit architecture.
* Introduced a new class, BCOVCuePointProgressPolicy. This class isn't used directly by the Brightcove Player SDK for iOS at this time, but may be used in plugins.
* Fixed a bug in the firing of cue point events of type `kBCOVCuePointPositionTypeAfter`.
* The SDK now correctly reports the `video_name` and `device_type` parameters to Brightcove Video Cloud Analytics.
* NSOperationQueues used internally within the SDK are now given more useful logical names, to help with debugging code that executes in the queue.
* Fixed a bug in which the `kBCOVPlaybackSessionLifecycleEventPlay` lifecycle event would fire multiple times in response to the AVPlayer/s `rate` being set to a nonzero value more than once.

# 4.1.6

### Breaking Changes
* We reversed one change introduced in 4.1.5: if no BCOVSource with a HLS or MP4 `deliveryMethod` is found in a given playback session's BCOVVideo, the default source selection policy will select the first of the video's sources. We made this reversal due to the number of customers who reported that their videos  failed to play (because none of the sources in those videos had the expected `deliveryMethod`). This means that, as of 4.1.6, if you are not using a custom source selection policy, the playback controller will *not* advance to the next video if it cannot find an HLS or MP4 source in the current video; it will attempt to use the first source regardless of its delivery method.

### Additions and Improvements
* Automatically advance to the next playback session if the current playback session has no video, or if its video has no sources.
* Fixed a bug in which a video with a single cue point could cause a crash.

# 4.1.5

### Breaking Changes
* This release introduces an improved default source selection policy, and a mechanism to override the default source selection. Prior to 4.1.5, the default policy would select the first source on each video, regardless of the source's `url` or `deliveryMethod` properties. In 4.1.5, the default policy now selects the first source whose `deliveryMethod` is `kBCOVSourceDeliveryHLS` ("HLS"). If no HLS source is found, its fallback behavior will select the first source whose `deliveryMethod` is `kBCOVSourceDeliveryMP4` ("MP4"). If no source with a `deliveryMethod` of "HLS" or "MP4" exists on the video, the playback controller will advance to the next playback session. Most videos retrieved via BCOVCatalogService will have the expected sources.
* UIViews are prohibited from being added as children of the playback controller's video view.

### Additions and Improvements
* Added the `-[BCOVPlayerSDKManager createPlaybackController]` convenience overload for when a view strategy isn't needed.
* Fixed a bug to ensure the elapsed time label on the default controls is reset when advancing to a new session.
* Fixed video engagement reporting for Brightcove Analytics.
* Fixed a bug that prevented listeners for BCOVCuePoints of type `kBCOVCuePointPositionTypeAfter` from firing when advancing to a new session.
* Fixed a harmless bug where BCOVPlayerSDKManager could redundantly register components.

# 4.1.4

### Breaking Changes
* When `-[BCOVPlaybackController setVideos:]` is called, the current playback session is removed. Previously, calling `-setVideos:` would add the new videos to the playback controller, but would not affect the current session.
* BCOVPlaybackFacade and BCOVPlaybackQueue protocols are deprecated in this release, as we have consolidated their functionality within the BCOVPlaybackController protocol. We apologize for any inconvenience this may cause, but the migration path to update code that uses these protocols is straightforward:
    1. There is no longer any reason to create a BCOVPlaybackQueue object. Remove code that calls `-[BCOVPlayerSDKManager createPlaybackQueue]` altogether, as it will no longer compile.
    1. Replace calls to `-[BCOVPlayerSDKManager createPlaybackFacadeWithFrame:]` with `-[BCOVPlayerSDKManager createPlaybackControllerWithViewStrategy:]`. You can pass `nil` to this method. Then you can set your frame directly on the returned playback controller's `view`.
    1. If you implemented BCOVPlaybackFacadeDelegate, modify your delegate to implement BCOVPlaybackControllerDelegate instead. Replace each delegate method with the corresponding method from the BCOVPlaybackControllerDelegate protocol. For example, `-playbackFacade:playbackSession:didProgressTo:` would become `-playbackController:playbackSession:didProgressTo:`. There is no need to change the behavior of your delegate methods, it is just a renaming.
    1. Remaining references to `id<BCOVPlaybackFacade>` can be changed to `id<BCOVPlaybackController>`. In other words, wherever you previously used a facade, you should now use a playback controller.
    1. Remove any calls to `BCOVPlaybackFacade.controlsEnabled`. This property will no longer have any effect. If you are still developing your app and do not yet have your own controls implemented, you can re-enable the default playback controls by passing `-[BCOVPlayerSDKManager defaultControlsViewStrategy]` when you create the playback controller, instead of passing a `nil` strategy.
* Methods that create BCOVPlaybackController objects with a frame have been deprecated. If you used `-[BCOVPlayerSDKManager createPlaybackControllerWithFrame:]` or `-[BCOVPlayerSDKManager createPlaybackControllerWithSessions:frame:]`, the migration path is also straightforward:
    1. Use `-[BCOVPlayerSDKManager createPlaybackControllerWithViewStrategy:]`. You can pass `nil` to this method. Then you can set your frame directly on the returned playback controller's `view`.
    1. That's it.
* `-[BCOVPlaybackController seekToTime:]` has been deprecated. It should be replaced with a call to `-[AVPlayer seekToTime:completionHandler:]` on the given playback session's AVPlayer object.

### Additions and Improvements
* This release introduces support for loading plugin components into the BCOVPlayerSDKManager. With this 4.1.4 release, we are simultaneously releasing our first plugins: BCOVIMA, a plugin that offers built-in integration with Interactive Media Ads, and BCOVWidevine, a plugin that allows you to use Widevine-encrypted content with the Player SDK for iOS.
* Playback controllers obtain their playback sessions from a BCOVPlaybackSessionProvider object. Session providers provide a mechanism for plugins to affect content playback by stepping into the session construction process. The Player SDK for iOS ships with a basic session provider (aptly named BCOVBasicSessionProvider), which provides the default playback functionality.
* Playback controllers send their playback sessions to a list of BCOVPlaybackSessionConsumer objects. Session consumers provide a mechanism for plugins to respond to playback events without affecting the app developer's ability to specify a BCOVPlaybackControllerDelegate.
* Playback sessions now send a "terminate" event on their lifecycle signal when the playback controller is finished with them. Clients can listen for this event to know when to discard a reference to a playback session. A playback session should not be used after it has terminated.
* App developers can specify a view strategy that specifies how the playback controller should construct its `view`. For further information, refer to the README.
* Apps no longer have to wait for a playback session to be advanced before calling `-[BCOVPlaybackController play]`. If this method is called before advancing to a playback session, playback will begin as soon as the first session is advanced to.
* Detection of cue points during video playback has been significantly optimized to pose less of a burden on CPU and battery.
* Methods to pause and resume ads have been added to BCOVPlaybackController. However, these are merely stubs when used without an advertising plugin that supports them.
* API documentation is generated from header comments, and is available in the `html/` directory of the Player SDK for iOS.
* Corrected the documentation of the behavior of the `-[BCOVPlaybackSession lifecycle]` signal. Previously, this signal was described as sending its entire history of events to each subscriber, when in fact it is a hot signal and sends only events that occur *after* subscription. Note that this does not represent a change in functionality, but rather a fix to incorrect documentation about that functionality.

# 4.0.3

### Breaking Changes
* `-[BCOVPlayerSDKManager newPlaybackQueue]` is an [invalid method name for code built with ARC][arcnotes]. In 4.0.3, we renamed that method to `-createPlaybackQueue`, and for consistency, we renamed the other methods in BCOVPlayerSDKManager that begin with the word `new`. The following table illustrates the changes:

|              Removed Method                 |                  Replaced By                   |
| --------------------------------------------| ---------------------------------------------- |
| `-newPlaybackQueue`                         | `-createPlaybackQueue`                         |
| `-newPlaybackFacadeWithFrame:`              | `-createPlaybackFacadeWithFrame:`              |
| `-newPlaybackControllerWithSessions:frame:` | `-createPlaybackControllerWithSessions:frame:` |

[arcnotes]: https://developer.apple.com/library/mac/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html

### Additions and Improvements
* Fixes for memory leaks that could occur when destroying and recreating BCOVPlaybackFacade, BCOVPlaybackQueue, and BCOVPlaybackController instances.


# 4.0.2

### Breaking Changes
* BCOVPlaybackSession objects are released shortly after a new playback session is dequeued. Prior to 4.0.2, playback session objects would leak until the last session for any given collection of videos was dequeued (at which time the previous sessions would be released).
* Event signals on BCOVPlaybackSession objects send complete when a new playback session is dequeued.

### Additions and Improvements
* Fixed a bug in which cue point events could be sent (erroneously) for playback sessions that are no longer active.
* Corrections to reporting `video_engagement` metrics for Brightcove Analytics.
* Throttle the check for cue points down to only once per second, to avoid unnecessary calculations.
* Fixed a bug in which BCOVPlaybackFacadeDelegate event methods were called at inappropriate times, such as when new playback session were dequeued.
* Fixed a race condition that could occur if two threads concurrently attempted to access `-[BCOVPlaybackController view]`. (This race could result in creating two UIView objects.)
* Corrected the header documentation of the `-[AVPlayer+BCOVSignalSupport bcov_periodicTimeObserverSignalForInterval:]` and `-[AVPlayer+BCOVSignalSupport bcov_periodicTimeObserverSignalForInterval:queue:]` category methods, which misleadingly stated that the signals returned by these methods would complete if the AVPlayer deallocates. The implementation of `-[AVPlayer addPeriodicTimeObserverForInterval:queue:usingBlock:]`, used internally by these signals, prevents its AVPlayer from being released while these signals have active subscriptions. Furthermore, these signals never send complete; subscriptions to these signals live until explicitly disposed.


# 4.0.1

### Breaking Changes
* `Brightcove-Player-SDK.podspec` now uses the `~>` operator to declare its dependency on the latest `2.1.x` version of ReactiveCocoa. This means that running `pod install` or `pod update` will install the latest version of ReactiveCocoa up to, but not including, `2.2.0`.
* `NaN` values received by `-[BCOVPlaybackFacadeDelegate playbackFacade:playbackSession:didChangeDuration:]` due to an unknown duration are now suppressed. The `NaN` values were sent for `kCMTimeIndefinite` durations, which is the duration of AVPlayerItems prior to the `kBCOVPlaybackSessionLifecycleEventReady` lifecycle event. The `-[BCOVPlaybackSession durationChanges]` signal continues to report all durations, including the initial `kCMTimeIndefinite`, for clients that require this level of detail.

### Additions and Improvements
* Fixed a bug that could prevent AVPlayer objects from being released.
* Fixed a bug so that `-[BCOVPlaybackFacade setControlsEnabled:]` performs the expected behavior of enabling or disabling the default controls.
