# Meeting Minutes: SVSM Development Call (September 4th, 2024)

## Attendees:

Adam Dunlap, Diego Gonzalez Villalobos, Dionna Glaze, Hajira Zaman, Huibo Wang, James Bottomley, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Rama AMD, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Vijay Dhanraj

## Topics:

### Early Attestation Process Document

* Link: [https://docs.google.com/document/d/11ZsxP8jsviP3ddp9Hrn0rf6inttNw_Pbnz0psXlxlPs/edit#heading=h.7jvpsq5illyd](Early Attestation and Measurement Architecture)
* KBS Identity: The group discussed the need for KBS identity verification. It was concluded that while it's not strictly necessary, the worst-case scenario without it is a denial of service.
* Provisioning: The initial state creation should be done offline using a tool that can register the secret into the KBS.
* TPM State: The TPM state should be considered as a secret that needs to be stored and recovered on subsequent boots.
* KBS as Untrusted Entity: The KBS should be treated as a read-only, untrusted entity.

#### Communication Channel and Protocol

* HTTP Proxy: The group discussed using an HTTP proxy as a simple communication channel between SVSM and the KBS.
* Attestation Protocol: The attestation protocol should be implemented in the SVSM.
* Negotiation Phase: A negotiation phase between SVSM and the KBS is needed to establish communication parameters.
* Attested TLS: Using attested TLS for communication between SVSM and the KBS is recommended.

#### Persistent State

* Challenges: The group discussed the challenges of maintaining a persistent state in the TPM.
* Security Concerns: Persistent state is vulnerable to replay and cloning attacks

