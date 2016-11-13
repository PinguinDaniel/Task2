Task 2 Scenario:
Attached is a Network trace containing two calls made via SIP:
1. Phone A tries to call Phone B and it fails
2. Phone B tries to call Phone A and it fails

What you should send us
* Please explain why both calls fail

There are two phones and one SIP Server:
Phone1: Display info “Test1”, IP 192.168.9.147, ID 8910023
Phone2: Display info “Test2”, IP 192.168.1.102, ID 8910022
SIP Server: kamailio (4.2.3 (x86_64/linux))

Scenario 1: Phone1 try to call Phone2
Frame 34 - Phone1 send a SIP INVITE Request to Phone2 with parameter user=phone
Frame 35 - SIP Status 100 TRYING from Phone2 to Phone1
Frame 39 - Phone2 answers with SIP error 488 - Not Acceptable Here to Phone1
		Warning: 304 192.168.9.181 "No supported media type found"
Frame 50 - Phone1 ACKnowledge to Phone2 with parameter user=phone

Scenario 2: Phone2 try to call Phone1
Frame 187 - Phone2 send a SIP INVITE Request to Phone1 with parameter line=3uk2p3g2
Info - 		There is no SIP Status 100 TRYING send from Phone1
Frame 188 - Phone1 answers with SIP error 488 - Not Acceptable Here to Phone2
		Warning: 304 192.168.9.147 "No supported media type found"
Frame 189 - Phone2 ACKnowledge to Phone1 with parameter line=3uk2p3g2

* Suggest what could be done to make future calls between them succeed.
Phone1 is using codec g711U (ITU-T G.711 PCMU), Phone2 is using codec g711A (ITU-T G.711 PCMA)
My Suggestion:
-insure that both phones are using the same codec g711U or g711A
-check why does phone2 have as SIP contact IP address 192.168.9.181 instead of 192.168.1.102 in frame 39
