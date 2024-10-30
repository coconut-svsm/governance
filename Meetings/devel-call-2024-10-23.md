# Meeting Minutes: SVSM Development Call (October 23rd, 2024)

## Attendees:

Adam Dunlap, Chris Hawblitzel, Cláudio Carvalho, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, Jon Lange, Mine & John Starks, Nicolai Stange, Oliver Steffen, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj, Weidong Cui, Ziqiao Zhou

## Topics:

### Presentation and Discussion about formal verification with Verus (from Microsoft Research)

* Goal: To prove the security and correctness of the COCONUT-SVSM code using formal verification.
* Verus: A formal verification tool for Rust developed by Microsoft, CMU, and VMware ([Slides](Data/verismo-10-23-2024-talk.pdf)).
* Benefits of Verus:
  * Incremental verification without affecting development.
  * Efficient use of SMT solvers.
  * Support for proof engineering.
* Challenges:
  * False positives can occur if incorrect assumptions are made about hardware or if insufficient proof is provided.
  * Verifying complex properties can be difficult.
  * Can be time-consuming and requires specialized knowledge.
* Integration into COCONUT-SVSM:
  * Start with verifying critical components like the SVSM core protocol handling and memory allocators.
  * Incrementally add verification to the codebase.
  * Develop a plan for incremental verification.
  * Consider maintaining a separate branch for verification changes.
* Decision: Continue the discussion in the next meeting to decide on a process for integrating formal verification into COCONUT-SVSM.
