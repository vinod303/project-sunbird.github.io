---
type: landing
directory: developer-docs
title: Telemetry HTML Interface Library
page_title: Telemetry HTML Interface Library
description: Telemetry HTML Interface Library
published: true
allowSearch: true
---
The ContentRenderer handles telemetry events for ECML content. HTML content has functionality such as click, navigation, assessment, etc. These functionalities are specific to or different for individual HTML content pieces. For HTML Content, the ContentRenderer logs only the telemetry start event. It does not log telemetry for any other event. By embedding the HTML interface library within the HTML content helps log telemetry events for the actions that take place in the HTML content.

This section details information about the library used to log telemetry events for HTML content.

## Need for an HTML interface library

The HTML interface library eases the HTML developer’s effort to log telemetry events from HTML content. It uses simple API methods exposed by the library to log associated events. The reasons to develop the HTML interface library are:

* Any HTML content can package the interface library as part of the content. Thus using the library, the HTML content can log telemetry events.

* There are simple API methods to generate the complete telemetry event as only the required fields are passed

* It is easy to upgrade to new versions, in case of major changes in the telemetry library

* There is effortless backward compatibility, as changes are handled within the telemetry library. Any upgrade of the telemetry library does not require code changes in the content

* The library will handle logging of events from HTML content when it is playing in case portal or device/app.

## HTML Interface API methods

The HTML interface provides simple methods to log telemetry, to handle the ContentRenderer overlay, to get content information, etc.

The HTML interface exposes the following list of API methods:

* [dispatchEvent](#heading=h.8mpvijdun4ir) - This method helps dispatch events to the ContentRenderer to handle specific functionality of ContentRenderer

* [getcontentMetadata](#heading=h.unjbn7wh2gxg) - This method is used to access content metadata

* [getConfig](#heading=h.7z6hh8t088oo) - This method is used to access content-renderer configuration

* [gotoEndPage](#heading=h.ezyw78ci2rnx) - This method helps to open the ContentRenderer end page after HTML content is completely viewed

* [exit](#heading=h.4s16ed5ur7og) - This method helps to close the ContentRenderer

* [telemetryService.interact](#heading=h.k5yn4tsg9w7d)- This method helps to log telemetry interact event

* [telemetryService.impression](#heading=h.kqgsrsebgi9z) - This method helps to log the Impression event on page or state change

* [telemetryService.response](#heading=h.1wfvl9hq6lo) - This method helps to log telemetry response event when an option is selected during an assessment

* [telemetryService.assessmentStart](#heading=h.ebhs2851lwwh) - This method is used when an assessment begins and it returns the event object

* [telemetryService.assess](#heading=h.9z35wwgz8awa) - This method helps to log the Assess event when the assessment is evaluated

* [telemetryService.exdata](#heading=h.7skc6puguem3) - This method helps log the telemetry ExData event

### DispatchEvent

Dispatch an specific event to control ContentRenderer functionalities.

<pre>
/**
  * eventName - Event name that has to dispatch to handle ContentRenderer functionality
  */
dispatchEvent: function(eventName) {
  // dispatch event to control ContentRenderer functionalities
}
</pre>

### getcontentMetadata

This will return the content metadata information(HTML Cotnent metadata here).

<pre>
/**
  * contentId - Current opened HTML content identifier
  * cb - callback function after after getting content iformation from API call
  */
getcontentMetadata = function(contentId, cb){
}
</pre>

### getConfig

This will return the content renderer configuration. This will help to know what is the context of HTML content playing in ContentRenderer.

<pre>
getConfig = function(){
}
</pre>

### gotoEndPage

After completion of HTML content, you can call this function to show ContentRenderer end-page. This will take the user out of HTML content view.

<pre>
gotoEndPage = function(){
}
</pre>

### exit

If you want to close the HTML game & contentRenderer to take user back to app, you can call this function.

<pre>
exit= function(){
}
</pre>

### Telemetry Interact

Api method to log telemtry interact events. Any interact events in HTML can log using this API method.

<pre>
/**
 * Interface to log temetry interact(INTERACT) event
 * data - {Object} Telemetry event data
 */
interact: function(data){
  _telemetryService.interact(data.type, data.id, data.extype, data.eks);
}
</pre>

### Telemetry Response

Api method to log telemtry response events. When an assessment is playing in content, on selection of option/answer data can be passed by calling this function.

<pre>
/**
 * Interface to log telemetry response(RESPONSE) event
 * data - {Object} Telemetry event data
 */
response: function(data){
    _telemetryService.interact(data.type, data.id, data.extype, data.eks);
}
</pre>

### Telemetry assessmentStart

Api method to get assessment start event data. This event object should be passed as a parameter while calling telemetry assess api method.

<pre>
/**
 * Interface to get assess start event
 * data - {Object} Telemetry event data
 */
assessmentStart: function(data){
    _telemetryService.assess(data.qid, data.subj, data.qlevel, data.data);
}
</pre>

### Telemetry Assess

Api method to log telemetry assess event. After submitting/validating the result of assessment question, call this funciton to log assessment result data.

<pre>
/**
 * Interface to log telemetry assess(ASSESS) event
 * event - {Object} telemetry event object returned after calling assessmentStart() API method
 * data - {Object} Telemetry event data
 */
assess: function(event, data){
    _telemetryService.assessEnd(event, data);
}
</pre>

### Telemetry Impression

Api method to log telemtry impression event. When there is a state/page change, call this method to log impression event

<pre>
/**
 * Interface to log telemetry impression(IMPRESSION)  event
 * data - {Object} Telemetry event data
 */
impression: function(data){
    _telemetryService.impression(data.stageid, data.stageto, data.data);
}
</pre>

### Telemetry Exdata

Api method to log telemtry exdata events. Any additional information of can be passed by calling this function.

<pre>
/**
 * Interface to log telemetry Exdata(EXDATA) event
 * data - {Object} Telemetry event data
 */
exdata: function(data){
   _telemetryService.xapi(data);
},
</pre>

## How to Use HTML interface library

Add the following to your HTML Content:

The file_path is the relative path (eg. assets/js) to these files within the html content.

<pre>
<!-- HTML Interface  JS library -->
<script src="[relative_path]/htmlinterface.js"></script>

//you can log telemetry interact event as shown below
org.ekstep.contentrenderer.interface.telemetryService.interact(data) 
//or 
RI.telemetryService.interact(data)
</pre>