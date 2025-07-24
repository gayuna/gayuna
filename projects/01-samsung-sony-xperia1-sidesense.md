# From 'Impossible' to Marketed Feature: The Sony Xperia 1 Project with 'Side Sense' feature

![Side Sense](https://github.com/user-attachments/assets/0c13e4fe-8529-4251-8c23-1c3c3899140b)
Full Sony Xperia 1 trailer is available [here](https://www.youtube.com/watch?v=50CQxuVaQQI).

## The Business Context & The Challenge
While at __Samsung Electronics__, our team developed and supplied Touch Controller ICs, key B2B components for global smartphone manufacturers. To diversify revenue beyond the Samsung Galaxy series, we pursued strategic partnerships with other global brands.

Sony Mobile approached our team to supply the touch IC for their new flagship, the Xperia 1. They chose us for our unique mass-production expertise with Y-OCTA display technology, which they planned to use.

As part of the engagement, Sony requested a novel "Side Sense" feature to detect taps and slides on the curved side bezel of the display. However, the hardware team deemed this technically impossible, citing the extremely low signal-to-noise ratio on the bezel, which made distinguishing intentional touches from electrical noise unfeasible with standard methods.

## My Role: Bridging Engineering and Project Leadership
I was assigned to the Sony account as the lead software algorithm engineer for this feature. Due to my professional fluency in Japanese, I also became the primary technical point of contact for Sony's engineering teams. This dual role naturally evolved to include project management responsibilities, where I handled technical presentations, specification negotiations, and all cross-company communication, bridging the gap between our firmware team, our hardware team, and the client.

## The Action: A Pragmatic Approach to Signal Processing
My first step was to engage directly with Sony's display and QA teams. Through these conversations, I gained a crucial understanding of their intended use case and evaluation criteria. I learned that "Side Sense" was not for precision input but for simple gestures: 'double tap' to launch an app tray and 'slide' to go back.

This insight was key. It meant the system did not require the same sub-millisecond latency or single-pixel accuracy as the main touchscreen. This allowed me to architect a pragmatic software-based solution that worked around the hardware limitations by making intelligent trade-offs.

## Technical Implementation Details
The solution was a multi-stage filtering and logic algorithm implemented in C on an ARM Cortex-M microcontroller:

* __Multi-Scan Signal Averaging__: Instead of relying on a single, noisy sensor reading, the firmware scanned the bezel sensor channels multiple times for each report. The results were averaged to create a stable, filtered signal, effectively reducing momentary noise spikes.

* __Frame-Based Event Confirmation__: To eliminate phantom touches, an event was only confirmed and published to the Android OS if a touch signal persisted in the same region for two or more consecutive scan frames. This introduced a negligible amount of latency (a few milliseconds) but dramatically increased the reliability of the touch data.

* __Movement Thresholding for Gestures__: For gesture recognition, absolute precision was unnecessary. I implemented a threshold where a 'slide' event would only be generated if the confirmed touch point moved more than 100 pixels. This prevented minor jitters from being misinterpreted as gestures and ensured only intentional actions were registered.

![Image](https://github.com/user-attachments/assets/231178a2-60c1-493f-99a5-e970ef01638a)
Sony Xperia 1 II - One of 3 projects we gained after customer satisfaction.

## The Results: Exceeding Expectations and Driving Business Growth
The "Side Sense" feature was delivered on time and was a definitive success. Sony's QA team, despite being aware of the hardware challenges, rated the feature's final usability as even better than previous models that used competing pressure-sensitive solutions.

The feature was prominently showcased in the Xperia 1's global marketing campaign, validating its importance to the final product. The success of this high-stakes project and the quality of our on-site support solidified Sony's confidence in our team, directly resulting in our partnership expanding to three additional projects the following year. This project taught me the critical importance of deeply understanding user context to drive successful technical implementation.
