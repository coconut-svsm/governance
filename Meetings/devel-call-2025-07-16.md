# Meeting Minutes: SVSM Development Call (July 16th, 2025)

## Topics:

### Opening

*   Jon Lange led the meeting.
*   No agenda topics were submitted beforehand.

### Memory Map Exchange Between SVSM and Guest Firmware

*   Jon Lange initiated a discussion to assess the urgency of implementing a memory map exchange mechanism between the SVSM and guest firmware. This would allow the SVSM to reserve memory for its private data, such as page validation bitmaps.
*   Richard Relph confirmed that he is not currently blocked by this issue. He believes he can statically allocate the necessary memory within the SVSM image for his immediate needs.
*   Jon Lange mentioned that the long-term goal is to find an architecture-independent solution, but there is currently no active engagement from the TDX side to implement this in OVMF.
*   The consensus was to put this work on hold until there is a broader commitment to a cross-platform implementation. The topic will be revisited if new requirements make it a priority.
*   Richard Relph was asked to speak up if his situation changes.
