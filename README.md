# WiFiTrace: Network-centric WiFi Contact Tracing

WiFiTrace is a network-centric contact tracing method that uses enterprise WiFi networks for contact tracing in office and campus settings. Unlike bluetooth-based methods, it does not require an app to be installed on user phones and instead uses syslog data generated by enterprise WiFi access points to trace locations within office/campus buildings that an infected user has visited. It can also report other users who were seen for a period of time near those access points.

WiFiTrace is an open-source project led by Computer Science researchers at the University of Massachusetts Amherst. The project has a website at http://wifitrace.github.io/ 

The tool and algorithm leverage our prior expertise in mobility modeling and modeling mobile trajectories to efficiently perform these computations on syslog WiFi data.

## How it works

WiFiTrace is designed primarily for contact tracing inside buildings within the university and corporate campuses. It uses network monitoring data,  such as Syslog and SNMP data, that are typically gathered by an institution's IT department for purposes of network performance and security monitoring and leverages it for contact tracing.

In the event an employee or a student comes down sick, this data can be used to determine the campus buildings and locations within a building visited by the infected user over the infection period. It can also be used to analyze other users who may have been present at those locations during that period.

WiFiTrace uses Access Point (AP) association and disassociation information from syslogs, SNMP, and RTLS reports for contact tracing. It assumes that users have mobile devices that are connected to a ubiquitous WiFi network. As the user visits different buildings or different rooms over the course of the day, their device connects to different access points, allowing the tool to reconstruct their path and visited locations. Devices from other users that were associated with those APs at those times can also be analyzed to determine the risk to other users.

## Differences with bluetooth-based approaches

WiFiTrace is a complementary approach to bluetooth-based methods for contact tracing. It does not require any app to be downloaded by users to their phones, nor does it require any data to be recorded on the user's device.

It is a network-centric approach that uses the network's view of users to infer their locations. WiFiTrace only works with enterprise WiFi networks and is primarily designed for large indoor environments with WiFi coverage (campuses, office buildings, shopping malls).  It does not work with most consumer-grade WiFi routers, such as ones deployed at home, since it assumes RADIUS authentication to associate a device to a specific user. 

It is designed for indoor contact tracing, and unlike bluetooth methods, it does not work outdoors (unless there is WiFi coverage in those outdoor areas).  

## Design of WiFiTrace 

The tool uses a modular architecture to make it compatible with WiFi devices from different networking vendors. 
The processor code processes raw networking monitoring logs/data to extract AP association/disassociation information and outputs it to a standard data format.  Currently, we provide a pre-processor for syslogs produced for HP/Aruba WiFi devices. Support for other vendors is a work in progress.  The output data format is fully documented so that others can write/contribute pre-processing scripts for other vendors.

The main tool then ingests this data in a standard format and generates contact tracing reports based on a specified user or a device MAC address. The output report can be in human-readable text or JSON format.

Additional details on tool installation, data formats, and a user guide can be found in the 
[User Guide](https://github.com/umassos/WiFiTrace/blob/master/USER-GUIDE.md)
 

The design of this tool leverages our research expertise in characterizing and modeling the mobility of users. A recent technical publication titled "Empirical Characterization of Mobility of Multi-Device Internet Users" describes our mobility characterization and modeling research and is available on 
[arxiv](https://arxiv.org/abs/2003.08512) 

Our research publication describing the network-centric WiFi-based contact tracing method used by WiFiTrace can be found here: [WiFiTrace: Network-based Contact Tracing for Infectious Diseases Using Passive WiFi Sensing](https://arxiv.org/abs/2005.12045v2)
