# MagicMirror Module: MMM-Homematic-Heaters
A MagicMirror Module for your radio controlled Homematic (eQ-3) radiator thermostats of type: <b><a href="http://amzn.to/2nzhd4a" target="_blank" title="">HM-CC-RT-DN</a></b><br>
According documentation, it should also work with devices of type HM-CC-RT-DN-BoM.

### The module displays the following information:

* The name of the heater
* The current temperature
* The target temperature
* The current mode
* The fault reporting (i.e. low battery), if any

Supported languages are: English, Deutsch

## Screenshots

<table width="100%">
	<tbody>
		<tr>
			<td>
				Default screen:
				<p><img src="https://cloud.githubusercontent.com/assets/26480749/24048049/ee2f90c2-0b27-11e7-80d8-8f232328f8a1.png" height="150"/></p>
			</td>
			<td>
				Default screen with a fault message:
				<p><img src="https://cloud.githubusercontent.com/assets/26480749/24048628/c636b6e8-0b29-11e7-9a2d-ce471f058b35.png" height="150"/></p>
			</td>
		</tr>
		<tr>
			<td>
				Default screen where heater in Kid's room is in manually mode:
				<p><img src="https://cloud.githubusercontent.com/assets/26480749/24070241/a1463d8c-0bb9-11e7-9b17-1ec5aaa29f73.png" height="150"/></p>
			</td>
			<td>
			&nbsp;
			</td>
		</tr>
		<tr>
			<td>
Screen showing all information: <p><code>showSetTemperature: true</code><br><code>showCurrentMode: true</code><br>
<code>showFaultReporting: true</code></p>
<p><img src="https://cloud.githubusercontent.com/assets/26480749/24070524/6927f9da-0bbf-11e7-815b-b7786317b8d1.png" height="150"/></p>
			</td>
			<td>
Minimalistic screen:<p><code>showSetTemperature: false</code><br> <code>showCurrentMode: false</code><br>
<code>showFaultReporting: false</code></p><p><img src="https://cloud.githubusercontent.com/assets/26480749/24048630/c63a891c-0b29-11e7-9639-1677d08c5781.png" height="150"/></p>
			</td>
		</tr>
		<tr>
			<td>
If you prefer it more colorful, just change the stylesheet...<p><img src="https://cloud.githubusercontent.com/assets/26480749/24070539/c0da85f8-0bbf-11e7-85ba-f03917709805.png" height="150"/></p>
			</td>
			<td>
			&nbsp;
			</td>
		</tr>
	</tbody>
</table>

## Pre-requisites
The following dependencies are required and must be installed to be able to use this module:
* <a href="https://github.com/MichMich/MagicMirror" target="_blank" title="MagicMirror2">MagigMirror<sup>2</sup></a><br/>
Obviously yes... without the mirror even this module is useless :-)
* <a href="https://github.com/hobbyquaker/XML-API" target="_blank" title="XML-API for CCU2">XML-API addon</a><br/>The XML-API addon must be installed on your Homematic central control unit (CCU1 / CCU2). 
* <a href="https://github.com/jindw/xmldom" target="_blank" title="xmldom for node.js">xmldom</a><br/>The xmldom DOMParser and XMLSerializer must be installed for node.js
* <a href="https://github.com/ashtuchkin/iconv-lite" target="_blank" title="iconv-lite for node.js">iconv-lite</a><br/>The iconv-lite is required to deal with the correct character encoding <code>iso-8859-1</code> (i.e.: German umlauts ä ü ö) after receiving data via the XML-API.

## Installation
In your terminal, go to your MagicMirror's Module folder:
````
cd ~/MagicMirror/modules
````

Clone this repository:
````
git clone https://github.com/MAF1981/MMM-Homematic-Heaters
````

Configure the module in your `config.js` file as followed.

## Using the module

To use this module, add it to the modules array in the `config/config.js` file:
````javascript
modules: [
 {
    module: 'MMM-Homematic-Heaters',
    header: 'Myhome: Heaters',
    position: 'top_left', // This can be any of the regions.
    config: {
      devices: [
        {
         id: '1112',
         label: 'Living Room',
         showSetTemperature: false,
         showCurrentMode: true,
         showFaultReporting: true
        }
        //Add all other devices you want to show
      ],
      ccu2IP: '127.0.0.1',
      xmlapiURL: 'config/xmlapi',
      updateInterval: 120000
    }
 }
]
````

## Configuration options
The following properties can be configured:

<table width="100%">
	<thead>
		<tr>
			<th>Option</th>
			<th width="100%">Description</th>
		</tr>
	</thead>
	<tbody>
    <tr>
      <td><code>devices</code></td>
      <td><b>Required</b> - Add all your devices that should appear in the MagicMirror. Each device must include the following properties:      <table width="100%">
        <thead>
          <tr>
            <th>Option</th>
            <th width="100%">Description</th>
          </tr>
        </thead>
        <tbody>
          <tr>
           <td><code>id</code></td>
           <td>The unique <code>ise_id</code> to identify the device. All ids can be extracted by calling the following URL of the installed XML-API addon: <code>http://ccu2IP/xmlapiURL/devicelist.cgi</code></td>
          </tr>
          <tr>
           <td><code>label</code></td>
           <td>The label for the device (i.e.: Living Room). If not present or empty, the internal device name is shown instead.</td>
          </tr>
          <tr>
           <td><code>showSetTemperature</code></td>
           <td>Whether to show or to hide the target temperature. Default is <code>false</code></td>
          </tr>
          <tr>
           <td><code>showCurrentMode</code></td>
           <td>Whether to show or to hide the current state (i.e.: Heater off). Default is <code>true</code></td>
          </tr>	
          <tr>
           <td><code>showFaultReporting</code></td>
           <td>Whether to show or to hide any faults of the device (i.e.: Low battery warning). Default is <code>true</code></td>
          </tr>	
        </tbody>
      </table>
      </td>
		</tr>
    <tr>
			<td><code>ccu2IP</code></td>
			<td><b>Optional</b></code> - The IP address of your HomeMatic central control unit.
<br/>If not set, the default is: <code>homematic-ccu2</code></td>
		</tr>
        <tr>
			<td><code>xmlapiURL</code></td>
			<td><b>Optional</b></code> - The URL to the XML-API addon on your HomeMatic central control unit. Is appended to <code>ccu2IP</code>.<br/>If not set, the default is: <code>config/xmlapi</code></td>
		</tr>
        <tr>
            <td><code>updateInterval</code></td>
            <td><b>Optional</b></code> - The update interval in milliseconds.<br/>
If not set, the default is: <code>300000</code> (5 minutes)</td>
        </tr>
	</tbody>
</table>

## Troubleshooting
Make sure that the XML-API addon is working fine. If you've setup the XML-API addon and your HomeMatic central control unit (CCU2) with default values, you should be able to see a list of all your connected devices by clicking the following URL:<br> <a href="http://homematic-ccu2/config/xmlapi/devicelist.cgi" target="_blank">http://homematic-ccu2/config/xmlapi/devicelist.cgi</a>

## Side notes
The requests via the XML-API addon does not require a login! If your HomeMatic control central unit is accessible without special protection via the Internet, this can be a serious security issue!

## Next steps
I'm planning to implement my HomeMatic window handles with the module to show the window state (open, closed). The window handles are of type <a href="http://amzn.to/2mCxxjU" target="_blank">HM-Sec-RHS</a>.

## Further information
* <a href="http://www.homematic.com/" target="_blank">homematic.com</a> - HomeMatic website 
* <a href="https://www.homematic-inside.de/" target="_blank">homematic-inside.de</a> - Best HomeMatic community (blogs, tipps, addons,...)
* <a href="https://www.homematic-forum.de/" target="_blank">homematic-forum.de</a> - Forum to get help
* <a href="https://www.homematic-inside.de/software/download/item/homematic-skript" target="_blank">HomeMatic script documentation / specification</a>
* <a href="https://www.homematic-inside.de/software/addons/item/xmlapi" target="_blank">XML-API section on homematic-inside.de</a>
