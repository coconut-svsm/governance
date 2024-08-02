# Meeting Minutes: SVSM Development Call (July 31st, 2024)

## Attendees:

Adam Dunlap, Carlos López, Christopher Oo, Chuanxiao Dong, Cláudio Carvalho, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, Jon Lange, Nicolai Stange, Pankaj Gupta, Peter Fang, Stefano Garzarella, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Stage1 Removal

* The group discussed removing stage1 support for the SVSM boot process.
* A decision was made to remove stage1 support in four weeks, with a PR to be opened and kept open until then.
* If no objections arise within four weeks, the PR will be merged.
* Google expressed interest in maintaining stage1 support on their own.

### Rust Version

* The group discussed the potential benefits and drawbacks of fixing the stable Rust version in the code repository.
* Arguments were made for both pinning to a specific version and using the latest stable version.
* It was decided to specify a minimum Rust version for development and a fixed Rust version in the CI to avoid random breakages.
* The `rust-toolchain.toml` file will be removed, and the makefile will be modified to compile the SVSM with the nightly Rust version.

### SVSM BoF at LPC:

* Team discussed potential benefits of hosting an SVSM BoF at the upcoming LPC conference.
* Decided to proceed with a session on Friday afternoon.
* Aim to gather feedback from a wider audience, including developers working on related components.

### Stack Unwinder Issues:

* Joerg reported fixing two issues with stack unwinding code, enabling reliable stack traces.
* Encountered stack overflows in debug builds and plans to investigate further.

### Stage2 Relocation:

* Jon shared progress on relocating Stage 2 and the kernel image.
* Team discussed implications for stack overflow handling and potential future modifications to Stage2.

### User Space Device Model:

* Peter inquired about recommendations for a network device model.
* Joerg suggested updating the existing proposal document and collaborating on a new process.

### No meeting next week

* No meeting on August 07th.
* Next meeting on August 14th.
