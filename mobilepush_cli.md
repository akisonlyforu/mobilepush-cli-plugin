---
 
copyright:
  years: 2020
lastupdated: "2020-08-17"

subcollection: mobilepush-cli-plugin

keywords: push notifications CLI, push notifications command line, push notifications terminal, push notifications shell, Push Notifications

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Push Notifications CLI
{: #mobilepush-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. {{site.data.keyword.cloud}} CLI supports a plug-in framework to extend its capability. You can install the {{site.data.keyword.mobilepushshort}} CLI plug-in from the {{site.data.keyword.cloud}} plug-in repository. With the {{site.data.keyword.mobilepushshort}} service CLI, you can easily send {{site.data.keyword.mobilepushshort}} by using the CLI commands available.
{:shortdesc} 

## Prerequisites
{: #mobilepush-cli-prereq}

* An {{site.data.keyword.cloud_notm}} account. If you do not have an account, click [here](https://cloud.ibm.com/) to create one.
* An instance of [{{site.data.keyword.cloud_notm}} {{site.data.keyword.mobilepushshort}}](https://cloud.ibm.com/catalog/services/push-notifications) service.
* [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

## Installing {{site.data.keyword.mobilepushshort}} CLI plug-in
{: #mobilepush-cli-install}

Install the {{site.data.keyword.mobilepushshort}} CLI plug-in by running the following command from the IBM plug-in repo '{{site.data.keyword.cloud_notm}}':

```sh
ibmcloud plugin install push-notifications
```
{: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

### Output
{: #mobilepush-cli-install-output}

The command returns the following output:
```
Looking up 'push-notifications' from repository 'IBM Cloud'...
Plug-in 'push-notifications/push 1.0.0' found in repository 'IBM Cloud'
Attempting to download the binary file...
 15.87 MiB / 15.87 MiB [==============================================================================================================================================] 100.00% 14s
16645396 bytes downloaded
Installing binary...
OK
Plug-in 'push-notifications 1.0.0' was successfully installed into /Users/<username>/.bluemix/plugins/push-notifications. Use 'ibmcloud plugin show push-notifications' to show its details.
```
{: screen}

## ibmcloud pn init
{: #mobilepush-initialize-cli}

Before proceeding with initializing the CLI plug-in make sure that you have set your ibmcloud account to particular resource group. 
{: note}

Initialize the cli plug-in by using the following command:

```sh
ibmcloud pn init
```
{: pre}

### Example
{: #mobilepush-cli-init-example}

Log in to {{site.data.keyword.cloud_notm}} and initialize the cli to {{site.data.keyword.mobilepushshort}} instance **pn1**

```sh
ibmcloud pn init
```
{: pre}

### Output
{: #mobilepush-cli-init-output}

The command returns the following output:

```
Initializing IBM Cloud Push Notifications Service plug-in...

Select a push instance:
1. pn1
2. pn2
Enter a number> 1
OK
Push instance 'pn1' was selected.
```
{: screen}

## ibmcloud pn message get
{: #mobilepush-get-message}

You can get the details of a message sent, by using the command:

```sh
ibmcloud pn message get --message_id MESSAGE_ID [--output FORMAT]
```
{: pre}

### Command options 
{: #mobilepush-get-message-options}

<dl>
<dt>--message_id MESSAGE_ID</dt>
<dd>The ID of the message sent. This value is required.</dd>
<dt>--output FORMAT (optional)</dt>
<dd>Specifies the output format. Default is tabular and the supported alternative is JSON/YAML.</dd>
</dl>

### Example
{: #mobilepush-cli-get-message-example}

To get the message details for the message ID `Yz0GQIsQ`, run the following command:

```sh
ibmcloud pn message get --message_id Yz0GQIsQ
```
{: pre}

### Output
{: #mobilepush-cli-get-message-output}

The command returns the following output:

```
ibmcloud pn message get --message_id Yz0GQIsQ
Retrieving message details...
OK
Message:                    
             Alert:   messageForAndroidWithSetting      
             URL:     testString      
Settings:                                 
             CollapseKey:           ping      
             InteractiveCategory:   Accept      
             DelayWhileIdle:        true      
             Sync:                  true      
             Visibility:            PUBLIC      
             Priority:              DEFAULT      
             Sound:                 default      
             TimeToLive:            1      
             Lights:                                     
                                    LedArgb:    BLACK         
                                    LedOnMs:    1         
                                    LedOffMs:   1         
             Style:                                   
                                    Type:    bigtext_notification         
                                    Title:   hello world title         
                                    URL:     https://ibm.com         
                                    Text:    abc         
                                    Lines:   a,b         
             Type:                  default      
Target:                         
             Platforms:   G      
MessageId:   Yz0GQIsQ   
Status:      FAILED   
```
{: screen}

## ibmcloud pn message send
{: #mobilepush-send-message}

Use this command to send a single message:

```sh
ibmcloud pn message send --message MESSAGE [--settings SETTINGS] [--target TARGET] [--output FORMAT]
```
{: pre}

### Command options 
{: #mobilepush-send-message-options}

<dl>
<dt>--message MESSAGE</dt>
<dd>The message to be sent. This value is required.
<table>
  <caption>Table 1. Additional properties that can be configured for the notification under `MESSAGE`.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>alert</td>
    <td>string</td>
    <td>The notification message to be shown to the user.</td>
  </tr>
  <tr>
    <td>url</td>
    <td>string</td>
    <td>An optional URL that can be sent along with the alert.</td>
  </tr>
</table>
</dd>
<dt>--settings SETTINGS (optional)</dt>
<dd>Additional properties that can be configured for the notification.
<p>
<table>
  <caption>Table 2. Settings specific to iOS platform.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>badge</td>
    <td>integer</td>
    <td>The number to display as the badge of the application icon.</td>
  </tr>
  <tr>
    <td>interactiveCategory</td>
    <td>string</td>
    <td>The category identifier to be used for the interactive push notifications.</td>
  </tr>
  <tr>
    <td>iosActionKey</td>
    <td>string</td>
    <td>The title for the Action key.</td>
  </tr>
  <tr>
    <td>payload</td>
    <td>JSON object</td>
    <td>Custom JSON payload that will be sent as part of the notification message.</td>
  </tr>
  <tr>
    <td>sound</td>
    <td>string</td>
    <td>The name of the sound file in the application bundle. The sound of this file is played as an alert.</td>
  </tr>
  <tr>
    <td>titleLocKey</td>
    <td>string</td>
    <td>The key to a title string in the Localizable.strings file for the current localization. The key string can be formatted with %@ and %n$@ specifiers to take the variables specified in the titleLocArgs array.</td>
  </tr>
  <tr>
    <td>locKey</td>
    <td>string</td>
    <td>A key to an alert-message string in a Localizabl.strings file for the current localization (which is set by the user's language preference). The key string can be formatted with %@ and %n$@ specifiers to  take the variables specified in the locArgs array.</td>
  </tr>
  <tr>
    <td>launchImage</td>
    <td>string</td>
    <td>The filename of an image file in the app bundle, with or without the filename extension. The image is used as the launch image when users tap the action button or move the action slider.</td>
  </tr>
  <tr>
    <td>titleLocArgs</td>
    <td>string[]</td>
    <td>Variable string values to appear in place of the format specifiers in title-loc-key.</td>
  </tr>
  <tr>
    <td>locArgs</td>
    <td>string[]</td>
    <td>Variable string values to appear in place of the format specifiers in locKey.</td>
  </tr>
  <tr>
    <td>title</td>
    <td>string</td>
    <td>The title of Rich Push notifications (Supported only on iOS 10 and above).</td>
  </tr>
  <tr>
    <td>subtitle</td>
    <td>string</td>
    <td>The subtitle of the Rich Notifications (Supported only on iOS 10 and above).</td>
  </tr>
  <tr>
    <td>attachmentUrl</td>
    <td>string</td>
    <td>The link to the iOS notifications media (video, audio, GIF, images - Supported only on iOS 10 and above).</td>
  </tr>
  <tr>
    <td>type</td>
    <td>string</td>
    <td>Allowable values: DEFAULT, MIXED, SILENT.</td>
  </tr>
  <tr>
    <td>apnsCollapseId</td>
    <td>string</td>
    <td>Multiple notifications with the same collapse identifier are displayed to the user as a single notification.</td>
  </tr>
  <tr>
    <td>apnsThreadId</td>
    <td>string</td>
    <td>An app-specific identifier for grouping related notifications. This value corresponds to the threadIdentifier property in the UNNotificationContent object.</td>
  </tr>
  <tr>
    <td><nobr>apnsGroupSummaryArg</nobr></td>
    <td>string</td>
    <td>The string the notification adds to the category’s summary format string.</td>
  </tr>
  <tr>
    <td><nobr>apnsGroupSummaryArgCount</nobr></td>
    <td>integer</td>
    <td>The number of items the notification adds to the category’s summary format string.</td>
  </tr>
</table>
</p>
<p>
<table>
  <caption>Table 3. Settings specific to Android platform.</caption>
  <tr>
    <th>Property</th>
    <th>Subproperty</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>collapseKey</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>Dozed devices to display only the latest notification and discard old low-priority notifications.</td>
  </tr>
  <tr>
    <td><nobr>interactiveCategory</nobr></td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>The category identifier to be used for the interactive push notifications.</td>
  </tr>
  <tr>
    <td>icon</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>Specify the name of the icon to be displayed for the notification. Make sure that the icon is already packaged with the client application.</td>
  </tr>
  <tr>
    <td>delayWhileIdle</td>
    <td>&nbsp;</td>
    <td>boolean</td>
    <td>When this parameter is set to true, it indicates that the message should not be sent until the device becomes active.</td>
  </tr>
  <tr>
    <td>sync</td>
    <td>&nbsp;</td>
    <td>boolean</td>
    <td>Device group messaging makes it possible for every app instance in a group to reflect the latest messaging state.</td>
  </tr>
  <tr>
    <td>visibility</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>private/public - Visibility of this notification, which affects how and when the notifications are revealed on a secure locked screen.</td>
  </tr>
  <tr>
    <td>redact</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>Content that is specified will show up on a secure locked screen on the device when visibility is set to Private.</td>
  </tr>
  <tr>
    <td>channelId</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>unique Id of the channel to add channel properties.</td>
  </tr>
  <tr>
    <td>payload</td>
    <td>&nbsp;</td>
    <td>JSON object</td>
    <td>Custom JSON payload that will be sent as part of the notification message.</td>
  </tr>
  <tr>
    <td>priority</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>A string value that indicates the priority of this notification. Allowed values are 'max', 'high', 'default', 'low' and 'min'. High/Max priority notifications along with 'sound' field might be used for Heads up notification in Android 5.0 or higher.sampleval='low'.</td>
  </tr>
  <tr>
    <td>sound</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>The sound file (on device) that will be attempted to play when the notification arrives on the device.</td>
  </tr>
  <tr>
    <td>timeToLive</td>
    <td>&nbsp;</td>
    <td>integer</td>
    <td>This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.</td>
  </tr>
  <tr>
    <td>lights</td>
    <td>&nbsp;</td>
    <td>&nbsp;</td>
    <td>Allows setting the notification LED color on receiving push notification.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>ledArgb</td>
    <td>string</td>
    <td>The color of the led. The hardware will do its best approximation.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>ledOnMs</td>
    <td>integer</td>
    <td>The number of milliseconds for the LED to be on while it's flashing. The hardware will do its best approximation.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>ledOffMs</td>
    <td>string</td>
    <td>The number of milliseconds for the LED to be off while it's flashing. The hardware will do its best approximation.</td>
  </tr>
  <tr>
    <td>androidTitle</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>The title of Rich Push notifications.</td>
  </tr>
  <tr>
    <td>groupId</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>Set this notification to be part of a group of notifications sharing the same key. Grouped notifications might display in a cluster or stack on devices that support such rendering.</td>
  </tr>
  <tr>
    <td>style</td>
    <td>&nbsp;</td>
    <td>&nbsp;</td>
    <td>Options to specify for Android expandable notifications. The types of expandable notifications are picture_notification, bigtext_notification, inbox_notification.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>type</td>
    <td>string</td>
    <td>Specifies the type of expandable notifications. The possible values are bigtext_notification, picture_notification, inbox_notification.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>title</td>
    <td>string</td>
    <td>Specifies the title of the notification. The title is displayed when the notification is expanded. Title must be specified for all three expandable notifications.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>url</td>
    <td>string</td>
    <td>A URL from which the picture have to be obtained for the notification. Must be specified for picture_notification.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>text</td>
    <td>string</td>
    <td>The big text that needs to be displayed on expanding a bigtext_notification. Must be specified for bigtext_notification.</td>
  </tr>
  <tr>
    <td>&nbsp;</td>
    <td>lines</td>
    <td>string[]</td>
    <td>An array of strings that is to be displayed in inbox style for inbox_notification. Must be specified for inbox_notification.</td>
  </tr>
  <tr>
    <td>type</td>
    <td>&nbsp;</td>
    <td>string</td>
    <td>Allowable values: DEFAULT, SILENT.</td>
  </tr>
</table>
</p>
<p>
<table>
  <caption>Table 4. Web Push Notifications settings specific to Mozilla Firefox browser.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>iconUrl</td>
    <td>string</td>
    <td>The URL of the icon to be set for the WebPush Notification.</td>
  </tr>
  <tr>
    <td>timeToLive</td>
    <td>integer</td>
    <td>This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.</td>
  </tr>
  <tr>
    <td>payload</td>
    <td>string</td>
    <td>Custom JSON payload that will be sent as part of the notification message.</td>
  </tr>
</table>
</p>
<p>
<table>
  <caption>Table 5. Web Push Notifications settings specific to Chrome browser.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>iconUrl</td>
    <td>string</td>
    <td>The URL of the icon to be set for the WebPush Notification.</td>
  </tr>
  <tr>
    <td>timeToLive</td>
    <td>integer</td>
    <td>This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.</td>
  </tr>
  <tr>
    <td>payload</td>
    <td>string</td>
    <td>Custom JSON payload that will be sent as part of the notification message.</td>
  </tr>
</table>
</p>
<p>
<table>
  <caption>Table 6. Web Push Notifications settings specific to Safari browser.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>title</td>
    <td>string</td>
    <td>Specifies the title to be set for the Safari Push Notifications.</td>
  </tr>
  <tr>
    <td>urlArgs</td>
    <td>string[]</td>
    <td>The URL arguments that need to be used with this notification. This has to provided in the form of a JSON Array.</td>
  </tr>
  <tr>
    <td>action</td>
    <td>string</td>
    <td>The label of the action button.</td>
  </tr>
</table>
</p>
<p>
<table>
  <caption>Table 7. Web Push Notifications settings specific to Chrome App extension.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>collapseKey</td>
    <td>string</td>
    <td>Dozed devices to display only the latest notification and discard old low-priority notifications.</td>
  </tr>
  <tr>
    <td>delayWhileIdle</td>
    <td>boolean</td>
    <td>When this parameter is set to true, it indicates that the message should not be sent until the device becomes active.</td>
  </tr>
  <tr>
    <td>title</td>
    <td>string</td>
    <td>Specifies the title to be set for the WebPush Notification.</td>
  </tr>
  <tr>
    <td>iconUrl</td>
    <td>string</td>
    <td>The URL of the icon to be set for the WebPush Notification.</td>
  </tr>
  <tr>
    <td>timeToLive</td>
    <td>integer</td>
    <td>This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.</td>
  </tr>
  <tr>
    <td>payload</td>
    <td>string</td>
    <td>Custom JSON payload that will be sent as part of the notification message.</td>
  </tr>
</table>
</p>
</dd>
<dt>--target TARGET (optional)</dt>
<dd>An optional target for the message. Specify one of the target parameters to choose the recipients of the notification. If no target is specified, a broadcast notification will be sent to all the registered devices. 
<p>
<table>
  <caption>Table 8. Additional properties that can be configured for the notification under `TARGET`.</caption>
  <tr>
    <th>Property</th>
    <th>Property type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>deviceIds</td>
    <td>string[]</td>
    <td>Send notification to the list of specified devices.</td>
  </tr>
  <tr>
    <td>userIds</td>
    <td>string[]</td>
    <td>Send notification to the specified userIds.</td>
  </tr>
  <tr>
    <td>platforms</td>
    <td>string[]</td>
    <td>Send notification to the devices of the specified platforms. 'A' for apple (iOS) devices, 'G' for google (Android) devices, 'WEB_CHROME' for Chrome Web Browsers, 'WEB_FIREFOX' for Firefox Web Browsers, 'WEB_SAFARI' for Safari Push Notifications and 'APPEXT_CHROME' for Chrome App Extension.</td>
  </tr>
  <tr>
    <td>tagNames</td>
    <td>string[]</td>
    <td>Send notification to the devices that have subscribed to any of these tags.</td>
  </tr>
</table>
</p>
</dd>
<dt>--output FORMAT (optional)</dt>
<dd>The format can be of JSON/YAML. The default output format is tabular.</dd>
</dl>

### Example
{: #mobilepush-send-message-example}

Send a simple message with the optional values.

```sh
ibmcloud pn message send --message '{"alert": "message1", "url": "https://ibm.com"}' --settings '{"gcm":{"collapseKey":"ping","interactiveCategory":"Accept","icon":"icon","delayWhileIdle":true,"sync":true,"visibility":"PUBLIC","payload":{"additionalInfo":"additionalInfo"},"priority":"default","sound":"default","timeToLive":1,"lights":{"ledArgb":"BLACK","ledOnMs":1,"ledOffMs":1},"style":{"type":"bigtext_notification","title":"notification title","url":"https://ibm.com","text":"text","lines":["line1","line2"]}}}' --target '{"platforms":["G"]}'
```
{: pre}

### Output
{: #mobilepush-send-message-output}

The command returns the following output:
```
Sending message...
OK
MessageID   Status   
1DTVa5uX    Accepted                      
```
{: screen}

## ibmcloud pn message send-in-bulk
{: #mobilepush-send-in-bulk-message}

Use this command to send bulk messages:

```sh
ibmcloud pn message send-in-bulk --body BODY [--output FORMAT]
```
{: pre}

### Command options 
{: #mobilepush-send-bulk-message-options}

<dl>
<dt>--body BODY</dt>
<dd>Array of messages in JSON string format that needs to be sent in bulk. This value is required.

For body message formats and command options, refer [here](#mobilepush-send-message-options).
{: note}
</dd>
<dt>--output FORMAT (optional)</dt>
<dd>The format can be of JSON/YAML. The default output format is tabular.</dd>
</dl>


### Example
{: #mobilepush-send-bulk-message-example}

Send a simple message with the optional values.

```sh
ibmcloud pn message send-in-bulk --body='[{"message":{"alert":"message1","url":"testString"},"settings":{"gcm":{"collapseKey":"ping","interactiveCategory":"Accept","icon":"","delayWhileIdle":true,"sync":true,"visibility":"PUBLIC","payload":{"additionalInfo":"additionalInfo"},"priority":"default","sound":"default","timeToLive":1,"lights":{"ledArgb":"BLACK","ledOnMs":1,"ledOffMs":1},"style":{"type":"bigtext_notification","title":"notification title","url":"https://ibm.com","text":"text","lines":["line1","line2"]}}},"target":{"platforms":["G"]}},{"message":{"alert":"message2","url":"http://ibm.com"},"settings":{"gcm":{"collapseKey":"ping","interactiveCategory":"Accept","icon":"","delayWhileIdle":true,"sync":true,"visibility":"PUBLIC","payload":{"additionalInfo":"additionalInfo"},"priority":"default","sound":"default","timeToLive":1,"lights":{"ledArgb":"BLACK","ledOnMs":1,"ledOffMs":1},"style":{"type":"bigtext_notification","title":"notification title","url":"https://ibm.com","text":"text","lines":["line1","line2"]}}},"target":{"platforms":["G"]}}]'
```
{: pre}

### Output
{: #mobilepush-send-bulk-message-output}

The command returns the following output:
```
Sending bulk messages...
OK
MessageID   Status   
udBShb07    Accepted   
8bewYSpJ    Accepted                    
```
{: screen}

## ibmcloud plugin uninstall
{: #mobilepush-cli-uninstall}

Use this command to uninstall the {{site.data.keyword.mobilepushshort}} CLI plugin.

```sh
ibmcloud plugin uninstall push-notifications
```
{pre}

Uninstall returns a success message, if no errors.
