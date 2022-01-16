/**
 *  Activate Foscam Camera on Motion Detect
 *
 *  Copyright 2015 Nagaraja Chitters
 *
 *  Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except
 *  in compliance with the License. You may obtain a copy of the License at:
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 *  Unless required by applicable law or agreed to in writing, software distributed under the License is distributed
 *  on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License
 *  for the specific language governing permissions and limitations under the License.
 *
 */
definition(
    name: "Activate Foscam on Motion",
    namespace: "nagchi",
    author: "Nagaraja Chitters",
    description: "Activates Foscam IP Camera if Motion Detected and turns OFF when no Motion",
    category: "Convenience",
    iconUrl: "https://s3.amazonaws.com/smartapp-icons/Convenience/Cat-Convenience.png",
    iconX2Url: "https://s3.amazonaws.com/smartapp-icons/Convenience/Cat-Convenience@2x.png",
    iconX3Url: "https://s3.amazonaws.com/smartapp-icons/Convenience/Cat-Convenience@2x.png"
)

preferences {
	section("When the mode changes to...") {
		input "alarmMode", "mode", multiple: true
	}
	
    section("Enable these Foscam Camera...") {
		input "cameras", "capability.imageCapture", multiple: true
	}
    
    section("Disable App for Manual Recording") {
        input "appDisable", "bool", title: "App Disabble?", required: false
    }
	
	section("Select Motion Sensor") {
		input "motionSensors", "capability.motionSensor", title: "Choose motion sensor", multiple: true
	}
    
    section("Send message to this phone number"){
        //input("recipients", "contact", title: "Send notifications to") 
        input "phone1", "phone", title: "Phone Number", required: false
    }
	section("Send message to this phone number"){
        //input("recipients", "contact", title: "Send notifications to") 
        input "phone2", "phone", title: "Phone Number", required: false
    }
	section("Send message to this phone number"){
        //input("recipients", "contact", title: "Send notifications to")
        input "phone3", "phone", title: "Phone Number", required: false
    }
	section("Send message to this phone number"){
        //input("recipients", "contact", title: "Send notifications to")
        input "phone4", "phone", title: "Phone Number", required: false
    }
}

def installed() {
    subscribe(motionSensors, "motion", motionHandler)
    cameras?.alarmOff()
}

def updated() {
    unsubscribe()
    subscribe(motionSensors, "motion", motionHandler)
    cameras?.alarmOff() 
}

def motionHandler(evt) {
	//log.debug "handler $evt.name: $evt.value"  
	
    if (appDisable == true) {
        log.debug "App is Disabled for manual recording"
        return
    }
    
	if (evt.value == "active") {
	    if (location.currentMode == "Away") {
	        cameras?.alarmOn()
	        //log.debug "Foscam Hall Camera Activated on Motion"
            if (phone1)
	        	sendSms(phone1, "Foscam Hall Camera Activated on Motion")
            if (phone2)
	        	sendSms(phone2, "Foscam Hall Camera Activated on Motion")
            if (phone3)
	        	sendSms(phone3, "Foscam Hall Camera Activated on Motion")
            if (phone4)
	        	sendSms(phone4, "Foscam Hall Camera Activated on Motion")          
	    }
    } else {
        cameras?.alarmOff()
        //log.debug "Foscam Hall Camera Deactivated"
        if (location.currentMode == "Away") {
            if (phone1)
                sendSms(phone1, "Foscam Hall Camera Deactivated")
            if (phone2)
                sendSms(phone2, "Foscam Hall Camera Deactivated")            
            if (phone3)
                sendSms(phone3, "Foscam Hall Camera Deactivated")
            if (phone4)
                sendSms(phone4, "Foscam Hall Camera Deactivated")     
        }
    }
}
