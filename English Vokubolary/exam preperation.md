
# Lesson 1: Telecom Basics

Teletalk Bangladesh Limited — Assistant Manager (Technical) | MCQ Crash Course

আজকের লক্ষ্য: Telecom-এর মৌলিক ধারণাগুলো বুঝে পরীক্ষায় আসতে পারে এমন MCQ উত্তর দেওয়ার প্রস্তুতি নেওয়া। প্রতিটি Topic-এ English definition, সহজ বাংলা ব্যাখ্যা, বাস্তব উদাহরণ এবং গুরুত্বপূর্ণ তথ্য থাকবে।

## Topic 1: What is Telecommunication?

Definition: Telecommunication is the transmission of information over a distance using electrical, electromagnetic, or optical signals.

বাংলায়, দূরে থাকা দুই ব্যক্তি বা দুটি ডিভাইসের মধ্যে তথ্য আদান-প্রদান করার প্রযুক্তিকে Telecommunication বলে।

Information Source

তুমি কথা বলছ

Transmitter

তথ্যকে পাঠানোর উপযোগী signal-এ রূপান্তর করে

Communication Channel

Radio wave, cable অথবা optical fiber

Receiver

Signal গ্রহণ করে তথ্য পুনরুদ্ধার করে

বাস্তব উদাহরণ: তুমি মোবাইলে কথা বললে microphone তোমার কণ্ঠকে electrical signal-এ রূপান্তর করে। ফোন সেটি প্রক্রিয়াকরণ করে radio signal হিসেবে পাঠায়। অপর প্রান্তে সেই signal থেকে কণ্ঠ পুনরুদ্ধার করা হয়।

মনে রাখবে: বাস্তব cellular network-এ Base Station, Core Network এবং আরও অনেক component থাকে। উপরের diagram হলো একটি সরলীকৃত communication model।

## Topic 2: Communication System-এর প্রধান অংশ

| Component          | কাজ                                                 |
| ------------------ | --------------------------------------------------- |
| Information Source | যে তথ্য পাঠানো হবে, সেটি তৈরি করে                   |
| Transmitter        | তথ্যকে transmission-এর উপযোগী signal-এ রূপান্তর করে |
| Channel            | Signal চলাচলের মাধ্যম                               |
| Noise              | অনাকাঙ্ক্ষিত disturbance                            |
| Receiver           | Signal গ্রহণ ও প্রক্রিয়াকরণ করে                     |
| Destination        | চূড়ান্ত তথ্য গ্রহণ করে                              |

MCQ Trap: Noise কোনো উপকারী information নয়; এটি signal-কে প্রভাবিত করতে পারে।

## Topic 3: Signal কী?

Signal হলো এমন একটি পরিবর্তনশীল physical quantity, যার মাধ্যমে তথ্য বহন করা হয়।

### Analog Signal

[How do Analog to Digital Converters (ADCs) work? | CircuitBread](https://images.openai.com/static-rsc-4/A1cS9pLhmep6lV_V8YB5LqUhjfM1XPeub8gi7WVEuASOWqgOcp2U-ZukrTM80z02drg-3uGTZaYx8ve_FtQ995uzmyTA01-r5GZDNC6bPnLVU66DjMJ9kI5aJ2jNL2daYrJ_pSGbkIZlHA8hEQYnnXoH9Rr5uqW9pxOpBw0cfJ4?purpose=inline)

[circuitbread.com](https://www.circuitbread.com/ee-faq/how-do-analog-to-digital-converters-adcs-work)

- সময়ের সঙ্গে ধারাবাহিকভাবে পরিবর্তিত হয়।
- উদাহরণ: microphone-এর analog audio output।
- এর amplitude বা frequency সময়ের সঙ্গে পরিবর্তিত হতে পারে।

### Digital Signal

[Digital Signal (Glossary Entry) – Embedded Systems](https://images.openai.com/static-rsc-4/Iol0lPtIQN6buzTsAz3UyqrtnjD03ERpANK7JVB4j-8h0dMeDVqCNi-G7AN_fvYJ43Go_Snxr9WagcVqu0WbJb3ZZDDUmL5i28BASrF2eZTVrz4I1hpQ2RPb0BX1m6Q4fw0C2Tr8KyxKoyOHAV9x8AlWYf_Ae1dQ64AgqaOoSTc?purpose=inline)

[blogs.plymouth.ac.uk](https://blogs.plymouth.ac.uk/embedded-systems/glossary-2/digital-signal-glossary-entry/)

- সাধারণ digital communication-এ discrete symbol ব্যবহার করা হয়।
- Binary data সাধারণত `0` ও `1` দিয়ে প্রকাশ করা হয়।
- উদাহরণ: computer network-এ পাঠানো digital data।

পরীক্ষার জন্য মনে রাখবে: Analog ও Digital signal-এর পার্থক্য প্রায়ই সংজ্ঞাভিত্তিক MCQ-তে কাজে লাগে। তবে digital signal বাস্তবে noisy channel-এও ত্রুটির শিকার হতে পারে।

## Topic 4: Frequency, Wavelength ও Amplitude

এই তিনটি বিষয় খুবই গুরুত্বপূর্ণ।

[How Wi-Fi Motion Sensing Works: The Physics Behind the Technology - Surety Home](https://images.openai.com/static-rsc-4/5nDWU8U1nVtderOkntd75taf9Fb2bKI3vlcwX8Bs-tg5OBspeHbcduPK9mZx7lPF8ThVSVrOnu9sZwa3YT16iWwCLm_afJ6-h5mBgAtSR0hGV1CPpV83EjFlUhOREZEc9Y03W4wPzJYUiDO6ik_YIWuO6P61F6GSOG1WAnJMaFk?purpose=inline)

Amplitude

Signal-এর সর্বোচ্চ বিচ্যুতি বা magnitude-এর পরিমাপ। সাধারণভাবে signal power-এর সঙ্গে সম্পর্কিত, কিন্তু amplitude আর power এক জিনিস নয়।

[Just a moment...](https://images.openai.com/static-rsc-4/FR4zx04LlPQZ6bhfL_XkrwQbhoz4T3t_Vl9GyRU2jv3McH7p5QmcDCAmkaDbqzBYv9aDXjcP1WJatCX98neIw-1jS8HJAiRRB6BBevg1tXamgr7AzCJNWovMmbbab_wcmZuHElylmYaqawT8h-itDbsgKTdi31Jq2f8vQvHzZJI?purpose=inline)

Frequency (\\(f\\))

প্রতি সেকেন্ডে সম্পন্ন cycle-এর সংখ্যা।

একক: Hertz (Hz)

\\(1\\,\text{MHz}=10^6\\,\text{Hz}\\)

[Wavelength Explained: Definition, Formula, Spectrum Types & Real-World Applications](https://images.openai.com/static-rsc-4/ZIXsDMfTXwCUWJcsDPmCqGjRaIFfTETW-PH8FsScfHQZ5pyAyYPLEhNWBW2svNXv1fCwvznxFhzufLhKNFkf-Cwo-oOtz-RhxcvNvBs-8_8vw5p5TNNXhrRFmkgZ4JNgHDpztLkQVUbVoNuhuI-KpjiDAyxKRmu_B37EN9q3soI?purpose=inline)

Wavelength (\\(\lambda\\))

Wave-এর পরপর দুটি সমফেজ বিন্দুর মধ্যবর্তী দূরত্ব।

একক: Meter (m)

### গুরুত্বপূর্ণ সূত্র

\\[ v=f\lambda \\]

এখানে:

- \\(v\\) = Wave propagation speed
- \\(f\\) = Frequency
- \\(\lambda\\) = Wavelength

শূন্যস্থানে electromagnetic wave-এর গতি প্রায় \\(3\times10^8\\) m/s।

উদাহরণ: একটি radio wave-এর frequency 100 MHz হলে তার free-space wavelength কত?

\\[ \lambda=\frac{v}{f} =\frac{3\times10^8}{100\times10^6} =3\text{ m} \\]

অর্থাৎ wavelength প্রায় ৩ মিটার।

Exam shortcut: একই মাধ্যমে wave speed স্থির থাকলে frequency বাড়লে wavelength কমে।

## Topic 5: Bandwidth কী?

Bandwidth হলো কোনো signal বা communication channel-এর frequency range-এর প্রস্থ।

\\[ B=f\_{\text{high}}-f\_{\text{low}} \\]

উদাহরণ: একটি channel যদি 1800 MHz থেকে 1810 MHz পর্যন্ত হয়, তবে bandwidth:

\\[ B=1810-1800=10\text{ MHz} \\]

- Bandwidth-এর একক Hz, kHz, MHz বা GHz হতে পারে।
- সাধারণভাবে বেশি bandwidth বেশি data rate অর্জনে সহায়তা করতে পারে।
- কিন্তু actual throughput নির্ভর করে signal quality, modulation, coding, interference ও অন্যান্য বিষয়ের ওপরও।

সাবধান: Frequency আর bandwidth এক নয়। Frequency একটি নির্দিষ্ট মান হতে পারে; bandwidth হলো frequency range-এর প্রস্থ।

## Topic 6: Modulation

Definition: Modulation is the process of varying a carrier signal's parameter according to the information signal.

সহজভাবে, তথ্য বহন করার জন্য একটি carrier wave-এর বৈশিষ্ট্য পরিবর্তন করা হয়।

প্রধান তিনটি analog modulation type:

| Type                      | কী পরিবর্তন হয় |
| ------------------------- | -------------- |
| AM — Amplitude Modulation | Amplitude      |
| FM — Frequency Modulation | Frequency      |
| PM — Phase Modulation     | Phase          |

Digital modulation-এর উদাহরণ:

- ASK — Amplitude Shift Keying
- FSK — Frequency Shift Keying
- PSK — Phase Shift Keying
- QAM — Quadrature Amplitude Modulation

MCQ মনে রাখবে: AM → Amplitude, FM → Frequency, PM → Phase।

## Topic 7: Noise, SNR ও Signal Quality

Noise হলো অনাকাঙ্ক্ষিত signal বা disturbance, যা communication-এর মান কমাতে পারে।

SNR = Signal-to-Noise Ratio

\\[ \mathrm{SNR}=\frac{P\_{\text{signal}}}{P\_{\text{noise}}} \\]

Power ratio-কে decibel-এ প্রকাশ করলে:

\\[ \mathrm{SNR}\_{dB}=10\log\_{10} \left(\frac{P\_{\text{signal}}}{P\_{\text{noise}}}\right) \\]

উদাহরণ: Signal power 100 mW এবং noise power 1 mW হলে:

\\[ \mathrm{SNR}=100 \\]

\\[ \mathrm{SNR}\_{dB}=20\text{ dB} \\]

সাধারণভাবে SNR বেশি হলে receiver-এর পক্ষে তথ্য নির্ভরযোগ্যভাবে উদ্ধার করা সহজ হয়।

মনে রাখবে: Signal power ও noise power একই ধরনের power quantity হলে তাদের অনুপাত unitless হয়।

## Topic 8: Simplex, Half-Duplex ও Full-Duplex

| Mode        | Communication                | উদাহরণ                         |
| ----------- | ---------------------------- | ------------------------------ |
| Simplex     | একদিকে তথ্য যায়              | সাধারণ broadcast transmission  |
| Half-duplex | দুইদিকে যায়, তবে একই সময়ে নয় | সাধারণ walkie-talkie operation |
| Full-duplex | দুইদিকে একই সময়ে তথ্য যায়    | সাধারণ telephone conversation  |
|             |                              |                                |
|             |                              |                                |

এগুলো প্রায়ই সহজ MCQ-র জন্য উপযোগী।

## Topic 9: Telecom-এর সঙ্গে সম্পর্কিত একক

| Quantity                 | Unit               |
| ------------------------ | ------------------ |
| Frequency                | Hz                 |
| Wavelength               | m                  |
| Bandwidth                | Hz                 |
| Power                    | Watt (W)           |
| Voltage                  | Volt (V)           |
| Resistance               | Ohm (\\(\Omega\\)) |
| Data rate                | bit/s, Mbps, Gbps  |
| Signal power ratio in dB | Decibel (dB)       |
|                          |                    |

dB হলো logarithmic ratio প্রকাশের একক; dBm হলো 1 mW reference-এর তুলনায় power level প্রকাশ করে।

উদাহরণ: 0 dBm = 1 mW।

# Lesson 1 — MCQ Practice Test

প্রথমে নিজে উত্তর দাও। এরপর উত্তর যাচাই করো বাটনে চাপলে স্কোর ও ব্যাখ্যা দেখতে পারবে।

## Lesson 1 Quiz

0/10 উত্তর

1\. Telecommunication-এর প্রধান উদ্দেশ্য কী?

A. শুধু বিদ্যুৎ উৎপাদন

B. দূরত্ব অতিক্রম করে তথ্য আদান-প্রদান

C. শুধু data store করা

D. শুধু computer তৈরি

2\. Frequency-এর SI unit কোনটি?

A. Watt

B. Volt

C. Hertz

D. Ohm

3\. 100 MHz frequency-এর free-space wavelength কত?

A. 30 m

B. 3 m

C. 0.3 m

D. 300 m

4\. Bandwidth-এর সঠিক সংজ্ঞা কোনটি?

A. দুটি frequency-র পার্থক্য

B. Signal-এর voltage

C. শুধু carrier amplitude

D. Noise-এর power

5\. AM-এ carrier-এর কোন বৈশিষ্ট্য পরিবর্তিত হয়?

A. Phase only

B. Amplitude

C. Wavelength only

D. Resistance

6\. FM-এ কোন বৈশিষ্ট্য পরিবর্তিত হয়?

A. Frequency

B. Amplitude only

C. Resistance

D. Battery capacity

7\. সাধারণভাবে ভালো signal quality-এর সঙ্গে কোনটি সম্পর্কিত?

A. উচ্চ SNR

B. শুধু বেশি noise

C. শূন্য bandwidth

D. শুধু কম frequency

8\. Walkie-talkie-এর সাধারণ push-to-talk operation কোন mode?

A. Simplex only

B. Half-duplex

C. Full-duplex

D. No communication

9\. 0 dBm কত power-এর সমান?

A. 1 W

B. 1 mW

C. 10 mW

D. 0 W

10\. Signal বহন করার জন্য carrier-এর phase পরিবর্তনের পদ্ধতি কোনটি?

A. AM

B. FM

C. PM

D. Rectification

উত্তর যাচাই করো

## পরীক্ষার আগে ১ মিনিটের Revision

- Frequency → Hz
- Wavelength → Meter
- Bandwidth → $\\(f\_{\text{high}}-f\_{\text{low}}\\)$
- Wave speed → $\\(v=f\lambda\\)$
- AM → Amplitude পরিবর্তন
- FM → Frequency পরিবর্তন
- PM → Phase পরিবর্তন
- SNR বেশি → সাধারণত ভালো signal quality
- 0 dBm → 1 mW
- Simplex → একদিকে; Half-duplex → পালাক্রমে; Full-duplex → একই সময়ে দুইদিকে

পরবর্তী লেসন: Lesson 2 — Radio Communication Basics: RF spectrum, antenna, propagation, path loss, fading, interference, SNR, dB/dBm এবং গুরুত্বপূর্ণ পরীক্ষাভিত্তিক MCQ।

----
# Lesson 2: Radio Communication Basics

Teletalk Bangladesh Limited — Assistant Manager (Technical) | MCQ Crash Course

এই লেসনে আমরা শিখব Radio Frequency (RF), Electromagnetic Waves, Antenna, Radio Propagation, Path Loss, Fading, Interference, dB/dBm এবং Link Budget। এগুলো তোমার দেওয়া সিলেবাসের Radio Communication Basics অংশের জন্য প্রাসঙ্গিক।

## Topic 1: What is Radio Communication?

Definition: Radio communication is the transmission of information through electromagnetic waves, typically in the radio-frequency spectrum, without requiring a physical cable between transmitter and receiver.

সহজভাবে, মোবাইল ফোন থেকে কাছের cellular tower-এ যে wireless signal যায়, সেটি radio communication-এর উদাহরণ।

Mobile Transmitter

Electrical/RF signal তৈরি করে

Wireless radio link — electromagnetic wave-এর মাধ্যমে

Base Station Receiver

Signal গ্রহণ করে network-এ পাঠায়

বাস্তবে cellular phone ও base station—দুই দিকেই transmit এবং receive করার ব্যবস্থা থাকে।

## Topic 2: Radio Frequency (RF) Spectrum

Radio frequency হলো electromagnetic signal-এর frequency range-এর একটি অংশ।

### প্রচলিত RF Bands

### kHz

Low-frequency radio bands

উদাহরণ: LF — 30–300 kHz

### MHz

VHF / UHF

VHF: 30–300 MHz; UHF: 300 MHz–3 GHz

অনেক cellular band UHF range-এ অবস্থিত।

### GHz

SHF

3–30 GHz; 5G-এর কিছু band এই range-এ পড়ে।

### পরীক্ষায় মনে রাখবে

| Prefix | মান           |
| ------ | ------------- |
| 1 kHz  | \\(10^3\\) Hz |
| 1 MHz  | \\(10^6\\) Hz |
| 1 GHz  | \\(10^9\\) Hz |

MCQ fact: UHF-এর frequency range হলো 300 MHz থেকে 3 GHz।

## Topic 3: Electromagnetic Wave ও Antenna

Electromagnetic wave-এর মাধ্যমে wireless communication সম্ভব হয়। Antenna বৈদ্যুতিক RF signal ও radiated electromagnetic wave-এর মধ্যে শক্তি স্থানান্তর করে।

### Antenna-এর প্রধান কাজ

- Transmit antenna: RF energy radiate করে।
- Receive antenna: আগত electromagnetic wave থেকে signal গ্রহণ করে।
- Antenna gain: নির্দিষ্ট দিকে radiation কতটা কেন্দ্রীভূত, তার পরিমাপ।
- Polarization: electromagnetic wave-এর electric field-এর orientation।

[Стоимость интернета в Таджикистане: новые тарифы 2025](https://images.openai.com/static-rsc-4/lVN94WYH17BPdxiPInyiNYdYgWrefOEl2Lmfihn4WY1W7r3EyZa6z-rwiWMn4MToufady-sUiGEJgvp_fz9BYV-1ZyO4F0jySCq0NpTXjLlYgcztOAirjoIhxQfwjHsuaAmXiL5P9Ub8_04yniVBXfAaNEdS7T1OKsIVuxMVrQE?purpose=inline)

[Altycom - Services](https://images.openai.com/static-rsc-4/po9XFjxmzXAHMZsi0K-B1kpEeAYJttrKNmcf4VAveR5GWFsHG3qjAxdBlmGVqV0LbC6VvAq3PA_FA41uuSgN1f62ZcNTGeF8l4Hcq_812mxsVyQ36eRm9cEpYPNgJNwmQf0tXDzWwrYUgRAOvFlq2RhgUisrDJ9WpFYcBIU6TAg?purpose=inline)

[When to use omni-directional antenna?](https://images.openai.com/static-rsc-4/5kYgeJ5drtke6vAhhbla5RAe57JiumG48Sicznym5LFej4a3GIQVmIc3ROYqqI9xbUiXxLheYh5E_6Wnf2uC3dBv5SHi8ome2fDmtooE3FC-xhXR-jgGkeMmY40oQL7whuMCAmrGKkAUBCfo8d63MtCRRKWszDItYwYSTo9oFvI?purpose=inline)

8

### Direction অনুযায়ী antenna

- Omnidirectional: horizontal plane-এ সব দিকে প্রায় সমানভাবে radiate করে।
- Directional: নির্দিষ্ট দিকে বেশি radiation কেন্দ্রীভূত করে।
- Sector antenna: নির্দিষ্ট angular sector কভার করে; cellular tower-এ বহুল ব্যবহৃত।

গুরুত্বপূর্ণ: Antenna gain শক্তি তৈরি করে না; এটি নির্দিষ্ট দিকে radiation distribution পরিবর্তন করে। Gain সাধারণত dBi বা dBd-এ প্রকাশ করা হয়।

## Topic 4: Radio Wave Propagation

Radio propagation হলো transmitter থেকে receiver পর্যন্ত radio wave ছড়িয়ে পড়ার প্রক্রিয়া।

প্রধান তিনটি propagation mechanism:

[Understanding UHF VHF HF Radio: Key Differences and Military Applications](https://images.openai.com/static-rsc-4/f72jww-rDL2kchexLDm8Ydzsuy07HJoo4uI-ZMjFihsV2UbRsMEXFi8-Xi_qxxTpcP7Tpufzhd0RXhVM-RylZwpCdicy8zJkvsXp3GGlGFFrg5c05qPdaWRPdcJXxP1xd-FPth1rPI54fRz7zRJ0o3Hjw9szZWycBMlu_KdtgCU?purpose=inline)

1\. Line of Sight (LOS)

Transmitter ও receiver-এর মধ্যে সরাসরি পথ থাকে। Microwave point-to-point link-এ এটি গুরুত্বপূর্ণ।

[Understanding Reflection, Diffraction, and Scattering](https://images.openai.com/static-rsc-4/Iegr7fKC95Q9p6FxpEPkNnvXZpKpcZeVR_7TKVtBxDEHuGjVhNmUoadKjxUIT0sFRQhFs4mAFCLCso1UQ4W4D-iARjR2sew9vHTCHkm5qE7xrG90u2Jl-6sf1vSPRI-44bc-lUZxF0LJTcAA5n0h-Ulr-WOSq3vQ-QdViYaqYpM?purpose=inline)

2\. Reflection, Diffraction ও Scattering

- Reflection: কোনো পৃষ্ঠ থেকে wave প্রতিফলিত হয়।
- Diffraction: বাধার কিনারা ঘুরে wave ছড়িয়ে যেতে পারে।
- Scattering: ছোট বা অনিয়মিত বস্তু থেকে wave বিভিন্ন দিকে ছড়িয়ে পড়ে।

[Project 2](https://images.openai.com/static-rsc-4/lsub3fQSVTAB6OGUL5cc0_bHx3lTe4kvrGpUgA6nuC1egMMTNEbA09QmucM8blmeFTe2yMEs1Lc8f02eLDKqosFOwCtKEEPuZHJoAAJkOIy7vnG0z06qK7-tE7lM97hgJDERlBWeuwGUiGPVoDUwmrvJpId360Kf-VDywao0lmw?purpose=inline)

3\. Multipath Propagation

একই signal-এর একাধিক প্রতিফলিত বা ভিন্ন পথে আসা copy receiver-এ পৌঁছায়। এগুলো constructive বা destructive interference সৃষ্টি করতে পারে।

পরীক্ষার জন্য: Multipath fading এবং shadowing এক জিনিস নয়। Multipath-এর কারণে signal-এর amplitude বা phase বদলাতে পারে; shadowing সাধারণত বড় বাধা, যেমন ভবন বা পাহাড়ের কারণে signal কমে যাওয়াকে বোঝায়।

## Topic 5: Path Loss ও Free-Space Path Loss

দূরত্ব বাড়লে সাধারণত transmitter থেকে পাওয়া signal power কমে। Transmission path-এ signal power কমে যাওয়ার এই প্রভাবকে path loss বলা হয়।

### Free-Space Path Loss (FSPL)

শূন্য বাধার আদর্শ free-space model-এর জন্য:

\\[ FSPL(dB)=32.44+20\log\_{10}(f\_{\mathrm{MHz}}) +20\log\_{10}(d\_{\mathrm{km}}) \\]

এখানে frequency MHz-এ এবং distance km-এ নিতে হবে।

উদাহরণ: Frequency 900 MHz এবং distance 1 km হলে:

\\[ FSPL=32.44+20\log\_{10}(900) +20\log\_{10}(1) \\]

\\[ FSPL\approx91.5\text{ dB} \\]

এটি ideal free-space loss; বাস্তব cellular network-এ building penetration, terrain, interference, antenna pattern এবং fading-এর কারণে ফল ভিন্ন হতে পারে।

### High-yield facts

- দূরত্ব দ্বিগুণ হলে free-space path loss প্রায় 6 dB বাড়ে।
- Frequency দ্বিগুণ হলে একই দূরত্বে free-space path loss প্রায় 6 dB বাড়ে।
- বাস্তব network-এর propagation model আরও জটিল।

## Topic 6: Fading, Shadowing ও Interference

| বিষয়         | অর্থ                               | উদাহরণ                                            |
| ------------ | ---------------------------------- | ------------------------------------------------- |
| Fading       | Signal level-এর পরিবর্তন           | Multipath-এর কারণে signal ওঠানামা                 |
| Shadowing    | বড় বাধার কারণে signal কমে যাওয়া    | ভবনের আড়ালে mobile                                |
| Interference | অন্য signal-এর অনাকাঙ্ক্ষিত প্রভাব | একই বা কাছাকাছি frequency-র unwanted transmission |
| Noise        | অনাকাঙ্ক্ষিত random disturbance    | Receiver electronics-এর thermal noise             |

### Interference-এর সাধারণ ধরন

- Co-channel interference: একই frequency channel পুনর্ব্যবহারের কারণে এক cell-এর signal অন্য cell-কে প্রভাবিত করে।
- Adjacent-channel interference: পাশের frequency channel থেকে অনাকাঙ্ক্ষিত leakage বা insufficient filtering-এর প্রভাব।

মনে রাখবে: Cellular network-এ frequency planning, power control, filtering এবং network optimization interference কমাতে সাহায্য করে।

## Topic 7: dB, dBm ও dBi

এই তিনটি term খুব গুরুত্বপূর্ণ।

| Term | কী বোঝায়                                       |
| ---- | ---------------------------------------------- |
| dB   | Power বা অন্য অনুপাতের logarithmic expression  |
| dBm  | 1 mW reference-এর তুলনায় absolute power level  |
| dBi  | Ideal isotropic antenna-এর তুলনায় antenna gain |

### dBm-এর উদাহরণ

\\[ P\_{\mathrm{dBm}}=10\log\_{10}(P\_{\mathrm{mW}}) \\]

| Power         | dBm    |
| ------------- | ------ |
| 1 mW          | 0 dBm  |
| 10 mW         | 10 dBm |
| 100 mW        | 20 dBm |
| 1000 mW (1 W) | 30 dBm |

### dB যোগ-বিয়োগের নিয়ম

একটি simplified link budget:

\\[ P_r=P_t+G_t+G_r-L \\]

এখানে সব power/gain/loss dB-ভিত্তিক compatible unit-এ প্রকাশ করতে হবে; \\(P_t\\) এবং \\(P_r\\) সাধারণত dBm-এ, antenna gains ও losses dB-এ।

উদাহরণ:

- Transmit power = 30 dBm
- Transmit antenna gain = 10 dBi
- Receive antenna gain = 0 dBi
- Total path loss = 100 dB

আদর্শ হিসাব:

\\[ P_r=30+10+0-100=-60\text{ dBm} \\]

এখানে অন্য cable বা system loss ধরা হয়নি।

## Topic 8: Link Budget

Link budget দিয়ে transmitter থেকে receiver পর্যন্ত আনুমানিক received power হিসাব করা হয়।

\\[ \text{Received Power} =\text{Transmit Power} +\text{Gains} -\text{Losses} \\]

প্রধান উপাদান:

1. Transmit power
2. Transmit antenna gain
3. Propagation/path loss
4. Cable ও connector losses
5. Receive antenna gain

MCQ fact: Link budget-এ gain যোগ হয়, loss বিয়োগ হয়।

# Lesson 2: গুরুত্বপূর্ণ MCQ Test

## Radio Communication Quiz

0/10

প্রথমে উত্তর দাও, শেষে ব্যাখ্যাসহ ফলাফল দেখো।

1\. Radio communication-এর মাধ্যম কী?

A. শুধু copper cable

B. Electromagnetic waves

C. শুধু water waves

D. Mechanical gears

2\. UHF band-এর সাধারণ frequency range কোনটি?

A. 3–30 kHz

B. 30–300 kHz

C. 300 MHz–3 GHz

D. 30–300 GHz

3\. Antenna gain সাধারণত কোন unit-এ প্রকাশ করা হয়?

A. dBi

B. dBm only

C. Hertz

D. Ohm

4\. Multipath propagation বলতে কী বোঝায়?

A. Signal-এর একটিমাত্র পথ

B. একাধিক পথে signal-এর receiver-এ পৌঁছানো

C. শুধু cable transmission

D. Battery discharge

5\. Shadowing-এর একটি সাধারণ কারণ কী?

A. Building obstruction

B. শুধু battery voltage

C. Data compression

D. SIM PIN

6\. Free-space distance দ্বিগুণ হলে path loss আনুমানিক কত বাড়ে?

A. 1 dB

B. 3 dB

C. 6 dB

D. 20 dB

7\. 100 mW power কত dBm?

A. 0 dBm

B. 10 dBm

C. 20 dBm

D. 30 dBm

8\. Co-channel interference কী?

A. একই channel ব্যবহারের কারণে অনাকাঙ্ক্ষিত প্রভাব

B. Battery charging

C. Signal encryption

D. Optical fiber fusion

9\. 900 MHz frequency-তে 1 km free-space path loss আনুমানিক কত?

A. 31.5 dB

B. 61.5 dB

C. 91.5 dB

D. 121.5 dB

10\. Link budget-এ antenna gain কীভাবে বিবেচনা করা হয়?

A. যোগ করা হয়

B. সবসময় বিয়োগ করা হয়

C. Frequency হিসেবে ধরা হয়

D. সম্পূর্ণ বাদ দেওয়া হয়

উত্তর যাচাই করো

## শেষ মুহূর্তের Revision Sheet

- $RF = Radio Frequency$
- $UHF = 300 MHz–3 GHz$
- $Antenna gain = dBi বা dBd$
- $\\(v=f\lambda\\)$
- $Multipath = একাধিক propagation path$
- $Shadowing = বড় বাধার কারণে signal attenuation$
- $Fading = signal level-এর পরিবর্তন$
- $\\(FSPL \propto 20\log\_{10}(d)\\) এবং \\(20\log\_{10}(f)\\)$
- $10 dBm = 10 mW$
- $20 dBm = 100 mW$
- $Link budget = Transmit power + Gains − Losses$

পরবর্তী লেসন: Lesson 3 — Cellular Network Fundamentals: Cell, BTS, NodeB, eNodeB, gNodeB, Frequency Reuse, Sectorization, Handover, Roaming, RAN এবং গুরুত্বপূর্ণ MCQ।

# Lesson 3: Cellular Network Fundamentals

Teletalk Bangladesh Limited — Assistant Manager (Technical) | MCQ Crash Course

আজকের লেসনে শিখবে কীভাবে একটি mobile network কাজ করে, Cell ও BTS কী, 2G/3G/4G/5G Base Station-এর পার্থক্য, Frequency Reuse, Sectorization, Handover, Roaming এবং RAN Architecture।

আজকের লক্ষ্য: Cellular Network নিয়ে গুরুত্বপূর্ণ সংজ্ঞা, component-এর কাজ ও পার্থক্যভিত্তিক MCQ-র উত্তর দিতে পারা।

## Topic 1: What is a Cellular Network?

Definition: A cellular network is a wireless communication network divided into geographical areas called cells, each served by a base station or radio access equipment.

সহজভাবে, একটি বড় এলাকাকে অনেক ছোট ছোট এলাকায় ভাগ করে mobile communication পরিচালনা করা হয়। প্রতিটি এলাকাকে বলা হয় Cell।

[PPT - Ch1 Introduction to Wireless Communications &amp; Networks PowerPoint Presentation - ID:5580067](https://images.openai.com/static-rsc-4/2dbX57Ry3jIcPUOIxoB6prjFWzKegQKo5evGcO9XZB16T8aO8TDmcIzM8VIzXoLlQm5YOUA6O8ndWcrZDewcQLD0ZrjIXs8qxP6ETMMhl8_xHuh3faCcbSO6xxrh32dpSR8jjUc4iZ6qCll8na44VzvEgXsixrUxA7vVUPRHcdY?purpose=inline)

[slideserve.com](https://www.slideserve.com/curt/ch1-introduction-to-wireless-communications-networks)

উদাহরণ: ঢাকা শহরের বিভিন্ন এলাকায় একাধিক cellular site থাকে। তুমি এক এলাকা থেকে অন্য এলাকায় চলাচল করলে তোমার ফোন প্রয়োজন অনুযায়ী অন্য cell-এর সঙ্গে সংযোগ স্থাপন করতে পারে।

Cellular network ব্যবহারের সুবিধা:

- একই spectrum পরিকল্পিতভাবে একাধিক এলাকায় ব্যবহার করা যায়।
- বৃহৎ এলাকায় wireless coverage দেওয়া যায়।
- ব্যবহারকারীর অবস্থান পরিবর্তনের সঙ্গে connection পরিচালনা করা যায়।
- বিভিন্ন cell-এ radio resources ভাগ করে network capacity বাড়ানো যায়।

## Topic 2: Cell, Site, Sector ও Coverage

এই চারটি শব্দের পার্থক্য বুঝতে হবে।

[Hexagons in 3D – Is it time to update the defining image of the cellular industry? | Real Wireless Weblog](https://images.openai.com/static-rsc-4/yy0YsIrKWTGfuTtd714W3n0Zwso_C3pOP0vbjC2Jk2C7y2dMA5wdm3KrzJlKONgjqO8ALz2tlXOCEZolAXyBByd_BmLqjkvSauQA9zfDCwFrbsWwEZpvnFtyf6jbwLC_fAmB5CT7Rf1IBI1ZGWMjV8K_FkmktnahKm6_YI4kS9Q?purpose=inline)

1\. Cell

একটি নির্দিষ্ট radio coverage area, যেখানে mobile device একটি radio access point-এর মাধ্যমে network-এ যুক্ত হয়।

[Off-Grid Power Solutions | Commercial Solar Energy Company | AJC](https://images.openai.com/static-rsc-4/JxTqLyGzre2KV3jk-0cTFy0HCOYD2WXrvz-2fe3cNPcZEx4G45enljj3P3yBp8uRvD0rNOeKY5UpKYfstij80l2P4rHFd4CccgZ6jPXqTHAB8Ggz0OlZ9Yt-vYKWlQxyAeVYhob2NeyHLwJjhay5uokTvqxsvGyku3d_JgZR25c?purpose=inline)

2\. Cell Site

বাস্তব স্থাপনা বা location, যেখানে antenna, radio equipment ও অন্যান্য network equipment থাকতে পারে।

[Location traces in criminal investigations — ROXANNE](https://images.openai.com/static-rsc-4/RKLfZzDqes-OpOxasNkuMIZyF3QRQg32dAW1DKFXXf5lSR8vzSjxLjIWPNJdHWdj6Kz31X-vV7xxnEiJxju1YjCblYisXcZrvTCnmwmGkn0C3KymSiTn4VrSTg7zfEcoUDVV0av1Fu97cg62gtjug55CD-Wc7agXGrco_6NApys?purpose=inline)

3\. Sector

একটি cell site-এর coverage-কে একাধিক directional radio sector-এ ভাগ করা যায়। প্রচলিত উদাহরণ হলো তিনটি sector, প্রতিটি প্রায় 120°।

[(a) Cell tower distribution and cellular network coverage. (b)... | Download Scientific Diagram](https://images.openai.com/static-rsc-4/T3hPszHQ05q1L9ovrv-JKE3P2C16vrXV39wNDtyHe2O35UP26XPcWak2uST2VmQCEXzszPju2Q8IJxCnXsPammkTlPLj7oZaBd1_yhpK4YXGkmfUScEbyY6sDLZ4FLisMPFrOCu5ReeCt7Mq3wGja0MiYigBADMQJeHNG2iJ8ZA?purpose=inline)

4\. Coverage

যে এলাকায় একটি radio service ব্যবহারযোগ্য signal দিতে পারে। বাস্তব coverage terrain, buildings, frequency, antenna এবং interference-এর ওপর নির্ভর করে।

Exam trap: একটি tower বা site মানেই একটি cell নয়। একটি site-এ একাধিক sector বা cell থাকতে পারে।

## Topic 3: BTS, NodeB, eNodeB ও gNodeB

এগুলো mobile network-এর radio access equipment-এর সঙ্গে সম্পর্কিত গুরুত্বপূর্ণ নাম।

| Technology | Base station terminology |
| ---------- | ------------------------ |
| 2G GSM     | BTS                      |
| 3G UMTS    | NodeB                    |
| 4G LTE     | eNodeB / eNB             |
| 5G NR      | gNodeB / gNB             |

### কাজ কী?

- BTS: GSM mobile-এর সঙ্গে radio communication করে।
- NodeB: UMTS/3G radio access-এর base station।
- eNodeB: LTE/4G radio access পরিচালনা করে এবং LTE architecture-এ EPC-এর সঙ্গে যুক্ত থাকে।
- gNodeB: 5G NR radio access পরিচালনা করে এবং 5G architecture-এ 5GC বা deployment অনুযায়ী অন্য network architecture-এর সঙ্গে যুক্ত হতে পারে।

### মুখস্থ রাখার কৌশল

2G → BTS → GSM

3G → NodeB → UMTS

4G → eNodeB → LTE

5G → gNodeB → NR

## Topic 4: RAN — Radio Access Network

RAN হলো mobile network-এর সেই অংশ, যার মাধ্যমে mobile device radio link ব্যবহার করে network-এ প্রবেশ করে।

UE — User Equipment

Mobile phone বা অন্য device

RAN — Radio Access Network

BTS / NodeB / eNodeB / gNodeB — technology অনুযায়ী

Core Network

Subscriber management, session control, routing ও অন্যান্য service

মনে রাখবে:

- UE = User Equipment।
- RAN = Radio Access Network।
- Core Network = radio access-এর বাইরে subscriber, mobility, session ও service-সংক্রান্ত network functions-এর অংশ।
- Backhaul RAN site-কে aggregation বা core network-এর দিকে সংযুক্ত করে।

## Topic 5: Frequency Reuse

Cellular network-এর একটি প্রধান ধারণা হলো Frequency Reuse।

একই frequency channel যথাযথ দূরত্বে থাকা একাধিক cell-এ পুনরায় ব্যবহার করা যায়, যাতে সীমিত spectrum দিয়ে বেশি ব্যবহারকারীকে service দেওয়া সম্ভব হয়।

[File:Frequency reuse.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/Ru5cRwP09WzG4jjRXqI8VjIH0ev1kSQQy3Xtfsd0otV5MzGeahHkE9PYx3N0s6e9v7msnXFw6Fm0ebm3-BhCX7WrWyq7O9b2LPvwemo5oOnt0-K5j6Ab1UoR_QNWJ3L4k73Oc3Pt9nK52XuRpnk5SVnbx2PO2V_0gn7eCUr12zI?purpose=inline)

[commons.wikimedia.org](https://commons.wikimedia.org/wiki/File%3AFrequency_reuse.svg)

### কেন প্রয়োজন?

ধরো, একটি operator-এর কাছে সীমিত spectrum আছে। একই frequency একটিমাত্র এলাকায় ব্যবহার করলে capacity সীমিত হয়ে যাবে। তাই পরিকল্পিতভাবে আলাদা cell-এ frequency পুনর্ব্যবহার করা হয়।

তবে একই frequency খুব কাছাকাছি cell-এ ব্যবহৃত হলে Co-channel Interference হতে পারে।

### Frequency Reuse Factor

প্রচলিত hexagonal cellular planning model-এ cluster size:

$\\[ N=i^2+ij+j^2 \\]$

এখানে \\(i\\) ও \\(j\\) হলো non-negative integer। Idealized reuse factor:

$\\[ K=\frac{1}{N} \\]$

উদাহরণ: \\(i=2,\ j=1\\) হলে,

\\[ $N=2^2+(2)(1)+1^2=7$ \\]

সুতরাং idealized frequency reuse factor:

\\[ K=\frac{1}{7} \\]

এই সূত্রটি traditional hexagonal frequency-planning model-এর জন্য; আধুনিক LTE/5G-তে scheduling ও interference coordination-এর মতো আরও পদ্ধতি ব্যবহৃত হয়।

## Topic 6: Sectorization

একটি cell site-এর antenna coverage-কে বিভিন্ন directional sector-এ ভাগ করাকে Sectorization বলে।

[Introduction to Nokia Base Stations  BSS S10.5 ED | PPT](https://images.openai.com/static-rsc-4/0FfyM15BntIz4Ugrw-2fDU5wyUfr4Mx10UFmCuqlSbyIeiC3jnenPrP6hsvkJ7AM0nDQOfk-e_uJSI2aQ4fXoVEewdcv5BWldibsO_-iH4j3W1hEEDAhMpmtC8UGQRuq0prdBdIVkBFddh1LjEoQjRcCxwe2L32FDkQ8tq4NGXA?purpose=inline)

[slideshare.net](https://www.slideshare.net/slideshow/introduction-to-nokia-base-stations-bss-s10-5-ed/274278387)

### সুবিধা

- Directional coverage পাওয়া যায়।
- Capacity ও frequency reuse পরিকল্পনায় সহায়তা করে।
- নির্দিষ্ট এলাকায় radio resources আরও কার্যকরভাবে ব্যবহার করা যায়।
- উপযুক্ত planning-এ interference নিয়ন্ত্রণে সহায়তা করতে পারে।

MCQ fact: তিনটি সমান sector হলে প্রতিটির nominal angle \\(360^\circ/3=120^\circ\\)। বাস্তবে antenna beamwidth এবং coverage boundary সবসময় নিখুঁত 120° হয় না।

## Topic 7: Handover / Handoff

Definition: Handover is the transfer of an active mobile connection from one cell or radio access point to another while maintaining service continuity.

সহজভাবে, তুমি ফোনে কথা বলছ এবং চলন্ত অবস্থায় এক cell থেকে অন্য cell-এ যাচ্ছ। তখন network তোমার connection নতুন cell-এ স্থানান্তর করতে পারে। এটিই handover।

[\[Network\] 이동통신의 꽃 핸드오버↗ ˙  Handover ˙ HO :: dokylee's Tech Blog](https://images.openai.com/static-rsc-4/4rEZ4upRLz6YlNYL8xCGUeelfEVP6PtSLi_pyu3jyxQ2lAZWyuFEyjpGanZR3GD0wlEumWUsXfbo3DL2bP10fX-28SW4ZN1TzJFy8-0D61ecogp-nzvacCbWDIZ2bW0eghWH_SHvC8HYvGPL_4CzTsDDFB0Tr-BNlY_XR34bMO8?purpose=inline)

[dokylee.tistory.com](https://dokylee.tistory.com/10)

### Handover-এর ধরন

- Hard Handover: পুরোনো radio link ছাড়ার পর নতুন link স্থাপন করা হয়—break-before-make ধারণা।
- Soft Handover: কিছু প্রযুক্তিতে নতুন link যুক্ত হওয়ার সময় পুরোনো link-ও সাময়িকভাবে বজায় থাকে—make-before-break ধারণা।

Soft handover ঐতিহ্যগতভাবে CDMA/UMTS-জাতীয় ব্যবস্থার সঙ্গে সম্পর্কিত; এটি সব cellular technology-তে ব্যবহৃত হয় না।

### Handover বনাম Roaming

| Handover                              | Roaming                                                     |
| ------------------------------------- | ----------------------------------------------------------- |
| Cell বা radio access point পরিবর্তন   | অন্য network/operator-এর coverage বা service ব্যবহার        |
| চলমান connection বজায় রাখার প্রক্রিয়া | Subscriber-এর home network-এর বাইরে service পাওয়ার ব্যবস্থা |
| একই operator-এর network-এ প্রায়ই ঘটে  | অন্য operator-এর network-এ হতে পারে                         |

Exam trap: Handover আর roaming এক নয়।

## Topic 8: Location Update ও Mobility Management

Mobile device-এর অবস্থান ও সংযোগ পরিচালনার জন্য network-কে বিভিন্ন তথ্য বজায় রাখতে হয়।

- Mobility Management: ব্যবহারকারী চলাচল করলে network access ও reachability পরিচালনা।
- Location Update / Registration: নির্দিষ্ট technology অনুযায়ী device-এর অবস্থান বা registration তথ্য আপডেট।
- Paging: incoming call বা data-এর জন্য idle অবস্থায় থাকা device-কে খুঁজে বের করার প্রক্রিয়ার অংশ।
- Handover: সক্রিয় connection অন্য cell বা radio access point-এ স্থানান্তর।

এগুলো আলাদা কাজ হলেও পরস্পরের সঙ্গে সম্পর্কিত।

## Topic 9: Roaming ও Network Coverage

Roaming হলো এমন ব্যবস্থা, যার মাধ্যমে subscriber নিজের home network-এর বাইরে অন্য অনুমোদিত network ব্যবহার করে service পেতে পারে।

উদাহরণ: একজন subscriber বিদেশে গিয়ে roaming agreement থাকা operator-এর network-এ ফোন ব্যবহার করতে পারেন।

Roaming-এর ক্ষেত্রে গুরুত্বপূর্ণ বিষয়:

- Home network ও visited network-এর মধ্যে agreement ও coordination।
- Subscriber authentication।
- Service authorization এবং charging।
- Network technology ও device compatibility।

মনে রাখবে: Roaming শুধু বিদেশে নয়; দেশের ভেতরেও প্রাসঙ্গিক হতে পারে, যদি operator ও network arrangement তা সমর্থন করে।

# Lesson 3: High-Yield MCQ Test

এখন ১৫টি প্রশ্ন দিয়ে নিজেকে যাচাই করো। এগুলো সিলেবাসভিত্তিক অনুশীলনী; আসল বা পূর্ববর্তী পরীক্ষার প্রশ্ন নয়।

## Cellular Network Quiz

0/15

1\. GSM-এর base station-এর নাম কী?

A. NodeB

B. BTS

C. eNodeB

D. gNodeB

2\. LTE/4G base station-কে কী বলা হয়?

A. BTS

B. NodeB

C. eNodeB

D. HLR

3\. 5G NR-এর base station কোনটি?

A. gNodeB

B. BTS

C. NodeB

D. SGW

4\. Cellular network-এ Frequency Reuse-এর প্রধান উদ্দেশ্য কী?

A. Spectrum efficiency বাড়ানো

B. সব interference দূর করা

C. Battery capacity বাড়ানো

D. IP address মুছে ফেলা

5\. একটি তিন-sector site-এর প্রতিটি sector-এর nominal angle কত?

A. 60°

B. 90°

C. 120°

D. 180°

6\. Handover-এর প্রধান উদ্দেশ্য কী?

A. Active connection অন্য cell-এ স্থানান্তর করা

B. SIM তৈরি করা

C. Frequency spectrum বিক্রি করা

D. Battery charge করা

7\. RAN-এর পূর্ণরূপ কী?

A. Radio Access Network

B. Remote Antenna Number

C. Radio Allocation Node

D. Routing Access Name

8\. UE বলতে কী বোঝায়?

A. User Equipment

B. Universal Ethernet

C. Uplink Engine

D. User Encryption

9\. Cell site ও cell সম্পর্কে কোনটি সঠিক?

A. একই শব্দ, সবসময় একই অর্থ

B. একটি site-এ একাধিক sector/cell থাকতে পারে

C. একটি cell অবশ্যই একটি country

D. একটি site-এ antenna থাকতে পারে না

10\. Co-channel interference কখন হতে পারে?

A. একই frequency-তে অন্য transmission প্রভাব ফেললে

B. কোনো radio signal না থাকলে

C. শুধু battery charge হলে

D. শুধু optical fiber কাটলে

11\. Hard handover কোন ধারণার সঙ্গে সম্পর্কিত?

A. Break-before-make

B. Make-before-break only

C. No radio link change

D. Roaming billing only

12\. Roaming কী?

A. শুধু antenna rotation

B. Home network-এর বাইরে অনুমোদিত network service ব্যবহার

C. একটি cell-এর মধ্যে frequency পরিবর্তনমাত্র

D. শুধু call recording

13\. একটি hexagonal cluster-এ i=2 এবং j=1 হলে N কত?

A. 5

B. 6

C. 7

D. 9

14\. Paging-এর সাধারণ উদ্দেশ্য কী?

A. Idle device-কে incoming service-এর জন্য খুঁজে পাওয়া

B. Antenna gain তৈরি করা

C. AC-কে DC করা

D. Frequency unit পরিবর্তন

15\. Backhaul সাধারণত কী সংযুক্ত করে?

A. Radio access site-কে aggregation/core network-এর দিকে

B. শুধু microphone-কে speaker-এর সঙ্গে

C. SIM-কে battery-র সঙ্গে

D. শুধু দুটি antenna-র metal frame

উত্তর যাচাই করো

## শেষ মুহূর্তের Revision Sheet

- 2G GSM → BTS
- 3G UMTS → NodeB
- 4G LTE → eNodeB
- 5G NR → gNodeB
- RAN → Radio Access Network
- UE → User Equipment
- Frequency Reuse → সীমিত spectrum দক্ষভাবে পুনর্ব্যবহার
- Sectorization → coverage-কে directional sector-এ ভাগ
- Handover → active connection-এর radio access পরিবর্তন
- Roaming → home network-এর বাইরে অনুমোদিত network ব্যবহার
- Paging → idle device-কে incoming service-এর জন্য খুঁজে পাওয়া
- Backhaul → RAN site থেকে aggregation/core network-এর দিকে traffic বহন

পরবর্তী লেসন: Lesson 4 — Mobile Network Generations: 1G, 2G, 3G, 4G ও 5G। সেখানে প্রতিটি generation-এর technology, data services, architecture, গুরুত্বপূর্ণ protocol এবং তুলনামূলক MCQ শিখব।

# Lesson 4: Mobile Network Generations — 1G, 2G, 3G, 4G ও 5G

Teletalk Bangladesh Limited — Assistant Manager (Technical) | MCQ Crash Course

এই লেসনটি তোমার পরীক্ষার জন্য গুরুত্বপূর্ণ। এখানে আমরা প্রতিটি generation-এর technology, architecture, data service, network component এবং পার্থক্যগুলো শিখব। শেষে থাকবে ২০টি MCQ।

## Topic 1: Mobile Network Generation কী?

Mobile network generation বলতে cellular communication technology-এর বিভিন্ন প্রজন্মকে বোঝায়। প্রতিটি নতুন generation সাধারণত data capability, spectral efficiency, latency, network architecture এবং service উন্নত করেছে।

[El Diario - DynaTAC 8000X, el primer celular de la historia](https://images.openai.com/static-rsc-4/84W9FgvQOYo4QcHDI52uX2mQiPve4jtiy2RomFkNa5CFdv6stdK94NfUF1hVbu3dgz84a_opQCMlTAyyyheAfcDOQDV2F0CKQV9eqjO8i125k50qLZC0o9XUVSFU-u7Q1D_WNZTK6q7up4C5mYtI3Lmtk7UkI0IMngyLVcDWJW4?purpose=inline)

[Ericsson GH172 - Telefon Komórkowy](https://images.openai.com/static-rsc-4/mtgi63ROO_9V32SwJbopOFZyhQx4AhvTVtlBdclexPJIO53vs455rgOIFLTIYaqIWGgn0QR_p5TmDdc2ZNpQLQj_tDIMM1agvsN6MAgZFcvx2sKi4BdSz7Gr72n-URQ1Pt4d5IigNenNwoWLANhnxedlezlGlsjPhUqCYlmav5s?purpose=inline)

[Classic Handsets: the NEC e606 heralded 3G video calls](https://images.openai.com/static-rsc-4/qfmBUTLAXYgkGixkhlfZfrQ22ptvIIdjEAq_YSMMc6_LVTzZNOuNsog4NNmhpApDR0ZoeHIfGFgK-OZp-NfhJLVdrKg4w2EiHPcqsZLVMMIlVDdANOro4fByz9tHtl2Ep32Ty3hiYl8a7NlXA-wSaa0ysI64dOPTKuBZ83Cd5FY?purpose=inline)

5

দ্রুত মনে রাখার জন্য:

- 1G: Analog voice
- 2G: Digital voice ও SMS
- 3G: Mobile internet ও multimedia
- 4G: High-speed IP broadband
- 5G: Enhanced broadband, low-latency ও massive device connectivity-এর জন্য উন্নত architecture

এগুলো প্রধান বৈশিষ্ট্য; সব service প্রতিটি network-এ একইভাবে পাওয়া যায় না।

## Topic 2: 1G — First Generation

প্রধান সময়কাল: 1980-এর দশক।

1G ছিল প্রথম প্রজন্মের cellular mobile communication, যেখানে মূলত analog radio technology দিয়ে voice call করা হতো।

### গুরুত্বপূর্ণ বৈশিষ্ট্য

- Analog voice communication
- FDMA-ভিত্তিক radio access
- Digital encryption ও modern packet data service-এর সুবিধা ছিল না
- উদাহরণ: AMPS, NMT, TACS

AMPS-এর পূর্ণরূপ: Advanced Mobile Phone System।

Exam facts:

- 1G → Analog
- 1G-এর প্রধান service → Voice
- AMPS → 1G cellular system

## Topic 3: 2G — Second Generation

প্রধান সময়কাল: 1990-এর দশক থেকে ব্যাপক বিস্তার।

2G-তে digital cellular communication চালু হয়। এর ফলে voice quality, spectrum efficiency এবং subscriber services-এ উন্নতি ঘটে।

### প্রধান প্রযুক্তি

- GSM
- IS-95 / cdmaOne
- Digital voice
- SMS
- Authentication ও encryption-এর উন্নত ব্যবস্থা

### GSM Architecture

Mobile Station (MS)

Mobile device ও SIM

BTS → BSC

Radio transmission ও radio resource control

MSC / Core

Call switching ও mobility-related services

এটি একটি simplified GSM architecture। Subscriber database হিসেবে HLR ও authentication-related information ব্যবস্থাপনায় AuC গুরুত্বপূর্ণ।

### 2.5G ও 2.75G

- GPRS: GSM network-এ packet data service।
- EDGE: GSM/packet network-এ উন্নত data rates অর্জনের প্রযুক্তি; প্রায়ই 2.75G বলা হয়।

MCQ facts:

- GSM → 2G
- SMS ব্যাপকভাবে জনপ্রিয় হয় → 2G
- GPRS → Packet data
- EDGE → Enhanced Data rates for GSM Evolution

## Topic 4: 3G — Third Generation

প্রধান সময়কাল: 2000-এর দশক থেকে ব্যাপক বিস্তার।

3G mobile data, mobile internet, multimedia এবং video calling-কে আরও কার্যকর করে।

### প্রধান প্রযুক্তি

- UMTS / WCDMA
- CDMA2000
- HSPA / HSPA+ — 3G network-এর উন্নত data technology

### 3G-এর বৈশিষ্ট্য

- Mobile internet-এর উন্নতি
- Multimedia ও video calling
- Packet data capability
- Voice ও data service-এর উন্নত সমর্থন

UMTS-এর পূর্ণরূপ: Universal Mobile Telecommunications System।

WCDMA-এর পূর্ণরূপ: Wideband Code Division Multiple Access।

Exam facts:

- UMTS/WCDMA → 3G
- HSPA → 3G-এর উন্নত data technology
- 3G → Mobile broadband-এর গুরুত্বপূর্ণ ধাপ

## Topic 5: 4G — Fourth Generation

প্রধান সময়কাল: 2010-এর দশক থেকে ব্যাপক বিস্তার।

4G mobile broadband-কে আরও উন্নত করে। LTE হলো 4G-এর সবচেয়ে পরিচিত প্রযুক্তিগুলোর একটি।

### LTE Architecture

UE — Mobile Device

eNodeB

LTE Radio Access Network

EPC — Evolved Packet Core

MME, SGW, PGW, HSS ইত্যাদি

Internet / IP Services

### LTE/EPC-এর প্রধান component

| Component | প্রধান কাজ                                          |
| --------- | --------------------------------------------------- |
| eNodeB    | LTE radio access                                    |
| MME       | Control-plane mobility ও session-related signalling |
| SGW       | User-plane packet forwarding এবং mobility anchoring |
| PGW       | External packet network-এর সঙ্গে connectivity       |
| HSS       | Subscriber information ও authentication support     |

### 4G-এর গুরুত্বপূর্ণ বৈশিষ্ট্য

- Packet-switched architecture
- OFDMA downlink ও SC-FDMA uplink in conventional LTE
- High-speed mobile broadband
- VoLTE-এর মাধ্যমে LTE network-এ voice service
- IP-based service delivery

MCQ facts:

- LTE → 4G
- eNodeB → LTE base station
- EPC → 4G core architecture
- MME → Control plane
- SGW/PGW → User-plane packet forwarding ও connectivity-এর সঙ্গে সম্পর্কিত

মনে রাখবে, VoLTE হলো LTE-র ওপর voice service দেওয়ার একটি ব্যবস্থা; LTE নিজেই traditional circuit-switched voice network নয়।

## Topic 6: 5G — Fifth Generation

প্রধান সময়কাল: 2019 থেকে বিভিন্ন দেশে commercial rollout শুরু হয়; deployment এখনও উন্নত হচ্ছে।

5G NR-এর পূর্ণরূপ হলো 5G New Radio। এটি enhanced mobile broadband, ultra-reliable low-latency communication-এর লক্ষ্য এবং massive machine-type connectivity-এর মতো use case সমর্থনের জন্য তৈরি।

### 5G-এর তিনটি গুরুত্বপূর্ণ use case

eMBB — Enhanced Mobile Broadband

উচ্চ data rate ও উন্নত broadband service।

URLLC — Ultra-Reliable Low-Latency Communications

কম latency ও উচ্চ নির্ভরযোগ্যতা প্রয়োজন এমন use case-এর জন্য।

mMTC — Massive Machine-Type Communications

বিপুলসংখ্যক connected device-কে সমর্থনের লক্ষ্য।

### 5G Architecture

- gNodeB (gNB): 5G NR base station।
- 5GC: 5G Core।
- AMF: Access and Mobility Management Function।
- SMF: Session Management Function।
- UPF: User Plane Function।
- UDM: Unified Data Management।
- AUSF: Authentication Server Function।

5G Standalone (SA) architecture-এ 5G NR ও 5G Core ব্যবহৃত হয়। 5G Non-Standalone (NSA) deployment-এ LTE/EPC-সহ আগের generation-এর infrastructure-এর ওপর নির্ভরতা থাকতে পারে।

MCQ facts:

- 5G radio technology → NR
- 5G base station → gNodeB
- 5G core → 5GC
- AMF → Access/mobility management
- SMF → Session management
- UPF → User-plane forwarding

## Topic 7: 1G থেকে 5G — তুলনামূলক টেবিল

| বৈশিষ্ট্য               | 1G                       | 2G                | 3G               | 4G                        | 5G                                 |
| ----------------------- | ------------------------ | ----------------- | ---------------- | ------------------------- | ---------------------------------- |
| প্রধান voice technology | Analog                   | Digital           | Digital          | VoLTE/অন্যান্য deployment | VoNR/অন্যান্য deployment           |
| পরিচিত প্রযুক্তি        | AMPS                     | GSM               | UMTS             | LTE                       | 5G NR                              |
| Data capability         | অত্যন্ত সীমিত            | GPRS/EDGE-এ উন্নত | Mobile broadband | High-speed broadband      | Enhanced broadband ও নতুন use case |
| Base station term       | ঐতিহাসিক system-specific | BTS               | NodeB            | eNodeB                    | gNodeB                             |
| Core architecture       | System-specific          | GSM core          | 3G core          | EPC                       | 5GC (SA)                           |

গুরুত্বপূর্ণ সতর্কতা: Generation-এর নাম থেকে নির্দিষ্ট speed বা latency নিশ্চিত করা যায় না। বাস্তব performance spectrum, bandwidth, signal quality, deployment ও network load-এর ওপর নির্ভর করে।

## Topic 8: গুরুত্বপূর্ণ Abbreviations

| Abbreviation | Full form                                  |
| ------------ | ------------------------------------------ |
| GSM          | Global System for Mobile Communications    |
| GPRS         | General Packet Radio Service               |
| EDGE         | Enhanced Data rates for GSM Evolution      |
| UMTS         | Universal Mobile Telecommunications System |
| WCDMA        | Wideband Code Division Multiple Access     |
| HSPA         | High Speed Packet Access                   |
| LTE          | Long-Term Evolution                        |
| EPC          | Evolved Packet Core                        |
| NR           | New Radio                                  |
| 5GC          | 5G Core                                    |
| VoLTE        | Voice over LTE                             |
| VoNR         | Voice over New Radio                       |
| eMBB         | Enhanced Mobile Broadband                  |
| URLLC        | Ultra-Reliable Low-Latency Communications  |
| mMTC         | Massive Machine-Type Communications        |

# Lesson 4: MCQ Model Test

নিচের ২০টি প্রশ্নে প্রতিটি সঠিক উত্তর ১ নম্বর হিসেবে গণনা হবে। এটি অনুশীলনের স্কোর—তোমার আসল পরীক্ষার marking scheme নয়।

## 20-question quiz

0/20 উত্তর

1\. 1G cellular system-এর প্রধান বৈশিষ্ট্য কী?

A. Analog voice

B. Digital packet core

C. 5G NR

D. Network slicing

2\. GSM কোন generation-এর প্রযুক্তি?

A. 1G

B. 2G

C. 3G

D. 5G

3\. GPRS-এর প্রধান ভূমিকা কী?

A. GSM-এ packet data service

B. Analog television

C. 5G radio access

D. Fiber splicing

4\. UMTS/WCDMA কোন generation-এর সঙ্গে সম্পর্কিত?

A. 1G

B. 2G

C. 3G

D. 5G

5\. LTE সাধারণত কোন generation-এর সঙ্গে সম্পর্কিত?

A. 1G

B. 2G

C. 3G

D. 4G

6\. 5G NR-এর NR-এর পূর্ণরূপ কী?

A. Network Relay

B. New Radio

C. Narrow Routing

D. Node Register

7\. LTE base station-এর নাম কী?

A. BTS

B. NodeB

C. eNodeB

D. gNodeB

8\. 5G NR base station-এর নাম কী?

A. BTS

B. gNodeB

C. MSC

D. HLR

9\. LTE-এর core architecture-এর নাম কী?

A. EPC

B. 5GC only

C. AuC only

D. PSTN

10\. 5G Standalone architecture-এ কোন core ব্যবহৃত হয়?

A. GSM core only

B. EPC only

C. 5GC

D. HLR only

11\. LTE-তে MME মূলত কোন plane-এর কাজ করে?

A. Control plane

B. User plane only

C. Optical plane

D. Power plane

12\. 5G Core-এ UPF-এর প্রধান কাজ কী?

A. User-plane forwarding

B. Subscriber identity storage only

C. Radio antenna control only

D. AC rectification

13\. কোনটি 5G use case category?

A. eMBB

B. HTML

C. SMTP

D. AMPS

14\. VoLTE-এর অর্থ কী?

A. Voice over LTE

B. Video over Long Tower Ethernet

C. Virtual Optical LTE

D. Voice on Local Terminal Equipment

15\. GSM network-এ EDGE সাধারণত কী?

A. 2G-এর উন্নত data technology

B. 5G Core function

C. Analog 1G standard

D. Antenna type

16\. Traditional LTE downlink-এ কোন multiple-access scheme ব্যবহৃত হয়?

A. OFDMA

B. Pure TDMA only

C. AM only

D. FM only

17\. 5G SA ও NSA সম্পর্কে কোনটি সঠিক?

A. দুটিই সবসময় 5GC ব্যবহার করে

B. SA-তে 5GC, NSA-তে LTE/EPC-ভিত্তিক নির্ভরতা থাকতে পারে

C. NSA মানে no signal available

D. SA শুধু analog voice

18\. HSPA কোন generation-এর উন্নত data technology?

A. 1G

B. 2G

C. 3G

D. 5G

19\. 2G GSM-এর base station-এর নাম কী?

A. BTS

B. eNodeB

C. gNodeB

D. UPF

20\. 5G-এর mMTC মূলত কী সমর্থনের জন্য?

A. Massive machine-type connectivity

B. Analog voice only

C. শুধু circuit switching

D. শুধু SMS

উত্তর যাচাই করো

## এক মিনিটের Revision

- 1G → Analog voice → AMPS
- 2G → Digital voice/SMS → GSM
- 2.5G → GPRS
- 2.75G → EDGE
- 3G → UMTS/WCDMA → HSPA
- 4G → LTE → eNodeB + EPC
- 5G → NR → gNodeB + 5GC (SA)
- LTE downlink → OFDMA
- MME → LTE control plane
- UPF → 5G user plane
- eMBB → Enhanced broadband
- URLLC → Low-latency, high-reliability use case
- mMTC → Massive device connectivity

পরবর্তী লেসন: Lesson 5 — Circuit Switching vs Packet Switching। সেখানে circuit-switched voice, packet routing, IP networks, LTE কেন packet-based এবং তুলনামূলক MCQ শিখব।

# Lesson 5: Circuit Switching vs Packet Switching

Teletalk Bangladesh Limited Technical Exam • Quick Preparation • বাংলা ক্লাস

এই লেসনে আমরা শিখব কীভাবে টেলিফোন কল ও ইন্টারনেট ডেটা নেটওয়ার্কের মধ্যে চলাচল করে, Circuit Switching ও Packet Switching-এর পার্থক্য, এবং কেন 4G LTE মূলত packet-based network।

## 1. Circuit Switching কী?

Circuit Switching হলো এমন একটি যোগাযোগ পদ্ধতি যেখানে দুই পক্ষের মধ্যে যোগাযোগের পুরো সময়ের জন্য একটি নির্দিষ্ট communication path বা circuit বরাদ্দ করা হয়।

[Circuit Switching in Computer Networks](https://images.openai.com/static-rsc-4/K54WeU_ORLRKEsl_k2dl1QigtNTcU2qKGIviCajxfqVP4Za1ActhX8SYm1U3sdQbBJbcQh8IPOUEb3CduRvXeOKUDUIgEV69EM4No44AQrbmnHmKzBvIhN8PHv_j_vY8gsfcCgTTOhi7Be9d_VDIBBuXhWb8L3BeuScKJom7dYs?purpose=inline)

[tutorialspoint.com](https://www.tutorialspoint.com/data_communication_computer_network/circuit_switching.htm)

উদাহরণ: পুরোনো PSTN landline telephone network-এ একটি কল স্থাপন হলে কল চলাকালীন দুই পক্ষের মধ্যে নির্দিষ্ট circuit ব্যবহৃত হতো।

### Circuit Switching-এর ৩টি ধাপ

1. Connection Setup: কল করার আগে connection বা circuit তৈরি হয়।
2. Data Transfer: নির্ধারিত circuit দিয়ে voice আদান-প্রদান হয়।
3. Connection Release: কল শেষ হলে circuit ছেড়ে দেওয়া হয়।

বৈশিষ্ট্য

- Dedicated path বা circuit থাকে।
- নির্দিষ্ট bandwidth বরাদ্দ থাকতে পারে।
- কল চলাকালে অন্য ব্যবহারকারী একই circuit-এর সেই capacity ব্যবহার করতে পারে না।
- Traditional circuit-switched voice-এর জন্য উপযোগী।
- Connection setup করতে সময় লাগে।

## 2. Packet Switching কী?

Packet Switching-এ ডেটাকে ছোট ছোট অংশে ভাগ করা হয়। প্রতিটি অংশকে packet বলা হয়। Packet-গুলো নেটওয়ার্কের মাধ্যমে গন্তব্যে যায় এবং প্রয়োজন অনুযায়ী সেখানে পুনরায় একত্র করা হয়।

[Packet Switching in Computer Networks](https://images.openai.com/static-rsc-4/80kCscP3KD88q4TsoEJd4DPXUtDzrSWY4KZ0lTYjxZiVQFtOgQdn2NlqjL2wB70J2v_k77KcBRWd0s93AGLaXD1LY6G6scqUfAkR45hbmGq3QvY96lJ7OCThZIN1DvYgQPAIRH4ivxUBJaka9bVHveon9TLsbCaeVuibuatpuE8?purpose=inline)

[tutorialspoint.com](https://www.tutorialspoint.com/data_communication_computer_network/packet_switching.htm)

উদাহরণ: ওয়েবসাইট খোলা, ইমেইল পাঠানো, অনলাইন ভিডিও দেখা এবং IP-based communication।

### Packet Switching কীভাবে কাজ করে?

1. Sender ডেটাকে packet-এ ভাগ করে।
2. প্রতিটি packet-এ প্রয়োজনীয় addressing ও control information থাকে।
3. Router packet-এর destination দেখে forwarding decision নেয়।
4. Packet বিভিন্ন route দিয়ে যেতে পারে—নেটওয়ার্কের পরিস্থিতির ওপর নির্ভর করে।
5. Receiver packet-গুলো থেকে মূল ডেটা পুনর্গঠন করে।

বৈশিষ্ট্য

- Dedicated end-to-end physical circuit প্রয়োজন হয় না।
- Network resources অনেক ব্যবহারকারী ভাগ করে ব্যবহার করতে পারেন।
- Bursty data traffic-এর জন্য কার্যকর।
- Congestion হলে delay বা packet loss হতে পারে।
- Internet মূলত packet-switched network।

## 3. Circuit Switching vs Packet Switching

| বিষয়           | Circuit Switching                                     | Packet Switching                    |
| -------------- | ----------------------------------------------------- | ----------------------------------- |
| Path           | Dedicated circuit                                     | Shared network resources            |
| Data           | Continuous stream over circuit                        | ছোট ছোট packets                     |
| Resource use   | Circuit-এর capacity কল চলাকালীন বরাদ্দ থাকে           | প্রয়োজন অনুযায়ী resources share হয়  |
| Delay          | Setup delay; established call-এ তুলনামূলক predictable | Queueing-এর কারণে delay পরিবর্তনশীল |
| Congestion     | নতুন circuit স্থাপন ব্যর্থ হতে পারে                   | Packet delay বা loss হতে পারে       |
| উদাহরণ         | Traditional PSTN voice                                | Internet, IP data                   |
| প্রধান ব্যবহার | Traditional circuit-switched calls                    | Web, email, IP services             |

## 4. IP Network ও Router

IP (Internet Protocol) হলো network-layer protocol, যা packet-কে source থেকে destination-এ পৌঁছাতে addressing ও forwarding-এর ভিত্তি দেয়।

Router কী করে?

- Packet-এর destination IP address দেখে।
- Routing table অনুযায়ী পরবর্তী hop নির্ধারণ করে।
- Packet-কে উপযুক্ত interface বা next router-এর দিকে পাঠায়।

মনে রাখবে: IP address = network address; Router = packet forwarding device।

## 5. কেন 4G LTE packet-based?

LTE হলো 4G mobile broadband technology। LTE-তে user data এবং voice services IP-based architecture-এর মাধ্যমে বহন করা যায়।

- E-UTRAN: LTE radio access network।
- EPC (Evolved Packet Core): LTE core network।
- VoLTE: LTE network-এর ওপর IP-based voice service।
- IMS: VoLTE-সহ বিভিন্ন IP multimedia service-এর জন্য ব্যবহৃত service architecture।

একটি গুরুত্বপূর্ণ পার্থক্য:

- পুরোনো GSM circuit-switched voice: Voice call-এর জন্য circuit-switched domain ব্যবহার করে।
- LTE/VoLTE: Voice-কে IP packet হিসেবে বহন করে।
- LTE-তে voice service দিতে VoLTE বা প্রয়োজনে legacy network-এ fallback-এর মতো ব্যবস্থা থাকতে পারে।

## 6. পরীক্ষার জন্য মনে রাখার শর্ট নোট

Circuit Switching: Dedicated circuit, setup → communication → release।

Packet Switching: Data divided into packets; network resources shared।

Router: IP packet forward করে।

LTE: E-UTRAN + EPC; VoLTE: LTE-তে IP-based voice।

## 7. MCQ Practice Test — 10 Questions

## Lesson 5 Quiz

0/10 answered

প্রতিটি প্রশ্নে একটি সঠিক উত্তর নির্বাচন করো। তারপর ফলাফল দেখো।

1\. Circuit Switching-এর প্রধান বৈশিষ্ট্য কোনটি?

A. Data packet-এ ভাগ করা

B. Dedicated circuit ব্যবহার

C. প্রতিটি packet অবশ্যই একই router দিয়ে যায়

D. কোনো connection setup লাগে না

2\. Internet প্রধানত কোন switching পদ্ধতি ব্যবহার করে?

A. Circuit Switching

B. Manual Switching

C. Packet Switching

D. Frequency Switching

3\. Packet Switching-এ ডেটার ছোট অংশকে কী বলে?

A. Cell site

B. Packet

C. Sector

D. Circuit

4\. Circuit Switching-এর সঠিক ধাপ কোনটি?

A. Release → Setup → Transfer

B. Transfer → Setup → Release

C. Setup → Transfer → Release

D. Setup → Release → Transfer

5\. IP packet forward করার প্রধান কাজ কোন ডিভাইসের?

A. Router

B. Microphone

C. Antenna only

D. SIM card

6\. Packet Switching-এর একটি সম্ভাব্য সমস্যা কী?

A. Dedicated circuit সব সময় লাগে

B. Queueing delay ও packet loss

C. IP address ব্যবহার করা যায় না

D. ডেটা ভাগ করা যায় না

7\. LTE-এর core network-এর নাম কী?

A. BSC

B. EPC

C. PSTN

D. DSLAM

8\. VoLTE-এর পূর্ণরূপ কী?

A. Voice over Long-Term Evolution

B. Video of LTE Equipment

C. Virtual Operation of Local Telephone Exchange

D. Voice on Local Ethernet

9\. LTE radio access network-কে কী বলা হয়?

A. E-UTRAN

B. EPC

C. IMS

D. PSTN

10\. Circuit Switching-এ connection release কখন হয়?

A. কল শুরু হওয়ার আগে

B. প্রতিটি packet-এর পরে

C. যোগাযোগ শেষ হলে

D. Router চালু হলে

Submit Answers

পরবর্তী ক্লাস: Lesson 6 — Optical Fiber Communication, যেখানে থাকবে fiber optic-এর working principle, core/cladding, total internal reflection, single-mode বনাম multimode fiber, attenuation, splicing এবং MCQ practice।

# Lesson 6: Optical Fiber Communication

Teletalk Bangladesh Limited Technical Exam • দ্রুত প্রস্তুতি • বাংলা ক্লাস

এই লেসনে আমরা শিখব কীভাবে optical fiber দিয়ে আলো ব্যবহার করে ডেটা পাঠানো হয়, fiber-এর গঠন, Single-mode বনাম Multimode fiber, attenuation, splicing এবং গুরুত্বপূর্ণ MCQ।

## 1. Optical Fiber কী?

Optical fiber হলো একটি সরু, নমনীয়, স্বচ্ছ মাধ্যম—সাধারণত কাচ (glass) বা প্লাস্টিক দিয়ে তৈরি—যার মধ্য দিয়ে আলোর সংকেত ব্যবহার করে ডেটা পরিবহন করা হয়।

[Introduction of Optical Fiber Communication System | PPTX](https://images.openai.com/static-rsc-4/yj2aWjrQW5v-btB3cFvqF6iuYeny1Sf-xg9Qng4BDyrVcIo7RsKevMft-VJUYrp1dftHCTN837y8hjGlZjf5PoY42M91fSsBEG9gkomAvCQroV12zFamOXGElhbPqUAqTKu_ydi6ZmPkNS_OFvWSorAPUH8bH25KIX4erZsGg2o?purpose=inline)

[slideshare.net](https://www.slideshare.net/slideshow/introduction-of-optical-fiber-communication-system/87595015)

টেলিকম নেটওয়ার্কে optical fiber ব্যবহৃত হয় কারণ এটি:

- উচ্চ bandwidth প্রদান করতে পারে।
- দীর্ঘ দূরত্বে ডেটা পাঠাতে উপযোগী।
- Electromagnetic interference (EMI)-এর প্রভাব থেকে অনেকটাই মুক্ত।
- Copper cable-এর তুলনায় কম signal attenuation দিতে পারে—উপযুক্ত fiber ও wavelength-এ।
- Mobile tower, exchange, data center এবং international communication link-এ ব্যবহৃত হয়।

## 2. Optical Fiber-এর প্রধান অংশ

[PPT - Optical fiber Transmission Media PowerPoint Presentation, free download - ID:5090478](https://images.openai.com/static-rsc-4/NtxvQnkY_SL5MXMZlMRH7vlGnrMSTOKE68Bu5ZyMnB5kFvX_ULreEIsqoYrHfTzK4I3Zjs1bZhqGPed53DdLHnNzWUnpnS9HjWqMFelfonRd6yz1lJmU1a5bQKLyaTjkf9V4XGd72_ENbSit5Jkt2s52_qbiXo6p8xZO7Q4vN_0?purpose=inline)

1\. Core

Fiber-এর কেন্দ্রীয় অংশ। আলোর সংকেত মূলত এই অংশ দিয়ে চলাচল করে।

[Special Cut-off Wavelength Single-Mode Fiber Optic - 2026 Single-Mode Fiber Optic, Single Mode Optical Fiber price | Made-in-china.com](https://images.openai.com/static-rsc-4/n7pADZelk7RlZiltv5DUpHPfdWCPPGqZq3gQII9_1DXtekeIqEupADjLAGX8of6B78dO2np1rJ4SEZWr5FUOHlXHy-zi4suS94ogJdJE7n5kyxQUfTsd2Pyy8He5vl2ibJya13Cg2twILtXpODUn3jA7unbaSRlUdFiP9gWKfYU?purpose=inline)

2\. Cladding

Core-কে ঘিরে থাকে। এর refractive index core-এর তুলনায় কম হওয়ায় total internal reflection সম্ভব হয়।

[Fiber Optic Cable in Computer Network: 10 Powerful Benefits 2025](https://images.openai.com/static-rsc-4/6uueTLpe1iV7A7AUJYVuqD0WMVpxahS44s0TWAtjy4s50SHdh4cnjMROYBrvH5xT3A5YUx5z1dopBjyDe6i6K4wH8nUuo2Xxtuu2mybGpXVYbLXDrOVuR8rB6j4n-y-D7HxeHn5_8e5quPM24uB8g9N7RCWNApKS51Z3xUOXFVw?purpose=inline)

3\. Coating / Protective layers

Fiber-কে আর্দ্রতা, ঘর্ষণ ও অন্যান্য বাহ্যিক ক্ষতি থেকে রক্ষা করতে সাহায্য করে।

পরীক্ষার জন্য মনে রাখবে: Core → আলো বহন করে; Cladding → আলোকে core-এর মধ্যে guide করতে সাহায্য করে; Coating → সুরক্ষা দেয়।

## 3. Total Internal Reflection (TIR)

Optical fiber কীভাবে আলোকে গন্তব্যে পৌঁছে দেয়, সেটি বোঝার সবচেয়ে গুরুত্বপূর্ণ ধারণা হলো Total Internal Reflection।

[Download 58774 P023b - Total Internal Reflection In Fibre PNG Image with No Background - PNGkey.com](https://images.openai.com/static-rsc-4/_JIpZAXwRHmvRK-FEFZb3yK5pkiQWzZnp7wPgXRvwMXpMVOKyqtCHbbrrU153tm0bW1PUUnBLob7sPoN-P8ifbPeC95SEQhx4oaT5VNAceZtMt4nlXYHRt-pGdzTCxtgL8v47n84MRM9X55CpIc7XVS2750oyMobvD6GE1ME63I?purpose=inline)

[pngkey.com](https://www.pngkey.com/maxpic/u2q8u2o0y3o0w7t4/)

TIR ঘটার জন্য দুটি শর্ত মনে রাখবে:

1. আলোকে বেশি refractive index-এর মাধ্যম থেকে কম refractive index-এর মাধ্যমে যাওয়ার সীমানার দিকে যেতে হবে।
2. আপতন কোণ (angle of incidence) critical angle-এর চেয়ে বেশি হতে হবে।

Optical fiber-এ core-এর refractive index সাধারণত cladding-এর চেয়ে বেশি। উপযুক্ত কোণে আলো core–cladding boundary-তে বারবার প্রতিফলিত হয়ে core-এর মধ্যে guided থাকে।

Exam tip: Optical fiber-এর আলো পরিবহনের সঙ্গে Total Internal Reflection সরাসরি সম্পর্কিত।

## 4. Single-mode vs Multimode Fiber

[Single Mode vs Multimode Fiber: What’s the Difference & Which Should You Use?](https://images.openai.com/static-rsc-4/T4Z6UaRpRoCwGreWOymyGUqnY09baBH3uR2Sn_sfY9f0TFq8hz2us5RT1Q7HIYWsVsyq01sIkyq616XayzVjLUcAXWPmzYx1k1TYmGrX508LqLEgRg3KmvO3_6Oby9x41BafDy-kBgDb4KVcLrWNj2yEKre41FyxDD7V_NmVSX4?purpose=inline)

[Introduction and application of Single Mode and Multimode Fiber Cable  – Splicer Market](https://images.openai.com/static-rsc-4/90oyF_e4FJn5IDGhWrcv59MegQN06x1nlNDETpSwTqc5A2jXQV4liNE2j27CeOoT7lln_cN_unIx7MIrDlOR5C4ti_NUU4LN8cKp94r3OQRB6jWBH2EamYaqd0GcAtB7QwWKQLULTeNPG17W7j4biVOGcFfPj_myNnS6s_DfNvc?purpose=inline)

[Fiber Optics Part 3: Fiber Dispersion Will Change The Way You See Your Links - Cisco Blogs](https://images.openai.com/static-rsc-4/pELqLQ52nlGwXhCQMf0ioRCOzplQkncfUU2etKGO_s0Cu-P5VmwUw6KF6ifSicaXSPhXyO0aiGX8BOvRUFsjw6thiY9uKghbCDZAEDyyMr7N8qnabqwSmdE83BqLm7lJ32hNc-c36e6VjAfZq-zr87Qs1oqVcXSM83e06en2X8Y?purpose=inline)

7

| বৈশিষ্ট্য              | Single-mode Fiber (SMF)               | Multimode Fiber (MMF)                            |
| ---------------------- | ------------------------------------- | ------------------------------------------------ |
| Light propagation mode | একটি প্রধান mode                      | একাধিক mode                                      |
| Core size              | ছোট, সাধারণত প্রায় 8–10 µm            | তুলনামূলক বড়, সাধারণত 50 বা 62.5 µm              |
| Dispersion             | Modal dispersion নেই                  | Modal dispersion হতে পারে                        |
| ব্যবহার                | Long-distance telecom, FTTH, backbone | Short-distance links, অনেক LAN/data-center সংযোগ |
| Light source           | সাধারণত laser                         | সাধারণত VCSEL বা LED—সিস্টেমভেদে                 |

মনে রাখবে: Single-mode fiber দীর্ঘ দূরত্বের telecom link-এর জন্য খুবই গুরুত্বপূর্ণ। তবে বাস্তবে কোন fiber ব্যবহার হবে, তা distance, bandwidth, optics ও খরচের ওপর নির্ভর করে।

## 5. Attenuation কী?

Attenuation হলো fiber-এর মধ্য দিয়ে চলার সময় signal power কমে যাওয়া।

সাধারণত attenuation প্রকাশ করা হয় dB/km এককে।

উদাহরণ: একটি fiber-এর attenuation \\(0.2\ \text{dB/km}\\), এবং দৈর্ঘ্য 10 km হলে fiber-এর কারণে মোট attenuation:

\\[ 0.2 \times 10 = 2\ \text{dB} \\]

এটি শুধু fiber-এর attenuation; connector, splice ও অন্যান্য loss আলাদাভাবে যোগ হতে পারে।

Attenuation-এর প্রধান কারণ:

- Absorption: উপাদান আলো শোষণ করে।
- Scattering: আলোর একটি অংশ বিভিন্ন দিকে ছড়িয়ে পড়ে।
- Bending loss: Fiber বেশি বাঁকলে আলো বেরিয়ে যেতে পারে।

## 6. Fiber Splicing ও Connector

[Fusion splicer fiber optic.](https://images.openai.com/static-rsc-4/utVbCZ4arYrIE5CpRG4LsbbfdPvXaYhug9Hbd1W83f-ZUMuxjpLKXW4Tkz2vq-UVy4dPPsUNjYYyAviWHt-HBGrPHV8cGWE61kHednElHVijA66eSsXxYsSgVyo45U9IIfFRkbmfbDXZCHPoMMclT5VpTyD7cx3GFz62gvOTlkqqsRAr4LwjfWN_CzomTTfC?purpose=inline)

[【楽天市場】光ファイバーケーブル LCコネクタSCコネクタ シングルモード コア径9.2マイクロメートル 2芯 光回線 光電話 1m：サンワダイレクト楽天市場店](https://images.openai.com/static-rsc-4/zigmt3YsSsdD_6jUD7h98_9IAumyNtr2wcocDLh67Qexy6clObQNJwp5dnrsYfYriYvialoupjUVq3c1s-__6_fyRt2SkU_ReU7AZ8RnrAaqfIIb-Bgo44lJxBXt3chJgImuMmWPEpKkHw3r2Jkd8u_uADMRrDKIJjbuY0R7eSg?purpose=inline)

[What is Fiber Fusion Splicer - Fibconet Communicate](https://images.openai.com/static-rsc-4/_XvfewNc5i-9xA21cIJCi-7KKuxZi7fziwO00roBvMC1fTzoXbFHpAfvghXZCyk3ZZL03wtUxq0JtCi4IotxWXJn2mtLvqOiPsV9Fee1yVor-BAJ9NpQbyMkUfqeJ_uk1LPJPooqO3flpt72DPP78S-HAyMTv78vyg2jYX5bBSI?purpose=inline)

7

Fiber Splicing: দুটি optical fiber স্থায়ীভাবে যুক্ত করার পদ্ধতি।

- Fusion splicing: দুই fiber-এর প্রান্ত গলিয়ে যুক্ত করা হয়। সাধারণত কম splice loss পাওয়ার জন্য ব্যবহৃত হয়।
- Mechanical splicing: বিশেষ alignment device দিয়ে fiber-এর প্রান্ত যুক্ত করা হয়।

Fiber Connector: Fiber-কে transceiver, patch panel বা অন্য যন্ত্রের সঙ্গে সংযোগ করতে ব্যবহৃত হয়।

পরিচিত connector:

- SC: Subscriber Connector / Standard Connector নামে পরিচিত।
- LC: Lucent Connector নামে পরিচিত।
- ST: Straight Tip connector।

Splice বা connector-এ ময়লা, ভুল alignment কিংবা ক্ষতিগ্রস্ত প্রান্ত থাকলে signal loss বাড়তে পারে।

## 7. Optical Fiber-এর গুরুত্বপূর্ণ telecom ব্যবহার

- FTTH: Fiber To The Home — বাসায় broadband সংযোগ।
- Backhaul: Mobile tower বা base station-এর traffic core network-এ পৌঁছে দেয়।
- Backbone network: বড় নেটওয়ার্কের বিভিন্ন শহর, exchange বা region-কে সংযুক্ত করে।
- Submarine fiber cable: সমুদ্রের নিচ দিয়ে আন্তর্জাতিক ডেটা পরিবহন করে।
- GPON: Passive optical network technology, যা FTTH-তে বহুল ব্যবহৃত।

## 8. MCQ Practice Test — 15 Questions

## Lesson 6 Quiz

0/15 answered

উত্তর নির্বাচন করে Submit Answers চাপো। ফলাফল ও ব্যাখ্যা দেখা যাবে।

1\. Optical fiber-এ ডেটা পরিবহনের জন্য কী ব্যবহার করা হয়?

A. শুধু বিদ্যুৎ প্রবাহ

B. আলোর সংকেত

C. শব্দ তরঙ্গ

D. চৌম্বক ক্ষেত্র

2\. Fiber-এর কেন্দ্রীয় অংশ কোনটি?

A. Cladding

B. Coating

C. Core

D. Jacket

3\. Core-এর চারপাশে কোন অংশ থাকে?

A. Cladding

B. Router

C. Transceiver

D. Splice tray

4\. Optical fiber-এ আলো guide হওয়ার সঙ্গে কোন নীতি সম্পর্কিত?

A. Electromagnetic induction

B. Total Internal Reflection

C. Photoelectric effect only

D. Thermal expansion

5\. Core-এর refractive index সাধারণত কেমন?

A. Cladding-এর চেয়ে বেশি

B. Cladding-এর চেয়ে কম

C. সবসময় শূন্য

D. সবসময় সমান

6\. Long-distance telecom-এ সাধারণত কোন fiber ব্যবহৃত হয়?

A. Single-mode fiber

B. Multimode fiber only

C. Copper pair only

D. Plastic wire only

7\. Multimode fiber-এর একটি বৈশিষ্ট্য কী?

A. শুধু একটি mode থাকে

B. একাধিক propagation mode থাকতে পারে

C. আলো ব্যবহার করা যায় না

D. কোনো core থাকে না

8\. Attenuation সাধারণত কোন এককে প্রকাশ করা হয়?

A. Hz/km

B. dB/km

C. Volt/second

D. Byte/s

9\. 0.2 dB/km attenuation-এর fiber 10 km হলে fiber loss কত?

A. 0.2 dB

B. 2 dB

C. 20 dB

D. 200 dB

10\. Fiber-এ আলো শোষিত হওয়ার কারণে কোন loss হয়?

A. Absorption loss

B. Routing loss

C. Paging loss

D. Handover loss

11\. Fiber অতিরিক্ত বাঁকালে কোন সমস্যা হতে পারে?

A. Bending loss

B. IP conflict

C. Frequency reuse

D. Circuit setup

12\. Fusion splicing কী করে?

A. Packet route করে

B. Fiber-এর প্রান্ত গলিয়ে যুক্ত করে

C. IP address দেয়

D. Signal encrypt করে

13\. FTTH-এর পূর্ণরূপ কী?

A. Fiber To The Home

B. Fast Transmission Through Hub

C. Frequency Transfer To Host

D. Fiber Terminal Telecom Highway

14\. Mobile network-এ fiber backhaul-এর কাজ কী?

A. SIM তৈরি করা

B. Base station-এর traffic network-এর অন্য অংশে বহন করা

C. ফোনের battery চার্জ করা

D. Antenna ঘোরানো

15\. GPON সাধারণত কোন ক্ষেত্রে ব্যবহৃত হয়?

A. FTTH optical access network

B. শুধু analog radio

C. GPS satellite navigation

D. Copper-only PSTN

Submit Answers

পরবর্তী ক্লাস — Lesson 7: Networking Fundamentals। এতে থাকবে OSI Model, TCP/IP Model, IP address, IPv4/IPv6, subnet mask, DNS, DHCP, TCP বনাম UDP, এবং পরীক্ষার MCQ।

# Lesson 7: Networking Fundamentals

Teletalk Bangladesh Limited Technical Exam • বাংলা Crash Course

এই লেসনে Computer Networking-এর গুরুত্বপূর্ণ বিষয়গুলো শিখব: OSI Model, TCP/IP Model, IP Address, IPv4 বনাম IPv6, DNS, DHCP, TCP বনাম UDP এবং Subnet Mask। টেলিকম ও IT-সম্পর্কিত টেকনিক্যাল পরীক্ষার জন্য এগুলো ভালোভাবে জানা দরকার।

## 1. Computer Network কী?

Computer Network হলো একাধিক কম্পিউটার, সার্ভার বা নেটওয়ার্ক ডিভাইসের মধ্যে সংযোগ, যার মাধ্যমে ডেটা ও রিসোর্স আদান-প্রদান করা যায়।

[Techills | IT Solutions & Services](https://images.openai.com/static-rsc-4/yV8AEmUcLr5_niJaYBGnTY0xFrpcZsbK736Nr-J_P3jMzonzOQp5LEi-hvPiKdEYVOeS5VBrEpwAWtnWiWCnCuv4M15B9m8qEsQTKN30wB2auFhHe5agDOE3hqs92vh0GPqUdtaQuur3B5s34s7Pu4VEp6LCwnSPT21jZ0m-4n4?purpose=inline)

[techills.com](https://www.techills.com/)

নেটওয়ার্কের পরিচিত ধরন:

- LAN (Local Area Network): ছোট এলাকার নেটওয়ার্ক, যেমন অফিস বা বাসা।
- MAN (Metropolitan Area Network): শহর বা মহানগরজুড়ে নেটওয়ার্ক।
- WAN (Wide Area Network): বৃহৎ ভৌগোলিক এলাকার নেটওয়ার্ক; Internet এর বড় উদাহরণ।
- WLAN: Wireless Local Area Network, যেমন Wi-Fi নেটওয়ার্ক।

## 2. OSI Model — 7 Layers

OSI Model নেটওয়ার্ক যোগাযোগকে সাতটি স্তরে ভাগ করে ব্যাখ্যা করে।

## 7

Application Layer

ব্যবহারকারীর নেটওয়ার্ক সেবা

HTTP, DNS, SMTP

## 6

Presentation Layer

Data format, encryption, compression

Encoding, encryption

## 5

Session Layer

Communication session পরিচালনা

Session control

## 4

Transport Layer

End-to-end delivery, port, reliability

TCP, UDP

## 3

Network Layer

Logical addressing ও routing

IP, routers

## 2

Data Link Layer

Frames, MAC address, local delivery

Ethernet, switches

## 1

Physical Layer

Bits ও physical signal

Cable, fiber, radio

পরীক্ষায় গুরুত্বপূর্ণ:

- Layer 1 — Physical
- Layer 2 — Data Link
- Layer 3 — Network
- Layer 4 — Transport
- Layer 7 — Application

OSI Layer মনে রাখার mnemonic, নিচ থেকে ওপরের দিকে: Please Do Not Throw Sausage Pizza Away।

আরেকটি গুরুত্বপূর্ণ বিষয়: OSI হলো একটি conceptual reference model; বাস্তব Internet protocol-গুলোকে সবসময় একেকটি OSI layer-এর সঙ্গে নিখুঁতভাবে মেলানো যায় না।

## 3. TCP/IP Model

Internet-এ যোগাযোগ বোঝার জন্য TCP/IP Model খুব গুরুত্বপূর্ণ।

| TCP/IP Layer   | প্রধান কাজ                            | উদাহরণ          |
| -------------- | ------------------------------------- | --------------- |
| Application    | Network application services          | HTTP, DNS, SMTP |
| Transport      | Process-to-process delivery           | TCP, UDP        |
| Internet       | IP addressing ও routing               | IPv4, IPv6      |
| Network Access | Local network ও physical transmission | Ethernet, Wi-Fi |

মনে রাখবে: OSI Model-এ ৭টি layer, প্রচলিত TCP/IP Model-এ ৪টি layer।

## 4. IP Address কী?

IP Address হলো নেটওয়ার্কে একটি interface-কে শনাক্ত ও packet-কে সঠিক গন্তব্যে পাঠানোর জন্য ব্যবহৃত logical address।

[IPv4 Address Classes - Complete Guide to Class A, B, C, D, E](https://images.openai.com/static-rsc-4/nUryV328rMk517JRuW60WMiaBP5FlM3DpYru7nN3FAiJHmKmPxMBDoBar0FzcSIvxbuBs_TkNoVIoCVxocyCw41h_cntzR6lR-0wnxSGRJ4KUDtrSvv1ntjeaUqLBeuw81pJFs7SX0UZFH78vorix2cI1WB4yfOLvKqavR4zbCY?purpose=inline)

IPv4

- 32-bit address
- চারটি octet
- Dotted decimal format
- উদাহরণ: `192.168.1.10`

[A Complete Guide to Static IPs: Costs, IPv4, IPv6, and More](https://images.openai.com/static-rsc-4/9azWFrfhB_wCR2aFqo_2LzEp51wEux9G6MPvJImTX6NjUFFJaMiHrvk_R1WRBPyu_blVpk-1CtvKO9fDSLKCxHtDY_CvAGgLoCFqbnOXAx8j76G89DzL3k_v2FKwWOIslBkryCHtYfJu_GywEenzsiLn6W5ES16KBdq7km0Egvs?purpose=inline)

IPv6

- 128-bit address
- Hexadecimal notation
- IPv4-এর তুলনায় অনেক বড় address space
- উদাহরণ: `2001:db8::1`

### Public IP বনাম Private IP

- Public IP: Internet-এ globally routable address।
- Private IP: সাধারণত internal network-এ ব্যবহৃত হয়; সরাসরি public Internet-এ route করা হয় না।

IPv4-এর private address range:

| Range            | উদাহরণ         |
| ---------------- | -------------- |
| `10.0.0.0/8`     | `10.1.2.3`     |
| `172.16.0.0/12`  | `172.16.5.4`   |
| `192.168.0.0/16` | `192.168.1.10` |

## 5. Subnet Mask ও CIDR

Subnet Mask একটি IPv4 address-এর network অংশ এবং host অংশ আলাদা করতে সাহায্য করে।

উদাহরণ:

- IP: `192.168.1.10`
- Subnet mask: `255.255.255.0`
- CIDR notation: `/24`

এখানে `/24` মানে IPv4-এর প্রথম 24 bit network prefix-এর অংশ।

সহজ নিয়ম: `192.168.1.10/24` হলে network address `192.168.1.0`।

আরেকটি পরীক্ষার তথ্য: একটি সাধারণ IPv4 `/24` subnet-এ মোট \\(2^8=256\\)টি address থাকে। প্রচলিত subnet-এ network ও broadcast address বাদ দিলে 254টি usable host address থাকে।

## 6. DNS, DHCP ও NAT

[The Path of a Request: A Tour of Modern Web Architecture](https://images.openai.com/static-rsc-4/rKH-tYsC0NCS2vnmjPoDMPNCkv1pgccAHj0F4lZqQfpJmdiPVH827Q1YvFT7RrB2TAec7Y_9tjBfmZatm6aOMKaJL8eIbtPMvYYwMAGc0wKYOsQaTrON9dwwny7wtTVnQRhEoNndW8D8nrRIN2lbg86MsAp1wT7qTe4_v9NIu6Y?purpose=inline)

DNS — Domain Name System

Domain name-কে IP address-এর সঙ্গে resolve করতে সাহায্য করে। যেমন `example.com`-এর address খুঁজে বের করা।

[DHCP | CloudNative.love 💕](https://images.openai.com/static-rsc-4/JS0uhcXT2yRVz2mVNzU51eQY3iMgxHJaK9-x5oU0Dlm5UUChFEaTYH33_TjxRrnRCej5IyWtmD3wgSiucDpfcqppKNHNWhKWsSS2r1R--w7KS3DHoeiJe0kojH8IAlndRbZeWW4wq0gqyb9oevDOGUd9sNBjXXDTcpjsdND7ZPY?purpose=inline)

DHCP — Dynamic Host Configuration Protocol

Network device-কে স্বয়ংক্রিয়ভাবে IP address, subnet mask, gateway এবং DNS configuration দিতে পারে।

DORA: Discover → Offer → Request → Acknowledge।

[Network Address Translation(NAT). Assigning IPs to your local network | by TechWithAdil | Medium](https://images.openai.com/static-rsc-4/Rw1PPzaWLLx-4ws0jbRwA72yKIIDWtIYf7kTslg74qeZEhDD-mscwUywCw2zV_Ng4QUGC1rvYkl4QEETtV6CRICPG55kRV6B7RlsZ2mRB4DN2J7QHbwtD4oQAeNw4mBB2J3EpaQmUfSF6ldWwZ-EH0yWdydadi9heMqGTluMf04?purpose=inline)

NAT — Network Address Translation

Private ও public network-এর মধ্যে address translation করতে পারে। বাসার অনেক device একটি public IPv4 address share করতে পারে, সাধারণত PAT ব্যবহার করে।

## 7. TCP বনাম UDP

| বিষয়       | TCP                               | UDP                                     |
| ---------- | --------------------------------- | --------------------------------------- |
| Connection | Connection-oriented               | Connectionless                          |
| Delivery   | Reliable delivery-এর ব্যবস্থা আছে | Delivery guarantee নেই                  |
| Ordering   | Ordered byte stream               | Packet/message ordering guarantee নেই   |
| Overhead   | তুলনামূলক বেশি                    | তুলনামূলক কম                            |
| উদাহরণ     | HTTP/1.1, HTTP/2 over TCP, SSH    | DNS সাধারণত UDP, real-time media-তে UDP |

পরীক্ষার ট্রিক: TCP-তে reliability ও ordered delivery-এর ব্যবস্থা আছে; UDP-তে কম overhead, কিন্তু delivery বা ordering নিশ্চিত নয়।

## 8. গুরুত্বপূর্ণ Port Numbers

| Service     | Port | Protocol                       |
| ----------- | ---- | ------------------------------ |
| HTTP        | 80   | TCP                            |
| HTTPS       | 443  | TCP; HTTP/3 uses QUIC over UDP |
| FTP control | 21   | TCP                            |
| SSH         | 22   | TCP                            |
| DNS         | 53   | UDP ও TCP                      |
| DHCP server | 67   | UDP                            |
| DHCP client | 68   | UDP                            |
| SMTP        | 25   | TCP                            |
| POP3        | 110  | TCP                            |
| IMAP        | 143  | TCP                            |

এগুলো MCQ-তে সরাসরি আসতে পারে।

## 9. MCQ Practice Test — 15 Questions

## Networking Quiz

0/15 answered

প্রতিটি প্রশ্নে একটি উত্তর নির্বাচন করো। শেষে Submit Answers চাপো।

1\. OSI Model-এ কয়টি layer আছে?

A. 4

B. 5

C. 7

D. 8

2\. OSI Model-এর Layer 3 কোনটি?

A. Physical

B. Network

C. Transport

D. Session

3\. TCP কোন layer-এ কাজ করে?

A. Physical

B. Data Link

C. Transport

D. Application

4\. IPv4 address কত bit?

A. 16

B. 32

C. 64

D. 128

5\. IPv6 address কত bit?

A. 32

B. 48

C. 64

D. 128

6\. নিচের কোনটি private IPv4 address?

A. 8.8.8.8

B. 172.20.1.5

C. 1.1.1.1

D. 208.67.222.222

7\. DNS-এর প্রধান কাজ কী?

A. Domain name resolve করা

B. IP packet encrypt করা

C. IP address বরাদ্দ করা

D. Fiber splice করা

8\. DHCP-এর DORA-তে প্রথম ধাপ কোনটি?

A. Request

B. Acknowledge

C. Discover

D. Offer

9\. Subnet mask 255.255.255.0-এর CIDR notation কী?

A. /8

B. /16

C. /24

D. /32

10\. একটি সাধারণ IPv4 /24 subnet-এ usable host address কত?

A. 24

B. 128

C. 254

D. 256

11\. কোন protocol reliable, ordered byte-stream delivery দেয়?

A. UDP

B. TCP

C. ARP

D. ICMP

12\. UDP-এর একটি বৈশিষ্ট্য কোনটি?

A. সব packet delivery নিশ্চিত

B. Connection setup বাধ্যতামূলক

C. Connectionless ও কম overhead

D. শুধু file transfer-এ ব্যবহার হয়

13\. HTTPS-এর standard port কোনটি?

A. 21

B. 25

C. 80

D. 443

14\. NAT-এর কাজ কী?

A. Address translation

B. Domain name registration

C. Fiber attenuation মাপা

D. Wireless frequency তৈরি করা

15\. সঠিক TCP/IP Model-এ প্রচলিত layer সংখ্যা কত?

A. 3

B. 4

C. 5

D. 7

Submit Answers

পরবর্তী ক্লাস: Lesson 8 — Mobile Network Architecture & Telecom Equipment: BTS, BSC, MSC, HLR, VLR, HSS, MME, SGW, PGW, eNodeB এবং 5G gNodeB—কোন যন্ত্র কী কাজ করে, সহজ diagram ও MCQ-সহ।

# Lesson 8: Mobile Network Architecture & Telecom Equipment

Teletalk Bangladesh Limited Technical Exam • বাংলা Crash Course

এই লেসনে আমরা শিখব মোবাইল নেটওয়ার্কের প্রধান যন্ত্রপাতি ও তাদের কাজ: BTS, BSC, MSC, HLR, VLR, HSS, MME, SGW, PGW, eNodeB এবং gNodeB। পরীক্ষায় এগুলোর পূর্ণরূপ, কাজ এবং 2G/3G/4G/5G-তে ব্যবহার গুরুত্বপূর্ণ।

## 1. Mobile Network Architecture কীভাবে কাজ করে?

একটি মোবাইল ফোন থেকে কল বা ইন্টারনেট ব্যবহার করলে সাধারণত কয়েকটি নেটওয়ার্ক অংশ কাজ করে:

Mobile Phone (UE)

ব্যবহারকারীর ডিভাইস

Radio Access Network (RAN)

BTS / NodeB / eNodeB / gNodeB

ফোনের সঙ্গে radio connection

Core Network

Authentication, mobility, call/data routing

Service / Destination

Internet, অন্য ফোন, বা অন্য নেটওয়ার্ক

মনে রাখবে:

- RAN: মোবাইল ফোনের সঙ্গে radio access-এর ব্যবস্থা করে।
- Core Network: subscriber management, mobility, call control এবং data connectivity-এর মতো কাজ করে।
- Backhaul: RAN site-কে core network বা aggregation network-এর সঙ্গে যুক্ত করে।

## 2. 2G GSM Network Equipment

[PPT - GSM Network Overview PowerPoint Presentation, free download - ID:3419029](https://images.openai.com/static-rsc-4/M2kKqL1aUl_R2q6XiAoNNlYtrBv9KwCyW85pI3vy3PCPN332AmFrIRbJhgFT-qDyMNnTAA32Ltwui26-3-eAoMjdHxoQDTfkTcTQMMQNkezG1BnYOaYzjsj_jopBIxap_3Bawg3F-TE_QXf8VA9nZRSJ324bHd0qWOSF1nkeMSk?purpose=inline)

[slideserve.com](https://www.slideserve.com/nicki/gsm-network-overview)

### BTS — Base Transceiver Station

- মোবাইল ফোনের সঙ্গে radio signal পাঠায় ও গ্রহণ করে।
- Cell বা radio coverage প্রদান করে।
- GSM/2G network-এর পরিচিত radio equipment।

### BSC — Base Station Controller

- একাধিক BTS নিয়ন্ত্রণ করে।
- Radio resource management এবং handover-সংক্রান্ত কিছু কাজ পরিচালনা করে।
- BTS ও core network-এর মধ্যে সংযোগে ভূমিকা রাখে।

### MSC — Mobile Switching Centre

- Circuit-switched voice call control ও switching করে।
- অন্য mobile network বা PSTN-এর সঙ্গে call routing-এ ভূমিকা রাখে।
- Mobility ও call-related signalling-এর কাজও করতে পারে।

### HLR — Home Location Register

- Subscriber-এর স্থায়ী বা home subscriber record সংরক্ষণ করে।
- Subscriber profile এবং সংশ্লিষ্ট service information রাখে।

### VLR — Visitor Location Register

- বর্তমানে কোনো MSC area-তে থাকা subscriber-দের প্রয়োজনীয় temporary information রাখে।
- Subscriber-এর location ও service handling-এ সাহায্য করে।

পরীক্ষার ট্রিক: BTS = radio; BSC = BTS controller; MSC = switching/call control; HLR = home subscriber data; VLR = serving area-র temporary data।

## 3. 3G Network: NodeB ও RNC

[PPT - UMTS ... … 3G Technology and Concepts PowerPoint Presentation, free download - ID:3380045](https://images.openai.com/static-rsc-4/pd0ZMYJHfthlzangL_C-GWliaPVoiK3xK0iPxgapgGNa0nKklGeLtqlmYA-x5unS-rxJo1quGM1g54_1Uk2K2zk51LGabMJwywo2dsusrtJpF_nj24qNdb02Rd4h8VNU94qKFHNZZjNa5hKRuzVu-v2rOo3a0jFgvRjQ2xmpvJk?purpose=inline)

NodeB — 3G Radio Base Station

মোবাইল ডিভাইসের সঙ্গে radio communication করে।

RNC — Radio Network Controller

একাধিক NodeB নিয়ন্ত্রণ করে এবং radio resource ও mobility management-এ ভূমিকা রাখে।

2G ও 3G-তে মনে রাখার সহজ তুলনা:

| 2G GSM | 3G UMTS |
| ------ | ------- |
| BTS    | NodeB   |
| BSC    | RNC     |

## 4. 4G LTE Network Equipment

4G LTE-তে radio access network ও core network-এর architecture আগের প্রজন্মের তুলনায় ভিন্ন।

[LTE EPC Core Network Components and Functionality | Shah Yar Hussaini posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/QxSMYCY54XU_dMqfUmJ3H5l6h9FwDI8KQTNdvrh_dOrLOdWvx0MTIxihMuhpRyRAqM3btEP1AppmSkdI70qtZp1Qh_9onFjUgpS4PvmqSgohiVH6Ft5GFZrZfNbSTqqQGnmZ8zHgQ9EPmbb_SaF9c69qVLP572YOyUrPfFcHPkY?purpose=inline)

[linkedin.com](https://www.linkedin.com/posts/shahyars_lte-epc-evolved-packet-core-is-the-activity-7424482044010852353-Rzdp)

### eNodeB — Evolved Node B

- LTE-এর radio base station।
- UE-এর সঙ্গে radio communication করে।
- Radio resource management ও scheduling করে।
- LTE-তে radio access-এর অনেক control function eNodeB-তেই থাকে; 2G/3G-এর মতো আলাদা BSC/RNC নেই।

### MME — Mobility Management Entity

- LTE control-plane node।
- UE registration/attach, mobility management এবং authentication-related signalling-এ ভূমিকা রাখে।
- User data সাধারণত MME দিয়ে বহন করা হয় না।

### SGW — Serving Gateway

- LTE user-plane packet traffic forward করে।
- eNodeB এবং core network-এর মধ্যে user-data path-এ ভূমিকা রাখে।
- Mobility-এর সময় user-plane anchoring-এর কাজ করতে পারে।

### PGW — Packet Data Network Gateway

- LTE network-কে external packet data network, যেমন Internet-এর সঙ্গে যুক্ত করে।
- IP connectivity ও policy/charging-সম্পর্কিত কিছু function পরিচালনা করে।

### HSS — Home Subscriber Server

- Subscriber information ও authentication-related data সংরক্ষণ করে।
- LTE-তে subscriber management-এর গুরুত্বপূর্ণ database/function।

গুরুত্বপূর্ণ পার্থক্য:

- MME = Control plane
- SGW ও PGW = User plane-এর গুরুত্বপূর্ণ gateway
- HSS = Subscriber information

## 5. 5G Network: gNodeB ও 5G Core

[Standalone 5G Networks](https://images.openai.com/static-rsc-4/uGvx71FQlzmsdRwgGTJQdab3e68LPFrBrxVgrJpAOYuFsF1MBDdwH90AjrSbAIv4JNgBoyx71FUWkFcScKqp7B6Orj7KFW8Ap_WU-Tj3xE38KBg-U_NEO7Hq6vmSaB060exc4Mr4hbmuvSeYPm0z3Q7xe-BJ6BPSdyYs_-nL6mM?purpose=inline)

[mpirical.com](https://www.mpirical.com/knowledge-base/standalone-5g-networks)

### gNodeB — Next Generation Node B

- 5G NR-এর radio base station।
- UE-এর সঙ্গে 5G radio connection স্থাপন করে।
- Radio resource management ও scheduling-এ ভূমিকা রাখে।

### 5G Core-এর গুরুত্বপূর্ণ function

| Function | পূর্ণরূপ / কাজ                                                      |
| -------- | ------------------------------------------------------------------- |
| AMF      | Access and Mobility Management Function — access ও mobility control |
| SMF      | Session Management Function — PDU session পরিচালনা                  |
| UPF      | User Plane Function — user-data packet forwarding                   |
| UDM      | Unified Data Management — subscriber data management                |
| AUSF     | Authentication Server Function — authentication                     |
| PCF      | Policy Control Function — policy decisions                          |

মনে রাখবে: 5G Core-এর architecture service-based। 4G EPC-এর MME, SGW, PGW-কে 5G Core-এর function-এর সঙ্গে একে একে একই জিনিস ভাবা ঠিক নয়।

## 6. 2G, 3G, 4G ও 5G — এক নজরে

| Generation | Radio equipment | Controller / Core-এর পরিচিত অংশ |
| ---------- | --------------- | ------------------------------- |
| 2G GSM     | BTS             | BSC, MSC, HLR, VLR              |
| 3G UMTS    | NodeB           | RNC, MSC, SGSN/GGSN             |
| 4G LTE     | eNodeB          | MME, SGW, PGW, HSS              |
| 5G NR      | gNodeB          | AMF, SMF, UPF, UDM              |

এই তালিকাটি দ্রুত revision-এর জন্য। বাস্তব নেটওয়ার্কে deployment ও architecture অনুযায়ী অতিরিক্ত উপাদানও থাকে।

## 7. MCQ Practice Test — 15 Questions

## Lesson 8 Quiz

0/15 answered

প্রতিটি প্রশ্নে একটি উত্তর নির্বাচন করে Submit Answers চাপো।

1\. BTS-এর পূর্ণরূপ কী?

A. Base Transceiver Station

B. Broadband Transmission System

C. Base Transfer Server

D. Binary Transceiver Service

2\. GSM network-এ একাধিক BTS নিয়ন্ত্রণ করে কোনটি?

A. HSS

B. BSC

C. PGW

D. UPF

3\. MSC-এর প্রধান কাজ কোনটি?

A. Circuit-switched call switching

B. Fiber splicing

C. DNS resolution

D. Radio spectrum তৈরি

4\. HLR কী সংরক্ষণ করে?

A. শুধু radio signal

B. Home subscriber information

C. শুধু Internet packets

D. Antenna frequency

5\. VLR-এর কাজ কী?

A. Serving area-তে temporary subscriber information রাখা

B. Web page render করা

C. Fiber loss মাপা

D. IP packet encrypt করা

6\. 3G UMTS radio base station কোনটি?

A. BTS only

B. NodeB

C. eNodeB

D. gNodeB

7\. 3G network-এ NodeB controller কোনটি?

A. RNC

B. MME

C. HSS

D. UPF

8\. LTE radio base station-এর নাম কী?

A. BSC

B. RNC

C. eNodeB

D. AMF

9\. LTE-তে control-plane mobility management-এর গুরুত্বপূর্ণ node কোনটি?

A. MME

B. SGW

C. PGW

D. BTS

10\. LTE user-plane traffic forward করার সঙ্গে কোন gateway যুক্ত?

A. SGW

B. HLR

C. BSC

D. RNC

11\. LTE network-কে external packet data network-এর সঙ্গে যুক্ত করে কোনটি?

A. PGW

B. VLR

C. BSC

D. NodeB

12\. LTE subscriber information-এর গুরুত্বপূর্ণ database/function কোনটি?

A. HSS

B. SGW

C. eNodeB

D. RNC

13\. 5G NR radio base station কোনটি?

A. BTS

B. NodeB

C. eNodeB

D. gNodeB

14\. 5G Core-এ user-plane packet forwarding করে কোনটি?

A. AMF

B. UPF

C. UDM

D. AUSF

15\. 5G Core-এ Access and Mobility Management Function কোনটি?

A. SMF

B. PCF

C. AMF

D. UPF

Submit Answers

পরবর্তী ক্লাস — Lesson 9: Telecom Signalling, SS7, Diameter, SIM/IMSI/IMEI ও Authentication। এতে থাকবে mobile subscriber কীভাবে network-এ authenticate হয়, SIM ও IMEI-এর পার্থক্য, এবং পরীক্ষায় আসতে পারে এমন MCQ।

# Lesson 9: Telecom Signalling, SS7, Diameter, SIM, IMSI, IMEI ও Authentication

Teletalk Bangladesh Limited Technical Exam • বাংলা Crash Course

এই লেসনে আমরা শিখব মোবাইল ফোন কীভাবে নেটওয়ার্কে নিবন্ধিত হয়, SIM কীভাবে subscriber-কে শনাক্ত করে, IMEI কী নির্দেশ করে, এবং SS7 ও Diameter কী কাজে ব্যবহৃত হয়।

## 1. Signalling কী?

Telecommunication network-এ signalling হলো network-এর বিভিন্ন device ও system-এর মধ্যে control information আদান-প্রদান, যার মাধ্যমে call setup, subscriber authentication, mobility এবং service management-এর মতো কাজ হয়।

উদাহরণ: তুমি কাউকে ফোন করলে network-কে জানতে হয়—

1. কলটি কোথায় পাঠাতে হবে।
2. subscriber-টি network ব্যবহার করার অনুমতি পাবে কি না।
3. অপর পক্ষের কাছে কল পৌঁছানো সম্ভব কি না।
4. কল শেষ হলে সংশ্লিষ্ট resources কীভাবে release হবে।

এ ধরনের control information আদান-প্রদানই signalling-এর অংশ।

## 2. SS7 কী?

[What is an SS7 Attack? | Certo Software](https://images.openai.com/static-rsc-4/648L3cf9wLnwUqWRkzTaEgeN-_wY4WTOGl7bk9bO4UG3oM6ebyhx2yeBubkFzja7jZ9wyDaQH8iennQSjs3KmXNwq6Wr25uVVqWQi2Kn9Y0t-Uld_ge8v92Ux-vxaJuWt0kyRYRx9D7N0JdsrK-nBnEc__NIgXJ2E48dSg6uGsE?purpose=inline)

[certosoftware.com](https://www.certosoftware.com/insights/ss7-attacks/)

SS7 = Signaling System No. 7

এটি traditional telephone ও mobile network-এ ব্যবহৃত একটি signalling protocol suite।

প্রধান ব্যবহার:

- Call setup ও call termination।
- Routing এবং mobility-related signalling।
- Subscriber information query।
- SMS delivery-সংক্রান্ত signalling।
- বিভিন্ন network element-এর মধ্যে control information বিনিময়।

### SS7-এর গুরুত্বপূর্ণ উপাদান

| উপাদান | পূর্ণরূপ                | কাজ                                          |
| ------ | ----------------------- | -------------------------------------------- |
| SSP    | Service Switching Point | Call switching ও signalling শুরু/পরিচালনা    |
| STP    | Signal Transfer Point   | Signalling message route করে                 |
| SCP    | Service Control Point   | Intelligent network service logic সরবরাহ করে |

পরীক্ষার ট্রিক: STP-এর কাজ signalling message transfer বা routing করা।

## 3. Diameter কী?

Diameter হলো IP-based network-এ ব্যবহৃত একটি protocol, যা authentication, authorization এবং accounting (AAA)-এর মতো কাজ সমর্থন করে।

4G LTE/EPC architecture-এ Diameter ব্যবহৃত হয় বিভিন্ন network function-এর মধ্যে subscriber ও policy-related signalling-এর জন্য।

উদাহরণ:

- MME ↔ HSS: Subscriber authentication ও subscription-related signalling।
- PCRF ↔ PCEF/P-GW: Policy ও charging control-এর জন্য Diameter interface ব্যবহৃত হতে পারে।

SS7 ও Diameter-এর ব্যবহার network generation এবং architecture অনুযায়ী আলাদা হতে পারে।

| SS7                                                 | Diameter                                           |
| --------------------------------------------------- | -------------------------------------------------- |
| Traditional circuit-switched telecom-এ বহুল ব্যবহৃত | IP-based network-এ বহুল ব্যবহৃত                    |
| Legacy mobile ও telephone signalling                | LTE/EPC-এর বিভিন্ন AAA/policy interface            |
| Signalling protocol suite                           | AAA ও policy-related signalling-এ ব্যবহৃত protocol |

## 4. SIM, IMSI, IMEI ও MSISDN-এর পার্থক্য

এই চারটি term MCQ-তে খুব গুরুত্বপূর্ণ।

[Close up of mobile phone sim card on white background](https://images.openai.com/static-rsc-4/0LBt1PmhFB4Nf3_2CWdPailYXb15QlyIl9DPlnkVjlOF4-lP-z8yVMOEzZbomhbZclVCYC_Lfj8sgw5n7jzlycwgxKIHKQ4N5bPIXlY5unehv3sNbH6UyXtsOXLpOa6P_utPlArOA-d1gpV2NaYAQ1qvAMLiFKIW-607Y86T3cQ77OMD4FWDolzCMNekycCb?purpose=inline)

SIM — Subscriber Identity Module

Subscriber-এর পরিচয় ও network authentication-এর জন্য প্রয়োজনীয় তথ্য/credentials সংরক্ষণ করে। আধুনিক SIM/UICC-এ security-related functionality থাকে।

[IMSI: The central subscriber identification explained](https://images.openai.com/static-rsc-4/S_MmhtXZdb0CrNb77InN-miacLyWINjyi29oF6w8kVdKMzlRvqX-3Z-f7zA0H2gB-7iumSRfDG3fU1df0q9Loz_dzMwcdU1sOyA8sTlpIdBYPNsAnQ76kwWavwoIehYFTZs_RUKN2l_zH-QmCnZ5mXl1mHGHEXE1rZkyS5EJBCg?purpose=inline)

IMSI — International Mobile Subscriber Identity

Mobile network-এ subscriber-কে শনাক্ত করার জন্য ব্যবহৃত identity। এটি সাধারণত SIM বা সংশ্লিষ্ট subscriber profile-এর সঙ্গে যুক্ত।

[Androidスマホの買取について｜買取総合サービスラクウル｜ソフマップ](https://images.openai.com/static-rsc-4/wDv_eZv76M5GbT26MnjK3PVLDw0McEMzYFU4KMirIONqqa7fY53watVfJcINkBLkYB8EjxsCC9ZDKPImGRdoZvpSztDeM1Gkq69kNZ2kiNpsIWil4ZuJKn2XSmDlWld2jrm5_Gi6yy_UJMslSMXMX7OjMxyASdysG18pBEPd6h0?purpose=inline)

IMEI — International Mobile Equipment Identity

Mobile equipment বা handset-কে শনাক্ত করার পরিচিতি। এটি subscriber identity নয়; device identity।

[Dial number concept.](https://images.openai.com/static-rsc-4/7_E_XrHBCYTNJekWofqZrYR0d_FuqHjh4TgIb2whavrj68LjFUSh8H_VHhnULf1agFXV0WzfJQcyTGo8rEWhCS5mPyS6f_euyLctyBgOexqmXPMte273EuB6BHmvLg1BYpAa4ahFQwyhMKzGKbCK27ezG0rb7TZZDPXElp-YJ5YVQpM22YQL7lfu14MoZHik?purpose=inline)

MSISDN — Mobile Station International Subscriber Directory Number

Subscriber-এর mobile telephone number—যে নম্বরে অন্যরা কল বা SMS পাঠাতে পারে।

### দ্রুত মনে রাখার টেবিল

| Term   | কী শনাক্ত করে?                                                   |
| ------ | ---------------------------------------------------------------- |
| SIM    | Subscriber identity ও authentication credentials ধারণকারী module |
| IMSI   | Subscriber                                                       |
| IMEI   | Mobile equipment/device                                          |
| MSISDN | Mobile telephone number                                          |

উদাহরণ: একই ফোনে SIM পরিবর্তন করলে IMSI ও MSISDN বদলাতে পারে, কিন্তু handset-এর IMEI সাধারণত একই থাকে। Dual-SIM device-এ একাধিক IMEI থাকতে পারে।

## 5. Mobile Network Authentication কীভাবে কাজ করে?

মোবাইল ফোন চালু করে network-এ যুক্ত হওয়ার সময় network subscriber-এর পরিচয় যাচাই করে।

1\. Mobile / SIM

Network-এ registration request

2\. Base Station / RAN

Radio access-এর মাধ্যমে request বহন

3\. Core Network

Subscriber authentication ও authorization process

4\. Authentication Result

সফল হলে network access-এর পরবর্তী ধাপ চলতে পারে

### Authentication-এর মূল ধারণা

- SIM-এ থাকা secret credential এবং network-এর subscriber data ব্যবহার করে authentication হয়।
- Network challenge পাঠাতে পারে; SIM-সংক্রান্ত security mechanism সেই challenge-এর response তৈরি করে।
- Network response যাচাই করে।
- সফল authentication মানেই সব service স্বয়ংক্রিয়ভাবে অনুমোদিত নয়—subscription, policy এবং অন্যান্য checks-ও প্রযোজ্য হতে পারে।

2G GSM: A3/A8-সম্পর্কিত authentication ও key-generation ধারণা গুরুত্বপূর্ণ।

3G/4G/5G: AKA (Authentication and Key Agreement) family-এর পদ্ধতি ব্যবহৃত হয়; 4G/5G-তে authentication ও key management আরও উন্নত।

## 6. EIR ও AuC কী?

- EIR — Equipment Identity Register: Device identity, যেমন IMEI-সংক্রান্ত equipment checking-এ ব্যবহৃত হতে পারে। Network policy অনুযায়ী কোনো device-কে allow, monitor বা block করা হতে পারে।
- AuC — Authentication Centre: Subscriber authentication-সংক্রান্ত secret data ও authentication information ব্যবস্থাপনায় সাহায্য করে।

মনে রাখবে:

- HLR/HSS: Subscriber information।
- AuC: Authentication-related data।
- EIR: Equipment identity checking।
- IMSI: Subscriber identity।
- IMEI: Device identity।

## 7. MCQ Practice Test — 15 Questions

## Lesson 9 Quiz

0/15 answered

প্রতিটি প্রশ্নে একটি উত্তর নির্বাচন করো, তারপর Submit Answers চাপো।

1\. SS7-এর পূর্ণরূপ কী?

A. Signaling System No. 7

B. Subscriber Service 7

C. Signal Switching Type 7

D. System Security Terminal 7

2\. SS7 network-এ STP-এর প্রধান কাজ কী?

A. Signalling message route করা

B. SIM manufacture করা

C. Internet browsing

D. Radio signal amplify করা

3\. Diameter প্রধানত কোন ধরনের network environment-এ ব্যবহৃত হয়?

A. শুধু analog telephone

B. IP-based network signalling

C. শুধু FM radio

D. শুধু optical fiber splicing

4\. IMSI কী শনাক্ত করে?

A. Mobile subscriber

B. Handset model only

C. Telephone tower

D. Wi-Fi router

5\. IMEI কী শনাক্ত করে?

A. Subscriber-এর telephone number

B. Mobile equipment/device

C. Subscriber-এর password

D. Cell tower location

6\. MSISDN কী?

A. Subscriber-এর mobile telephone number

B. Radio frequency

C. Authentication key

D. Base station ID only

7\. SIM-এর একটি গুরুত্বপূর্ণ কাজ কী?

A. Subscriber authentication-এ প্রয়োজনীয় credentials রাখা

B. Internet-এর সব route নির্ধারণ

C. Fiber cable repair

D. Tower-এর বিদ্যুৎ সরবরাহ

8\. AuC-এর পূর্ণরূপ কী?

A. Authentication Centre

B. Automatic User Controller

C. Access Utility Channel

D. Antenna Unit Connector

9\. EIR-এর সঙ্গে কোন identity সবচেয়ে বেশি সম্পর্কিত?

A. IMEI

B. MSISDN

C. DNS name

D. Subnet mask

10\. একই handset-এ SIM পরিবর্তন করলে সাধারণত কোনটি অপরিবর্তিত থাকে?

A. MSISDN

B. IMSI

C. IMEI

D. SIM identity

11\. AKA-এর পূর্ণরূপ কী?

A. Authentication and Key Agreement

B. Automatic Key Allocation

C. Access Knowledge Algorithm

D. Advanced Kernel Authentication

12\. Authentication সফল হলে কী বোঝায়?

A. সব service সবসময় অনুমোদিত

B. পরবর্তী access procedure-এ এগোনো সম্ভব; অন্যান্য checks-ও থাকতে পারে

C. IMEI পরিবর্তন হয়েছে

D. Network-এ আর কোনো security check নেই

13\. HLR/HSS-এর প্রধান ভূমিকা কী?

A. Subscriber information পরিচালনা

B. শুধু handset battery monitor

C. Optical signal generate

D. Cable connector clean

14\. 2G GSM authentication-এ কোন algorithm pair-এর ধারণা গুরুত্বপূর্ণ?

A. A3/A8

B. HTTP/FTP

C. HTML/CSS

D. TCP/IP only

15\. নিচের কোন জোড়াটি সঠিক?

A. IMSI—Device identity

B. IMEI—Subscriber identity

C. IMSI—Subscriber identity

D. MSISDN—Authentication algorithm

Submit Answers

পরবর্তী ক্লাস: Lesson 10 — Telecom Transmission, Microwave Links, Multiplexing ও Network Synchronization। এতে থাকবে microwave communication, LOS, SDH/PDH, TDM/FDM, bandwidth, transmission loss এবং পরীক্ষার MCQ।

# Lesson 10: Telecom Transmission, Microwave Links, Multiplexing & Synchronization

Teletalk Bangladesh Limited Technical Exam • বাংলা Crash Course

এই লেসনে শিখব মোবাইল টাওয়ার থেকে core network-এ ডেটা কীভাবে যায়, microwave link কীভাবে কাজ করে, LOS, TDM, FDM, PDH, SDH, bandwidth ও network synchronization কী—এবং পরীক্ষার জন্য গুরুত্বপূর্ণ MCQ।

## 1. Telecom Transmission কী?

Telecom Transmission হলো এক স্থান থেকে অন্য স্থানে voice, data বা অন্যান্য signal পাঠানোর প্রক্রিয়া।

মোবাইল নেটওয়ার্কে একটি সাধারণ যোগাযোগের পথ:

Mobile Tower / BTS / eNodeB

Transmission / Backhaul

Optical Fiber অথবা Microwave Link

Aggregation / Core Network

Transmission-এর প্রধান মাধ্যম:

- Optical Fiber: আলো ব্যবহার করে ডেটা পাঠায়; উচ্চ capacity ও দীর্ঘ দূরত্বের জন্য উপযোগী।
- Microwave Radio: Radio wave ব্যবহার করে দুইটি উপযুক্ত স্থানের মধ্যে wireless link তৈরি করে।
- Copper Cable: কিছু পুরোনো বা নির্দিষ্ট infrastructure-এ ব্যবহৃত হয়।

## 2. Microwave Communication কী?

[LOS Requirements in Microwave Communication: Clear Path Needed for Signal Integrity | Shah Yar Hussaini posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/kDyS1OXrWuJbX-gx7xDrL7NDaUSKUldQmrCE--fhv5B4tAtjwAisJKW_NuyB1PEN6sRngHyyaxZzUClvNqw3dZZr71mnC2oDEV0HloAYIi1XVRsswutMdzMHgrXrJ3Onfqb17KDQa5WR5-T34AhgSeooArVhsfNPAlW1hys4DEI?purpose=inline)

[linkedin.com](https://www.linkedin.com/posts/shahyars_in-microwave-communication-los-line-activity-7420114074052501505-ra6d)

Microwave communication-এ উচ্চ-ফ্রিকোয়েন্সির electromagnetic wave ব্যবহার করে সাধারণত দুটি স্থানের মধ্যে point-to-point communication করা হয়।

Telecom-এ ব্যবহার:

- যেখানে fiber নেওয়া কঠিন বা ব্যয়বহুল, সেখানে tower backhaul।
- দুর্গম এলাকায় network connectivity।
- Temporary বা দ্রুত স্থাপনযোগ্য communication link।

### Microwave Link-এর গুরুত্বপূর্ণ বৈশিষ্ট্য

- সাধারণত দুই প্রান্তে directional antenna ব্যবহার করা হয়।
- সঠিক alignment গুরুত্বপূর্ণ।
- দূরত্ব ও frequency অনুযায়ী path loss বাড়ে।
- বৃষ্টি, বাধা, multipath এবং link-এর design অনুযায়ী signal quality প্রভাবিত হতে পারে।

মনে রাখবে: Microwave link হলো wireless transmission; Optical fiber হলো guided optical transmission।

## 3. LOS — Line of Sight

LOS-এর পূর্ণরূপ Line of Sight। Microwave link-এ transmitter ও receiver antenna-র মধ্যে যথেষ্ট clear propagation path থাকা প্রয়োজন।

[#kingsat #fresnelzone #rfengineering #wirelesscommunication #microwavelinks #satellitecommunication #microwaveantenna #radiopropagation | Alex Kang | 15 comments](https://images.openai.com/static-rsc-4/XgtZCcSexOSWtLKlvEvldRg9hXgYjwMXu9VR8wDtmSnSIfQqJ-AuFNWfTaI4guQXvFcsBqsupZaHjFdldIF8ZJMpZV4tV8dobKfIdizBiMhl1uIqC4ikwWiMNS5O6r8_cH6TfG-2beYa4IH14IlTKKo_1wPmUf9ODat6j3uVI24?purpose=inline)

[linkedin.com](https://www.linkedin.com/feed/update/urn%3Ali%3Aactivity%3A7406548254278172672/)

LOS design-এর সময় শুধু চোখে দেখা যায় কি না, সেটাই যথেষ্ট নয়। Fresnel zone-ও বিবেচনা করতে হয়, কারণ এই অঞ্চলে বাধা থাকলে signal quality কমতে পারে।

Microwave link-এ সমস্যা হওয়ার কারণ:

- পাহাড়, ভবন বা গাছের মতো বাধা।
- Antenna misalignment।
- Heavy rain—বিশেষ করে উচ্চ microwave frequency-তে।
- Multipath fading।
- অপর্যাপ্ত link margin।

পরীক্ষার ট্রিক: LOS = Line of Sight; Fresnel zone clearance microwave link design-এর গুরুত্বপূর্ণ বিষয়।

## 4. Multiplexing কী?

Multiplexing হলো একাধিক signal বা data stream-কে একসঙ্গে একটি shared transmission medium দিয়ে পাঠানোর পদ্ধতি।

[Understanding MUX and DEMUX: A Guide to Network Efficiency](https://images.openai.com/static-rsc-4/IWgFzTYWZT07Pv2h6uXMcLMiLtfQ_VL_ZIcpQD0ITFZeoKvNkatGra-iY_EU6_A8PUfgTix43xvF6TWr9RouLpBpofqAHlXTejr5cfL49k-miMKOh35tpSPleNPpugBOa2HiD4qVSdx3ojhm2qUubI0hUb28v-yVafEIUX1cJ8Q?purpose=inline)

[resources.l-p.com](https://resources.l-p.com/knowledge-center/mux-and-demux-role-in-data-transmission-efficiency)

### Multiplexing-এর ধরন

[PPT - Introduction PowerPoint Presentation, free download - ID:6222415](https://images.openai.com/static-rsc-4/CoR-PJEneVuL3Eq9jch_UUn_BSqF5zaw0YTyZ6EZYwg4No28NQAEAlEGgIcuGfjos8rMyeD0BjUyI511TuHf4POnyIIKoKQssiqQ9xS4xx27RRIlwVTzYYuMgHZTsiv4RrOUY_eZkrWSRBm-Evb51GNYDzm0AdUvEmyDgDkasJ8?purpose=inline)

FDM — Frequency Division Multiplexing

আলাদা signal-কে আলাদা frequency band দেওয়া হয়। একাধিক signal একই সময়ে transmission করতে পারে।

[Time Division Multiplexing: Working Principle, Diagram, Differences &  Applications](https://images.openai.com/static-rsc-4/rGNaHP2PtS0DR-3QoKExl6LVilqbfy8CANX8lfaHIgYaU6nF02csAE3CbVB-BYqtMX1JXOTs72c0a0vfu6l6vHL0Lu1Q3VkTpoMtjzY5JaEoO1c3iTgXTaEIt7VvMNgmkJB-JbmuLsccz6rn7GpixfcNXLlAixXtoOUnnm2u5eo?purpose=inline)

TDM — Time Division Multiplexing

আলাদা signal-কে আলাদা time slot দেওয়া হয়। প্রত্যেকে নির্ধারিত সময়ে transmission করে।

[Multiplexing Techniques: The Invisible Highway System of Your Data](https://images.openai.com/static-rsc-4/giGxo3LxPKMd3bhapM0U_kUO8BMRQrqTL_moKq6Y8SQh1a8kf31wzeTX_iBCWQJeNzk8gwvjAoe4j8X6NJtQkZ8CMX7s31YGtxTgRKp6GllQDv_on8ZfWohIGYOzl8TK9h_IVLi-HIM21gqAAbeM2vMlltrkTs5idZt5zJLPwyI?purpose=inline)

WDM — Wavelength Division Multiplexing

Optical fiber-এ আলাদা wavelength বা optical channel ব্যবহার করে একাধিক data stream পাঠানো হয়।

| বিষয়          | FDM                  | TDM                       | WDM                      |
| ------------- | -------------------- | ------------------------- | ------------------------ |
| সম্পদ ভাগ হয়  | Frequency            | Time                      | Optical wavelength       |
| সাধারণ উদাহরণ | Radio broadcasting   | Digital time-slot systems | Fiber-optic transmission |
| মূল ধারণা     | আলাদা frequency band | আলাদা time slot           | আলাদা optical wavelength |

## 5. PDH ও SDH

PDH ও SDH হলো digital transmission technology, যা telecom network-এ একাধিক data stream বহন ও multiplex করতে ব্যবহৃত হয়েছে/হয়।

### PDH — Plesiochronous Digital Hierarchy

- বিভিন্ন digital stream-এর timing প্রায় একই, কিন্তু পুরোপুরি synchronized নাও হতে পারে।
- Stream multiplex করার সময় justification বা stuffing-এর প্রয়োজন হতে পারে।
- পুরোনো digital telephone transmission system-এ ব্যবহৃত হয়েছে।

### SDH — Synchronous Digital Hierarchy

- Synchronized digital transport-এর জন্য তৈরি।
- High-capacity transmission এবং network management সহজ করতে সাহায্য করে।
- Add/drop multiplexing-এর মাধ্যমে পুরো stream demultiplex না করেও নির্দিষ্ট traffic access করা যায়।
- Optical transport network-এ ঐতিহাসিকভাবে গুরুত্বপূর্ণ।

| PDH                           | SDH                                            |
| ----------------------------- | ---------------------------------------------- |
| Plesiochronous timing         | Synchronous timing                             |
| Multiplexing তুলনামূলক জটিল   | Structured multiplexing ও management           |
| পুরোনো transmission hierarchy | উচ্চ-capacity transport-এর জন্য বেশি সুবিধাজনক |

মনে রাখবে: PDH = Plesiochronous; SDH = Synchronous।

## 6. Bandwidth, Data Rate ও Latency

এই তিনটি শব্দ এক নয়।

- Bandwidth: Communication channel কতটা frequency range ব্যবহার করে, সাধারণত Hz-এ মাপা হয়। Network context-এ শব্দটি data-carrying capacity বোঝাতেও ব্যবহৃত হয়।
- Data Rate: প্রতি সেকেন্ডে কত bit পাঠানো হচ্ছে; একক bps, kbps, Mbps, Gbps।
- Latency: ডেটা এক প্রান্ত থেকে অন্য প্রান্তে পৌঁছাতে যে সময় লাগে; সাধারণত ms-এ প্রকাশ করা হয়।

উদাহরণ:

একটি link-এর data rate 100 Mbps হতে পারে, কিন্তু congestion বা propagation delay-এর কারণে latency বেশি হতে পারে। অর্থাৎ উচ্চ data rate মানেই সর্বদা কম latency নয়।

### দ্রুত একক রূপান্তর

- 1 Mbps = \\(10^6\\) bits per second।
- 1 Gbps = \\(10^9\\) bits per second।
- 1 byte = 8 bits।

তাই 80 Mbps-এর link-এর তাত্ত্বিক সর্বোচ্চ data rate প্রায় 10 MB/s—protocol overhead ও অন্যান্য সীমাবদ্ধতা বাদ দিয়ে।

## 7. Network Synchronization

Telecom network-এ timing synchronization গুরুত্বপূর্ণ, কারণ অনেক system নির্দিষ্ট সময় ও clock reference অনুযায়ী কাজ করে।

Synchronization-এর প্রয়োজন:

- Digital transmission-এর timing ঠিক রাখা।
- বিভিন্ন network element-এর মধ্যে timing coordination।
- Mobile network-এ নির্দিষ্ট radio technology ও deployment অনুযায়ী timing alignment।
- কিছু radio system-এ Time Division Duplex (TDD) ব্যবস্থায় transmission ও reception-এর timing সমন্বয় করা।

### Clock ও Synchronization

- Clock: Timing reference প্রদান করে।
- Frequency synchronization: Clock-এর frequency মিলিয়ে রাখা।
- Time/phase synchronization: Clock-এর time বা phase-এর পার্থক্য নিয়ন্ত্রণ করা।

Network synchronization-এর জন্য GNSS, Precision Time Protocol (PTP) বা SyncE-এর মতো প্রযুক্তি ব্যবহার হতে পারে—network design ও প্রয়োজন অনুযায়ী।

পরীক্ষার ট্রিক: PTP-এর পূর্ণরূপ Precision Time Protocol; SyncE-এর পূর্ণরূপ Synchronous Ethernet।

## 8. Link Budget ও Signal Loss

একটি communication link-এ receiver-এর কাছে কত power পৌঁছাবে, তা বোঝার জন্য link budget ব্যবহার করা হয়।

সরলভাবে:

\\[ P_r=P_t+G_t+G_r-L \\]

এখানে:

- \\(P_r\\) = Received power (dBm)
- \\(P_t\\) = Transmit power (dBm)
- \\(G_t\\) = Transmitting antenna gain (dB)
- \\(G_r\\) = Receiving antenna gain (dB)
- \\(L\\) = মোট path ও অন্যান্য loss (dB)

উদাহরণ:

Transmit power = 20 dBm, দুই antenna-র gain যথাক্রমে 10 dB ও 10 dB, মোট loss = 100 dB হলে:

\\[ P_r=20+10+10-100=-60\ \text{dBm} \\]

বাস্তব link budget-এ cable loss, connector loss, rain fade এবং প্রয়োজনীয় fade margin-ও হিসাব করা হতে পারে।

## 9. MCQ Practice Test — 15 Questions

## Lesson 10 Quiz

0/15 answered

প্রতিটি প্রশ্নে একটি উত্তর বেছে নাও, তারপর Submit Answers চাপো।

1\. Microwave communication-এ LOS-এর পূর্ণরূপ কী?

A. Line of Sight

B. Level of Signal

C. Link of Service

D. Loss of Spectrum

2\. Microwave link-এ Fresnel zone clearance কেন গুরুত্বপূর্ণ?

A. Signal propagation-এ বাধার প্রভাব কমাতে

B. SIM number পরিবর্তন করতে

C. IP address তৈরি করতে

D. Battery charge করতে

3\. FDM-এর পূর্ণরূপ কী?

A. Frequency Division Multiplexing

B. Fast Data Management

C. Fiber Distribution Method

D. Frequency Data Modulation

4\. TDM-এ signal কীভাবে ভাগ করা হয়?

A. আলাদা time slot-এ

B. আলাদা IP address-এ

C. আলাদা antenna tower-এ

D. আলাদা optical fiber-এ বাধ্যতামূলকভাবে

5\. WDM সাধারণত কোন মাধ্যমে ব্যবহৃত হয়?

A. Optical fiber

B. Copper telephone wire only

C. Loudspeaker

D. Keyboard

6\. PDH-এর পূর্ণরূপ কী?

A. Plesiochronous Digital Hierarchy

B. Packet Data Highway

C. Primary Digital Hub

D. Parallel Data Host

7\. SDH-এর পূর্ণরূপ কী?

A. Synchronous Digital Hierarchy

B. Signal Distribution Hardware

C. System Data Host

D. Subscriber Digital Hub

8\. নিচের কোনটি data rate-এর একক?

A. Mbps

B. dBm

C. dB

D. ms

9\. Latency সাধারণত কী দিয়ে প্রকাশ করা হয়?

A. Milliseconds (ms)

B. dB/km

C. Volts

D. Wavelength only

10\. 1 byte সমান কত bit?

A. 2

B. 4

C. 8

D. 16

11\. PTP-এর পূর্ণরূপ কী?

A. Precision Time Protocol

B. Packet Transfer Path

C. Primary Telecom Port

D. Power Timing Process

12\. SyncE-এর পূর্ণরূপ কী?

A. Synchronous Ethernet

B. Signal Exchange

C. System Encryption

D. Synchronized Equipment

13\. Link budget-এ antenna gain সাধারণত কোন এককে প্রকাশ করা হয়?

A. dB

B. dBm only

C. Mbps

D. ms

14\. Transmit power 20 dBm, antenna gains 10 dB ও 10 dB, total loss 100 dB হলে received power কত?

A. −60 dBm

B. 40 dBm

C. −100 dBm

D. 100 dBm

15\. Telecom transmission-এ backhaul-এর কাজ কী?

A. Radio access site-কে aggregation/core network-এর সঙ্গে যুক্ত করা

B. SIM-এর PIN পরিবর্তন করা

C. শুধু handset screen চালানো

D. DNS record মুছে ফেলা

Submit Answers

পরবর্তী ক্লাস: Lesson 11 — IP Routing, Switching, VLAN, Subnetting ও Network Troubleshooting। এতে থাকবে Switch বনাম Router, VLAN, Default Gateway, `ping`, `traceroute`, `ipconfig`/`ip`, এবং subnetting-এর অঙ্কসহ MCQ।

# Teletalk Technical Exam Preparation — Lesson 11

## IP Routing, Switching, VLAN, Subnetting ও Network Troubleshooting

এই লেসনে আমরা এমন কিছু Networking topic শিখব, যেগুলো টেলিকম ও IT technical exam-এর জন্য গুরুত্বপূর্ণ। প্রতিটি topic-এ থাকবে সংজ্ঞা, কাজ, পার্থক্য, উদাহরণ এবং MCQ practice।

## 1. Network Switch ও Router

[24-Port 10/100/1000Mbps Gigabit Ethernet Network Switch - Desktop/Wall](https://images.openai.com/static-rsc-4/fzcQ102_q4SbnTllA9KzVwEOimsz9idg8fmY2W9_MeSg0JgjKM6KFumnxJLoVmjQNvdCcE0vEsk4D-yLHFpRPNUFPnZvEIl68CJCaqb2uiX3epkqTF2t2WeBLTS3jy6SZfflHdYWF1wtMmgNGLWi6MUtFmbMZjSoenvg9gPhXIk?purpose=inline)

Switch

- একই LAN-এর একাধিক device-কে সংযুক্ত করে।
- সাধারণত MAC address ব্যবহার করে Ethernet frame সঠিক port-এ পাঠায়।
- প্রধানত OSI Layer 2-এ কাজ করে।
- উদাহরণ: একই অফিসের PC, printer ও server-কে সংযুক্ত করা।

[Cisco C1111X-8P Integrated Services Router with 8 Gigabit Ethernet Ports | New](https://images.openai.com/static-rsc-4/Av9-18ZaJd-ooMKLj020noSffvMZ3_qqSiscgO8GvlUrdH58X6mxuCPYQAI55fPFlImv--60hOaTmVbLfZSQ3ejZujh5a1hJ4XUS3N-xj6Ej5ovIDjEGIdaTX9AXsQwJnPXF9Lyk35cdXIpRrPp5-ce37wiVg1go4P0TuPwkwr4?purpose=inline)

Router

- ভিন্ন IP network-কে সংযুক্ত করে।
- সাধারণত destination IP address দেখে packet-এর পরবর্তী পথ নির্ধারণ করে।
- প্রধানত OSI Layer 3-এ কাজ করে।
- উদাহরণ: অফিসের LAN-কে Internet-এর সঙ্গে সংযুক্ত করা।

মনে রাখার কৌশল: Switch → MAC address → Layer 2; Router → IP address → Layer 3।

| বিষয়           | Switch                        | Router                          |
| -------------- | ----------------------------- | ------------------------------- |
| প্রধান address | MAC                           | IP                              |
| OSI layer      | Layer 2                       | Layer 3                         |
| মূল কাজ        | LAN-এর মধ্যে frame forwarding | Network-এর মধ্যে packet routing |
| তথ্য সংরক্ষণ   | MAC address table             | Routing table                   |

মনে রাখবে: Layer 3 switch-ও আছে; তবে সাধারণ পরীক্ষার প্রশ্নে উপরের পার্থক্যটিই বেশি ব্যবহৃত হয়।

## 2. IP Routing কী?

Routing হলো source network থেকে destination network-এ packet পাঠানোর জন্য উপযুক্ত পথ নির্ধারণ করা।

PC A&#x20;

192.168.1.10

Router&#x20;

Routing table দেখে next hop নির্বাচন করে

PC B&#x20;

192.168.2.20

দুটি আলাদা IP network-এর মধ্যে Router packet পাঠাচ্ছে।

### Routing-এর গুরুত্বপূর্ণ ধরন

- Static Routing: Network administrator হাতে route configure করেন।
- Dynamic Routing: Routing protocol ব্যবহার করে router স্বয়ংক্রিয়ভাবে route শিখতে ও update করতে পারে।
- Default Route: Routing table-এ আরও নির্দিষ্ট route না থাকলে ব্যবহৃত route।

গুরুত্বপূর্ণ protocol:

| Protocol | পূর্ণরূপ / বৈশিষ্ট্য                                                  |
| -------- | --------------------------------------------------------------------- |
| RIP      | Routing Information Protocol; hop count ব্যবহার করে                   |
| OSPF     | Open Shortest Path First; link-state protocol                         |
| BGP      | Border Gateway Protocol; autonomous system-এর মধ্যে routing-এ ব্যবহৃত |
| EIGRP    | Enhanced Interior Gateway Routing Protocol                            |

Exam fact: RIP-এর সর্বোচ্চ গ্রহণযোগ্য hop count 15; 16 hop-কে unreachable ধরা হয়।

## 3. VLAN — Virtual Local Area Network

VLAN হলো একটি physical switch network-কে একাধিক logical LAN-এ ভাগ করার পদ্ধতি।

ধরো, একটি টেলিকম অফিসে একই switch-এ তিনটি বিভাগ যুক্ত:

- HR Department — VLAN 10
- Accounts Department — VLAN 20
- IT Department — VLAN 30

VLAN ব্যবহার করে বিভাগগুলোকে আলাদা logical broadcast domain-এ রাখা যায়।

একটি Managed Switch

VLAN 10

HR

VLAN 20

Accounts

VLAN 30

IT

VLAN-এর মধ্যে যোগাযোগ নিয়ন্ত্রণ বা আন্তঃVLAN যোগাযোগের জন্য সাধারণত Layer 3 routing প্রয়োজন।

### VLAN-এর গুরুত্বপূর্ণ terms

- Access Port: সাধারণত একটি নির্দিষ্ট VLAN-এর end device-কে যুক্ত করে।
- Trunk Port: একাধিক VLAN-এর traffic বহন করতে পারে।
- IEEE 802.1Q: Ethernet trunk frame-এ VLAN tagging-এর বহুল ব্যবহৃত standard।
- Broadcast Domain: যে logical network-এ Layer 2 broadcast ছড়িয়ে পড়ে।

MCQ trap: VLAN তৈরি করলেই সব VLAN পরস্পরের সঙ্গে সরাসরি যোগাযোগ করতে পারবে না। Inter-VLAN routing প্রয়োজন হতে পারে।

## 4. Subnetting — IP Network ভাগ করা

Subnetting হলো একটি IP network-কে ছোট ছোট subnet-এ ভাগ করা।

উদাহরণ: `192.168.1.0/24`

এখানে `/24` মানে প্রথম 24 bit network portion-এর জন্য ব্যবহৃত হচ্ছে।

| CIDR  | Subnet mask     | মোট IPv4 address | সাধারণ usable host |
| ----- | --------------- | ---------------- | ------------------ |
| `/24` | 255.255.255.0   | 256              | 254                |
| `/25` | 255.255.255.128 | 128              | 126                |
| `/26` | 255.255.255.192 | 64               | 62                 |
| `/27` | 255.255.255.224 | 32               | 30                 |
| `/28` | 255.255.255.240 | 16               | 14                 |
| `/30` | 255.255.255.252 | 4                | 2                  |

এগুলো সাধারণ IPv4 subnet-এর হিসাব, যেখানে network ও broadcast address host হিসেবে ব্যবহার করা হয় না।

### গুরুত্বপূর্ণ formula

\\[ \text{Host bits}=32-\text{Prefix length} \\]

\\[ \text{Total addresses}=2^{\text{Host bits}} \\]

সাধারণ IPv4 subnet-এ:

\\[ \text{Usable hosts}=2^{h}-2 \\]

এখানে \\(h\\) হলো host bit-এর সংখ্যা।

### উদাহরণ: `/26`-এ কতটি usable host?

- Host bits = \\(32-26=6\\)
- মোট address = \\(2^6=64\\)
- Usable host = \\(64-2=62\\)

`192.168.1.0/26`-এর ক্ষেত্রে:

- Network address: `192.168.1.0`
- Usable host range: `192.168.1.1 – 192.168.1.62`
- Broadcast address: `192.168.1.63`

`192.168.1.64/26` হলো একই `/24` network-এর পরবর্তী `/26` subnet-এর network address।

পরীক্ষায় মনে রাখবে: `/24` থেকে `/25` করলে subnet-এর সংখ্যা দ্বিগুণ হয়, আর প্রতিটি subnet-এ address-এর সংখ্যা অর্ধেক হয়।

## 5. Network Troubleshooting

Network কাজ না করলে ধাপে ধাপে পরীক্ষা করতে হয়। সরাসরি বড় configuration পরিবর্তন না করে আগে সমস্যার জায়গা চিহ্নিত করবে।

| Command               | কাজ                                                     |
| --------------------- | ------------------------------------------------------- |
| `ping 8.8.8.8`        | IP connectivity পরীক্ষা                                 |
| `ping google.com`     | connectivity-এর সঙ্গে DNS resolution-ও পরীক্ষা হতে পারে |
| `ip addr`             | Linux-এ interface ও IP address দেখা                     |
| `ip route`            | Linux routing table দেখা                                |
| `traceroute 8.8.8.8`  | packet-এর পথ অনুসরণ                                     |
| `nslookup google.com` | DNS lookup পরীক্ষা                                      |
| `ipconfig`            | Windows-এ IP configuration দেখা                         |
| `tracert 8.8.8.8`     | Windows-এ route trace                                   |

### সাধারণ সমস্যার লক্ষণ

সমস্যা: IP address নেই

DHCP server, cable/Wi-Fi, network adapter এবং DHCP configuration পরীক্ষা করো।

সমস্যা: IP দিয়ে সংযোগ হয়, domain name দিয়ে হয় না

DNS configuration বা DNS server-এর সমস্যা থাকতে পারে।

সমস্যা: Local network চলে, কিন্তু Internet চলে না

Default gateway, router, upstream connection ও firewall পরীক্ষা করো।

সমস্যা: কিছু service বা port কাজ করছে না

Firewall rule, service status, routing এবং port configuration পরীক্ষা করো।

গুরুত্বপূর্ণ: `ping` ব্যর্থ হলেই যে network সম্পূর্ণ বন্ধ, তা নয়। Firewall বা ICMP filtering-এর কারণেও ping-এর reply নাও আসতে পারে।

## 6. Lesson 11 — Exam MCQ Practice

এবার 12টি প্রশ্ন দিয়ে নিজের প্রস্তুতি যাচাই করো। উত্তর নির্বাচন করে Check Answers চাপ দাও।

## Practice Test

0/12 answered

1\. কোন device সাধারণত MAC address ব্যবহার করে Layer 2-এ frame forward করে?

A. Router

B. Switch

C. Modem

D. Repeater

2\. Router সাধারণত কোন address দেখে packet route করে?

A. MAC address only

B. Port number only

C. Destination IP address

D. File name

3\. RIP-এর সর্বোচ্চ গ্রহণযোগ্য hop count কত?

A. 7

B. 15

C. 16

D. 255

4\. OSPF কোন ধরনের routing protocol?

A. Link-state

B. Distance-vector

C. Application protocol

D. Transport protocol

5\. একাধিক VLAN-এর traffic বহন করতে সাধারণত কোন port ব্যবহৃত হয়?

A. Access port

B. Console port only

C. Trunk port

D. USB port

6\. VLAN tagging-এর সঙ্গে কোন standard যুক্ত?

A. IEEE 802.11

B. IEEE 802.1Q

C. IEEE 802.3af only

D. IEEE 802.15

7\. একটি সাধারণ IPv4 /24 subnet-এ usable host কয়টি?

A. 128

B. 256

C. 254

D. 255

8\. একটি সাধারণ IPv4 /26 subnet-এ usable host কয়টি?

A. 30

B. 62

C. 64

D. 126

9\. 192.168.1.0/26 subnet-এর broadcast address কোনটি?

A. 192.168.1.1

B. 192.168.1.62

C. 192.168.1.63

D. 192.168.1.64

10\. Linux-এ routing table দেখতে কোন command ব্যবহার করা হয়?

A. ip route

B. ip addr

C. nslookup

D. mkdir

11\. IP address দিয়ে সংযোগ হচ্ছে কিন্তু domain name দিয়ে হচ্ছে না—কোন সমস্যাটি সন্দেহ করবে?

A. শুধু monitor

B. DNS

C. Keyboard

D. RAM

12\. ভিন্ন VLAN-এর মধ্যে যোগাযোগ করাতে সাধারণত কী প্রয়োজন?

A. শুধু VLAN নাম পরিবর্তন

B. শুধু MAC table মুছে ফেলা

C. Inter-VLAN routing

D. শুধু DHCP বন্ধ করা

Check Answers

## দ্রুত Revision — এক নজরে

- Switch: MAC address, Layer 2।
- Router: IP address, Layer 3।
- RIP: সর্বোচ্চ 15 hop।
- OSPF: Link-state routing protocol।
- VLAN: Logical LAN এবং পৃথক broadcast domain।
- 802.1Q: VLAN tagging।
- /24: 254 usable host; /26: 62 usable host।
- DNS: Domain name-কে IP address-এ resolve করে।
- `ip route`: Linux routing table দেখায়।
- Inter-VLAN routing: ভিন্ন VLAN-এর মধ্যে যোগাযোগ।

পরবর্তী লেসন হবে Lesson 12: Cybersecurity, Firewall, VPN, Encryption, Authentication এবং Common Network Attacks—টেকনিক্যাল পরীক্ষার জন্য গুরুত্বপূর্ণ ধারণা ও MCQ-সহ।

# Teletalk Technical Exam Preparation — Lesson 12

## Cybersecurity, Firewall, VPN, Encryption, Authentication ও Network Attacks

এই লেসনে আমরা Cybersecurity-এর গুরুত্বপূর্ণ বিষয়গুলো সহজ বাংলায় শিখব। টেলিকম ও IT technical exam-এর জন্য সংজ্ঞা, পার্থক্য, উদাহরণ এবং MCQ-তে বেশি কাজে লাগবে এমন তথ্যগুলোতে গুরুত্ব দেব।

## 1. Cybersecurity কী?

Cybersecurity হলো computer, network, server, application ও data-কে unauthorized access, attack, damage এবং theft থেকে সুরক্ষিত রাখার প্রক্রিয়া।

Cybersecurity-এর মূল তিনটি লক্ষ্যকে বলা হয় CIA Triad।

C — Confidentiality (গোপনীয়তা)

অনুমোদিত ব্যক্তি ছাড়া অন্য কেউ যেন তথ্য দেখতে না পারে।

উদাহরণ: Customer database শুধু অনুমোদিত কর্মী দেখতে পারবেন।

I — Integrity (তথ্যের অখণ্ডতা)

অনুমতি ছাড়া যেন data পরিবর্তন বা নষ্ট না হয়।

উদাহরণ: Transaction-এর amount গোপনে পরিবর্তন ঠেকানো।

A — Availability (প্রাপ্যতা)

প্রয়োজনের সময় অনুমোদিত ব্যবহারকারী যেন system ও data ব্যবহার করতে পারেন।

উদাহরণ: Network redundancy ও backup-এর মাধ্যমে service চালু রাখা।

Exam trick: Confidentiality = গোপনীয়তা, Integrity = সঠিকতা/অখণ্ডতা, Availability = ব্যবহারযোগ্যতা/প্রাপ্যতা।

## 2. Firewall কী?

Firewall হলো hardware বা software-ভিত্তিক security ব্যবস্থা, যা নির্ধারিত rules অনুযায়ী network traffic allow বা block করে।

[How the Internet Gets to Your App: A Tour Through Networking Hardware - DEV Community](https://images.openai.com/static-rsc-4/HB6bfwSKbWzUrBuAZDThQgAOwRqrPDX_yhNzg33qFAtO9pgh_v44133p2P5P-tWW4fu3G56zL9Sas59nenPaxax-NH69cBDha8XB2WGdQoS3guP4kqSuGBRZanqcco5rYPc4YS5w70dhCs91ERzqD_SMVeBqdd8Deu0piYG1pT0?purpose=inline)

[dev.to](https://dev.to/dev_avi/how-the-internet-gets-to-your-app-a-tour-through-networking-hardware-12eg)

Firewall-এর কাজ:

- অনুমোদিত ও অননুমোদিত traffic নিয়ন্ত্রণ করা।
- নির্দিষ্ট IP address, port ও protocol অনুযায়ী traffic filter করা।
- Network-এ প্রবেশ ও বের হওয়ার traffic-এর ওপর policy প্রয়োগ করা।
- কিছু firewall-এ application-aware inspection ও intrusion prevention সুবিধা থাকে।

### Firewall-এর ধরন

| ধরন                        | প্রধান বৈশিষ্ট্য                                                      |
| -------------------------- | --------------------------------------------------------------------- |
| Packet-filtering firewall  | IP, port ও protocol দেখে packet filter করে                            |
| Stateful firewall          | Connection-এর state অনুসরণ করে                                        |
| Proxy/Application firewall | Application-level traffic inspect করতে পারে                           |
| NGFW                       | Traditional firewall-এর সঙ্গে advanced inspection ও security features |

মনে রাখবে: Firewall থাকলেই সব ধরনের attack বন্ধ হবে না। ভুল configuration, compromised account বা অনুমোদিত traffic-এর ভেতরে থাকা malicious activity-ও ঝুঁকি তৈরি করতে পারে।

## 3. VPN — Virtual Private Network

VPN হলো এমন একটি প্রযুক্তি, যা public network-এর ওপর encrypted tunnel তৈরি করে network traffic-কে সুরক্ষিতভাবে বহন করতে পারে।

Remote Employee

Laptop / Mobile

Encrypted VPN Tunnel

Public Internet-এর মধ্য দিয়ে

Company Network

Private resources

### VPN-এর ব্যবহার

- দূর থেকে অফিসের private network-এ নিরাপদ প্রবেশ।
- Public Wi-Fi-তে traffic সুরক্ষায় সহায়তা।
- দুইটি office network-এর মধ্যে secure connection তৈরি।
- Remote employee-কে internal system ব্যবহারের সুযোগ দেওয়া।

### VPN-এর ধরন

- Remote-access VPN: একজন ব্যবহারকারী দূর থেকে private network-এ যুক্ত হন।
- Site-to-site VPN: দুটি বা তার বেশি network-এর মধ্যে secure tunnel তৈরি হয়।

পরীক্ষার প্রশ্ন: VPN-এর পূর্ণরূপ কী? — Virtual Private Network।

## 4. Encryption, Hashing ও Digital Signature

এই তিনটি বিষয় এক নয়।

| বিষয়              | কী করে?                                                                 | উদাহরণ / ব্যবহার                              |
| ----------------- | ----------------------------------------------------------------------- | --------------------------------------------- |
| Encryption        | তথ্যকে key ব্যবহার করে এমন রূপে রূপান্তর করে, যা সঠিক key ছাড়া পড়া কঠিন | HTTPS, encrypted data                         |
| Hashing           | Input থেকে নির্দিষ্ট দৈর্ঘ্যের digest তৈরি করে                          | Password verification, integrity checking     |
| Digital Signature | Private key দিয়ে signature তৈরি করে; public key দিয়ে যাচাই করা যায়      | Sender authenticity ও message integrity যাচাই |

### Symmetric বনাম Asymmetric Encryption

[Surviving a cyber security job interview (Cryptography) - JDriven Blog](https://images.openai.com/static-rsc-4/tbkk9fuzRkjR3NbHadrshAQz2kT2LyIdKZiZa2qRMMhIBDqukhcnlzYw9MkANVbuUYt8NiHKUnTD9sMJjfjf8E6vrs2U4Fwk2pkoDMjgZJo5LepygAle_2m0g4pyZUWIVznqYnLwtQPezhfbMmdqIRiKLHo043Wor06d1LGjp4A?purpose=inline)

Symmetric Encryption

একই secret key দিয়ে encryption ও decryption করা হয়।

উদাহরণ: AES।

সুবিধা: সাধারণত দ্রুত এবং বড় পরিমাণ data encryption-এর জন্য উপযোগী।

[File:Public key encryption.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/E0ZF21Ja5wAl7Ux-k9AzrGd-eDPDeDBt0KzzIeO0yyerEFn5tE_dGGBMKD40Fdr1Qex6AagYUblkrae43doYJEPYhB3C3MFrUjb8zMmQjgkc5Uvk8LrjehgDhpsAtFUF8pdGmkQEMWiRvyWow7swGugcrLQmLwyAUtjMN6L5EG4?purpose=inline)

Asymmetric Cryptography

Public key ও private key-এর একটি জোড়া ব্যবহার করা হয়।

উদাহরণ: RSA, elliptic-curve cryptography।

ব্যবহার: Key establishment, encryption-এর নির্দিষ্ট ব্যবহার এবং digital signature।

মনে রাখবে:

- AES → Symmetric encryption।
- RSA → Asymmetric cryptography।
- Hashing সাধারণত encryption নয়; hash থেকে সরাসরি original input ফেরত পাওয়ার জন্য decryption key থাকে না।
- Password নিরাপদে রাখতে salt-সহ Argon2, scrypt, bcrypt-এর মতো password-hashing algorithm ব্যবহার করা হয়।
- Digital signature-এ sender-এর private key দিয়ে signature তৈরি হয় এবং সংশ্লিষ্ট public key দিয়ে যাচাই করা হয়।

## 5. Authentication, Authorization ও MFA

এই তিনটি term technical exam-এ খুব গুরুত্বপূর্ণ।

- Authentication: তুমি কে, তা যাচাই করা।
- Authorization: যাচাই করা ব্যবহারকারী কী করতে পারবেন, তা নির্ধারণ করা।
- Accounting/Auditing: কে কখন কী কাজ করেছেন, তার record রাখা।

উদাহরণ: একজন employee login করলে authentication হয়। তিনি শুধু নিজের department-এর file দেখতে পারবেন কি না, সেটি authorization-এর বিষয়।

### Authentication factor

| Factor             | উদাহরণ                             |
| ------------------ | ---------------------------------- |
| Something you know | Password, PIN                      |
| Something you have | Security key, authenticator device |
| Something you are  | Fingerprint, face recognition      |

MFA (Multi-Factor Authentication)-এ একাধিক ভিন্ন ধরনের authentication factor ব্যবহার করা হয়। শুধু দুটি password ব্যবহার করলেই সাধারণত MFA হয় না, কারণ দুটিই knowledge factor।

## 6. Common Network Attacks

নিচে পরিচিত cyberattack-এর নাম ও বৈশিষ্ট্য দেওয়া হলো।

| Attack                   | কী ঘটে?                                                               | প্রতিরোধের মূল ধারণা                      |
| ------------------------ | --------------------------------------------------------------------- | ----------------------------------------- |
| Phishing                 | ভুয়া message বা website দিয়ে তথ্য হাতিয়ে নেওয়ার চেষ্টা                | URL যাচাই, phishing-resistant MFA         |
| Malware                  | ক্ষতিকর software system-এ কাজ করে                                     | Updates, endpoint protection              |
| Ransomware               | Data encrypt করে মুক্তিপণ দাবি করতে পারে                              | Offline/immutable backup, patching        |
| DoS                      | একটি service-কে অতিরিক্ত request বা traffic দিয়ে অপ্রাপ্য করার চেষ্টা | Filtering, rate limiting                  |
| DDoS                     | বহু source থেকে distributed attack                                    | DDoS mitigation, upstream filtering       |
| Man-in-the-Middle (MitM) | যোগাযোগের মাঝখানে attacker traffic intercept বা পরিবর্তনের চেষ্টা করে | TLS/HTTPS, certificate validation         |
| Brute-force attack       | বারবার সম্ভাব্য password চেষ্টা করা                                   | Rate limiting, MFA, strong authentication |
| Spoofing                 | পরিচয় বা source information ভুয়া দেখানো                               | Authentication, filtering, validation     |
| SQL Injection            | অনিরাপদ database query-তে malicious input প্রবেশ করানো                | Parameterized queries, input handling     |
| Insider threat           | প্রতিষ্ঠানের ভেতরের কারও মাধ্যমে security risk তৈরি হয়                | Least privilege, logging, access review   |

### DoS বনাম DDoS

- DoS: সাধারণ ধারণায় একটি source থেকে service-কে অপ্রাপ্য করার আক্রমণ।
- DDoS: বহু distributed source থেকে আক্রমণ।

DDoS-এর ক্ষেত্রে traffic-এর উৎস অনেক জায়গায় ছড়িয়ে থাকতে পারে, তাই mitigation কঠিন হতে পারে।

### HTTPS কীভাবে সাহায্য করে?

HTTPS হলো HTTP-এর সঙ্গে TLS security ব্যবহার করার ব্যবস্থা। এটি browser ও server-এর মধ্যে চলাচলকারী data-র confidentiality ও integrity রক্ষায় সহায়তা করে এবং certificate validation-এর মাধ্যমে server authentication দেয়।

তবে HTTPS ব্যবহার করলেই website যে সৎ বা নিরাপদ, তা নিশ্চিত হয় না।

## 7. Teletalk Technical Exam — MCQ Practice

নিজে উত্তর দাও, তারপর Check Answers চাপ দিয়ে score ও ব্যাখ্যা দেখো।

## Lesson 12 Test

0/12 answered

1\. Cybersecurity-এর CIA Triad-এ C-এর অর্থ কী?

A. Control

B. Confidentiality

C. Connectivity

D. Certification

2\. তথ্যের unauthorized পরিবর্তন ঠেকানোর সঙ্গে CIA Triad-এর কোন অংশটি সম্পর্কিত?

A. Availability

B. Confidentiality

C. Integrity

D. Routing

3\. Firewall-এর প্রধান কাজ কী?

A. সব data encrypt করা

B. Rules অনুযায়ী network traffic নিয়ন্ত্রণ করা

C. সব password তৈরি করা

D. IP address-কে domain name-এ রূপান্তর করা

4\. VPN-এর পূর্ণরূপ কী?

A. Virtual Private Network

B. Verified Public Network

C. Variable Protocol Node

D. Virtual Packet Number

5\. কোনটি symmetric encryption algorithm?

A. RSA

B. AES

C. SHA-256

D. DNS

6\. Hashing-এর সাধারণ বৈশিষ্ট্য কোনটি?

A. সবসময় original data ফেরত দেয়

B. সঠিক key দিয়ে decrypt করতেই হয়

C. একটি digest তৈরি করে; সাধারণত সরাসরি reverse করা যায় না

D. শুধু network routing করে

7\. Digital signature তৈরি করতে সাধারণত কোন key ব্যবহার করা হয়?

A. Sender-এর private key

B. Receiver-এর password

C. DNS server key

D. শুধু MAC address

8\. ব্যবহারকারী কে, তা যাচাই করার প্রক্রিয়া কোনটি?

A. Authorization

B. Authentication

C. Accounting

D. Compression

9\. কোনটি Multi-Factor Authentication-এর সঠিক উদাহরণ?

A. দুটি password

B. Password এবং authenticator app-এর code

C. একই password দুইবার

D. দুটি username

10\. বহু distributed source থেকে service-কে অপ্রাপ্য করার আক্রমণ কোনটি?

A. DDoS

B. DNS lookup

C. Backup

D. VLAN

11\. SQL Injection প্রতিরোধের গুরুত্বপূর্ণ পদ্ধতি কোনটি?

A. সব user-কে admin করা

B. Parameterized queries ব্যবহার করা

C. Database password public করা

D. Firewall বন্ধ করা

12\. HTTPS-এ browser-server যোগাযোগ সুরক্ষায় কোন protocol ব্যবহৃত হয়?

A. FTP

B. TLS

C. ARP

D. DHCP

Check Answers

## শেষ মুহূর্তের Revision

- CIA: Confidentiality, Integrity, Availability।
- Firewall: Traffic filtering ও access control।
- VPN: Virtual Private Network।
- AES: Symmetric encryption।
- RSA: Asymmetric cryptography।
- Hashing: Data digest তৈরি; encryption-এর সমান নয়।
- Authentication: পরিচয় যাচাই।
- Authorization: অনুমতি নির্ধারণ।
- MFA: একাধিক ভিন্ন authentication factor।
- DDoS: বহু source থেকে denial-of-service attack।
- SQL Injection: Parameterized queries দিয়ে ঝুঁকি কমানো যায়।
- HTTPS: HTTP over TLS।

পরবর্তী লেসন: Lesson 13 — Linux Commands, Server Administration, DNS, DHCP, SSH, Logs ও Basic Server Troubleshooting। এটি Teletalk-এর IT/networking technical preparation-এর জন্যও কাজে লাগবে।

# Teletalk Technical Exam Preparation — Lesson 13

## Linux Commands, Server Administration, DNS, DHCP, SSH, Logs ও Troubleshooting

এই লেসনে Linux ও server administration-এর প্রয়োজনীয় বিষয়গুলো শিখব। বিশেষ করে command-এর কাজ, পূর্ণরূপ, পার্থক্য এবং বাস্তব server troubleshooting-এর ওপর গুরুত্ব দেব।

## 1. Linux কী?

Linux হলো একটি open-source operating system kernel। Linux kernel-এর ওপর ভিত্তি করে Ubuntu, Debian, Fedora ও Rocky Linux-এর মতো operating system তৈরি হয়েছে।

Server-এ Linux ব্যাপকভাবে ব্যবহৃত হয়, কারণ এটি automation, networking, security ও server management-এর জন্য শক্তিশালী tools দেয়।

### Linux directory structure

| Directory  | সাধারণ ব্যবহার                                |
| ---------- | --------------------------------------------- |
| `/`        | Root directory; পুরো filesystem-এর শীর্ষ      |
| `/home`    | সাধারণ ব্যবহারকারীদের home directory          |
| `/root`    | Root user-এর home directory                   |
| `/etc`     | System ও application configuration            |
| `/var`     | পরিবর্তনশীল data, logs, cache ইত্যাদি         |
| `/var/log` | System ও application log files                |
| `/tmp`     | Temporary files                               |
| `/usr/bin` | অনেক user-level executable program            |
| `/dev`     | Device files                                  |
| `/proc`    | Kernel ও process সম্পর্কিত virtual filesystem |
| `/boot`    | Boot করার জন্য প্রয়োজনীয় files                |

Exam tip: `/etc` = configuration, `/var/log` = logs, `/home` = users' home directories।

## 2. গুরুত্বপূর্ণ Linux Commands

### File ও Directory Management

| Command          | কাজ                                   |
| ---------------- | ------------------------------------- |
| `pwd`            | বর্তমান directory দেখায়               |
| `ls`             | Files ও directories দেখায়             |
| `cd /etc`        | Directory পরিবর্তন করে                |
| `mkdir test`     | Directory তৈরি করে                    |
| `touch file.txt` | File তৈরি করে বা timestamp update করে |
| `cp a.txt b.txt` | File copy করে                         |
| `mv a.txt b.txt` | File move বা rename করে               |
| `rm file.txt`    | File মুছে দেয়                         |
| `cat file.txt`   | File-এর content দেখায়                 |
| `less file.txt`  | বড় file page ধরে পড়তে সাহায্য করে     |

### System Monitoring

| Command           | কাজ                                     |
| ----------------- | --------------------------------------- |
| `whoami`          | বর্তমান user দেখায়                      |
| `uname -a`        | Kernel/system information দেখায়         |
| `uptime`          | System কতক্ষণ চলছে ও load average দেখায় |
| `free -h`         | Memory usage দেখায়                      |
| `df -h`           | Filesystem disk space দেখায়             |
| `du -sh /var/log` | নির্দিষ্ট directory-এর মোট space দেখায়  |
| `top`             | Process ও resource usage দেখায়          |
| `ps aux`          | Process list দেখায়                      |

### Networking ও Troubleshooting

| Command                       | কাজ                                  |
| ----------------------------- | ------------------------------------ |
| `ip addr`                     | Network interface ও IP address দেখায় |
| `ip route`                    | Routing table দেখায়                  |
| `ping 8.8.8.8`                | IP connectivity পরীক্ষা করে          |
| `ss -tuln`                    | Listening TCP/UDP ports দেখায়        |
| `curl -I https://example.com` | HTTP response headers পরীক্ষা করে    |
| `dig example.com`             | DNS query করে                        |
| `traceroute 8.8.8.8`          | Network path trace করে               |

### গুরুত্বপূর্ণ পার্থক্য

- `df -h` → Filesystem-এ কত space আছে।
- `du -sh folder` → নির্দিষ্ট folder কত space ব্যবহার করছে।
- `free -h` → RAM ও swap usage।
- `top` → চলমান process ও system resource usage।
- `ps aux` → Process-এর snapshot বা তালিকা।

সতর্কতা: `rm` দিয়ে file মুছে ফেললে তা সহজে ফেরত পাওয়া নাও যেতে পারে। Server-এ কোনো command চালানোর আগে সেটি কী করবে নিশ্চিত হও।

## 3. Linux Permissions ও User Management

Linux-এ file ও directory-এর access সাধারণত তিনটি শ্রেণিতে নিয়ন্ত্রণ করা হয়:

- User (u): File-এর owner।
- Group (g): নির্দিষ্ট group-এর সদস্য।
- Others (o): অন্য ব্যবহারকারীরা।

তিন ধরনের permission:

| Permission    | অর্থ                                         | Numeric value |
| ------------- | -------------------------------------------- | ------------- |
| Read (`r`)    | পড়ার অনুমতি                                  | 4             |
| Write (`w`)   | পরিবর্তন/লেখার অনুমতি                        | 2             |
| Execute (`x`) | চালানোর অনুমতি; directory-তে প্রবেশের অনুমতি | 1             |

### `chmod 755` মানে কী?

- Owner: `7 = 4+2+1` → `rwx`
- Group: `5 = 4+1` → `r-x`
- Others: `5 = 4+1` → `r-x`

অর্থাৎ permission হলো `rwxr-xr-x`।

আরও কিছু গুরুত্বপূর্ণ command:

| Command               | কাজ                                              |
| --------------------- | ------------------------------------------------ |
| `chmod 644 file.txt`  | Owner read/write; অন্যরা read                    |
| `chmod 600 file.txt`  | Owner read/write; অন্যদের access নেই             |
| `chown user file.txt` | File owner পরিবর্তন                              |
| `id`                  | User ও group ID দেখায়                            |
| `sudo command`        | অনুমোদন থাকলে elevated privilege-এ command চালায় |
| `who`                 | বর্তমানে login করা user-দের তথ্য দেখায়           |

Exam tip: `chmod 777`-এ owner, group ও others—সবাই read, write ও execute permission পায়। অপ্রয়োজনে production server-এ এ ধরনের permission দেওয়া নিরাপদ নয়।

## 4. Process ও Service Management

Server-এ web server, database, SSH এবং অন্যান্য application সাধারণত process ও service হিসেবে চলে।

Ubuntu-তে `systemd` service পরিচালনায় বহুল ব্যবহৃত হয়।

| Command                        | কাজ                                           |
| ------------------------------ | --------------------------------------------- |
| `systemctl status nginx`       | Nginx service-এর status                       |
| `sudo systemctl start nginx`   | Service চালু করা                              |
| `sudo systemctl stop nginx`    | Service বন্ধ করা                              |
| `sudo systemctl restart nginx` | Service restart করা                           |
| `sudo systemctl enable nginx`  | Boot-এর সময় স্বয়ংক্রিয়ভাবে চালু করার ব্যবস্থা |
| `sudo systemctl disable nginx` | Boot-এ automatic start বন্ধ করা               |
| `journalctl -u nginx`          | Nginx service-এর journal logs                 |
| `journalctl -u nginx -f`       | নতুন log entry অনুসরণ করা                     |

### `restart` বনাম `reload`

- Restart: Service বন্ধ করে আবার চালু করে; সংযোগে interruption হতে পারে।
- Reload: সমর্থিত service-এর configuration পুনরায় load করে; অনেক ক্ষেত্রে সম্পূর্ণ restart প্রয়োজন হয় না।

প্রতিটি service `reload` সমর্থন করে না। পরিবর্তনের আগে configuration test করা ভালো।

## 5. DNS ও DHCP

### DNS — Domain Name System

DNS domain name-কে IP address-এর সঙ্গে resolve করতে সাহায্য করে।

উদাহরণ: `example.com`-এর জন্য DNS query করলে সংশ্লিষ্ট record-এ IP address পাওয়া যেতে পারে।

প্রধান DNS record:

| Record  | কাজ                                          |
| ------- | -------------------------------------------- |
| `A`     | IPv4 address                                 |
| `AAAA`  | IPv6 address                                 |
| `CNAME` | অন্য hostname-এর alias                       |
| `MX`    | Mail server নির্ধারণ                         |
| `NS`    | Authoritative name server নির্দেশ            |
| `TXT`   | Text-based তথ্য; SPF-সহ বিভিন্ন কাজে ব্যবহৃত |

DNS সাধারণত port 53 ব্যবহার করে; query সাধারণত UDP-তে হয়, আর প্রয়োজন অনুযায়ী TCP-ও ব্যবহৃত হয়।

### DHCP — Dynamic Host Configuration Protocol

DHCP network device-কে স্বয়ংক্রিয়ভাবে IP configuration দিতে পারে, যেমন IP address, subnet mask, default gateway ও DNS server।

DHCP-এর চারটি ধাপ মনে রাখো: DORA।

### D

### Discover

Client DHCP server খোঁজে

### O

### Offer

Server configuration প্রস্তাব করে

### R

### Request

Client প্রস্তাবিত configuration চায়

### A

### Acknowledge

Server lease নিশ্চিত করে

Exam facts:

- DHCP server port: UDP 67।
- DHCP client port: UDP 68।
- DNS: Port 53।
- SSH: TCP port 22।
- HTTP: TCP port 80।
- HTTPS: TCP port 443।

## 6. SSH ও Remote Server Access

SSH (Secure Shell) হলো remote system-এ encrypted connection-এর মাধ্যমে command চালানোর protocol।

উদাহরণ:

```
ssh username@192.168.1.20
```

এখানে `username` হলো remote server-এর user এবং `192.168.1.20` হলো server-এর IP address।

SSH-তে সাধারণত password অথবা public-key authentication ব্যবহার করা যায়। Public-key authentication-এ private key নিরাপদে নিজের কাছে রাখতে হয়।

গুরুত্বপূর্ণ command:

```
ssh user@server_ip
scp file.txt user@server_ip:/home/user/
```

- `ssh` → Remote login/command execution।
- `scp` → SSH-ভিত্তিক file copy।
- `sftp` → SSH-ভিত্তিক file transfer protocol।

Production server-এ strong authentication, প্রয়োজনীয় account-এ সীমিত access এবং নিয়মিত security updates গুরুত্বপূর্ণ।

## 7. Server Logs ও Troubleshooting

Server-এ সমস্যা হলে logs দেখে কারণ খুঁজে বের করা হয়।

| সমস্যা                           | কী পরীক্ষা করবে             |
| -------------------------------- | --------------------------- |
| Server-এর disk full              | `df -h`                     |
| কোনো directory বেশি space নিচ্ছে | `du -sh /path/to/folder`    |
| Nginx চালু হচ্ছে না              | `systemctl status nginx`    |
| Nginx error                      | `journalctl -u nginx -n 50` |
| কোন port listening করছে          | `ss -tuln`                  |
| DNS resolve হচ্ছে না             | `dig example.com`           |
| IP connectivity সমস্যা           | `ping 8.8.8.8`              |
| RAM usage বেশি                   | `free -h`, `top`            |

### বাস্তব উদাহরণ

ধরো, একটি Django API server কাজ করছে না।

1. `systemctl status nginx` দিয়ে Nginx-এর অবস্থা দেখো।
2. `journalctl -u nginx -n 50` দিয়ে সাম্প্রতিক log দেখো।
3. `ss -tuln` দিয়ে প্রয়োজনীয় port listening করছে কি না দেখো।
4. `curl -I http://127.0.0.1` দিয়ে local HTTP response পরীক্ষা করো।
5. Application ও database-এর logs আলাদাভাবে পরীক্ষা করো।

একটি গুরুত্বপূর্ণ বিষয়: Nginx চালু থাকলেই Django application ঠিক আছে—এমন নয়। Nginx, application server, Django application ও database—প্রতিটি স্তরে সমস্যা হতে পারে।

## 8. Teletalk Technical Exam — MCQ Practice

নিচের 15টি প্রশ্নের উত্তর দাও। শেষে Check Answers চাপলে score ও ব্যাখ্যা দেখতে পাবে।

## Lesson 13 Test

0/15 answered

1\. Linux-এ বর্তমান working directory দেখার command কোনটি?

A. ls

B. pwd

C. cd

D. whoami

2\. Linux-এ system configuration file সাধারণত কোন directory-তে থাকে?

A. /etc

B. /home

C. /tmp

D. /dev

3\. কোন command filesystem-এর disk space দেখায়?

A. free -h

B. df -h

C. ps aux

D. uptime

4\. কোন command RAM ও swap usage দেখায়?

A. du -sh

B. ip route

C. free -h

D. chmod

5\. chmod 755-এর owner permission কী?

A. r--

B. rw-

C. r-x

D. rwx

6\. Linux-এ service-এর status দেখার command কোনটি?

A. systemctl status

B. mkdir status

C. chmod status

D. ping status

7\. DNS-এর পূর্ণরূপ কী?

A. Dynamic Network Service

B. Domain Name System

C. Data Naming Service

D. Domain Node Security

8\. IPv4 address-এর জন্য কোন DNS record ব্যবহৃত হয়?

A. MX

B. AAAA

C. A

D. CNAME

9\. DHCP-এর DORA sequence কোনটি?

A. Discover, Offer, Request, Acknowledge

B. Domain, Open, Route, Access

C. Discover, Order, Resolve, Authenticate

D. Data, Offer, Relay, Assign

10\. DHCP server-এর প্রচলিত UDP port কোনটি?

A. 53

B. 22

C. 68

D. 67

11\. SSH-এর default TCP port কোনটি?

A. 21

B. 22

C. 25

D. 443

12\. HTTPS-এর default port কোনটি?

A. 80

B. 53

C. 443

D. 110

13\. Linux-এ listening TCP/UDP port দেখার command কোনটি?

A. ss -tuln

B. pwd

C. free -h

D. touch

14\. Nginx service-এর সাম্প্রতিক journal log দেখতে কোন command উপযুক্ত?

A. journalctl -u nginx -n 50

B. mkdir nginx

C. df -h nginx

D. chmod nginx

15\. Remote server-এ encrypted command-line access-এর জন্য কোন protocol ব্যবহৃত হয়?

A. HTTP

B. FTP

C. SSH

D. DHCP

Check Answers

## Final Revision Sheet

- `/etc` → Configuration।
- `/var/log` → Logs।
- `df -h` → Disk space।
- `free -h` → RAM/swap।
- `systemctl` → Service management।
- `journalctl` → Systemd journal logs।
- DNS → UDP/TCP 53।
- DHCP server/client → UDP 67/68।
- SSH → TCP 22।
- HTTP/HTTPS → TCP 80/443।
- `chmod 755` → Owner `rwx`, group ও others `r-x`।
- DORA → Discover, Offer, Request, Acknowledge।

পরবর্তী লেসন 14: Database, SQL, DBMS, Normalization, Primary Key, Foreign Key, JOIN, Index ও Transaction—technical exam-এর জন্য গুরুত্বপূর্ণ বিষয়।

# Teletalk Technical Exam Preparation — লেসন ১৪

## DBMS, SQL, Normalization, JOIN, Index ও Transaction

এই লেসনে Database ও DBMS-এর গুরুত্বপূর্ণ ধারণাগুলো শিখব। প্রতিটি বিষয়ের সংজ্ঞা, বাস্তব উদাহরণ, গুরুত্বপূর্ণ SQL command এবং পরীক্ষার উপযোগী MCQ থাকবে।

## ১. Database ও DBMS কী?

Database: সংগঠিতভাবে সংরক্ষিত সম্পর্কিত তথ্যের সংগ্রহ।

DBMS (Database Management System): Database তৈরি, সংরক্ষণ, অনুসন্ধান, পরিবর্তন ও নিয়ন্ত্রণ করার software।

উদাহরণ হিসেবে একটি টেলিকম প্রতিষ্ঠানের database-এ customer, SIM, call record, recharge ও payment-এর তথ্য থাকতে পারে।

Application

Customer / Billing / Recharge System

DBMS

PostgreSQL, MySQL, Oracle Database

Database

Customer records, SIM records, transactions

### DBMS-এর সুবিধা

- Data redundancy কমাতে সাহায্য করে।
- Data consistency বজায় রাখতে সাহায্য করে।
- Access control ও security দেয়।
- Backup ও recovery সুবিধা দেয়।
- একাধিক ব্যবহারকারীর concurrent access পরিচালনা করতে পারে।

### DBMS-এর ধরন

| ধরন                     | উদাহরণ                    |
| ----------------------- | ------------------------- |
| Relational DBMS (RDBMS) | PostgreSQL, MySQL, Oracle |
| Document database       | MongoDB                   |
| Key-value database      | Redis                     |
| Graph database          | Neo4j                     |

মনে রাখবে: SQL হলো relational database-এর সঙ্গে বহুল ব্যবহৃত query language; SQL নিজে DBMS নয়।

## ২. Table, Row, Column, Schema ও Instance

ধরো, `Customer` নামে একটি table আছে:

| customer_id | name  | phone       |
| ----------- | ----- | ----------- |
| 101         | Rahim | 017XXXXXXXX |
| 102         | Karim | 018XXXXXXXX |
| 103         | Salma | 019XXXXXXXX |

- Table: সম্পর্কিত data-এর কাঠামোবদ্ধ সংগ্রহ।
- Row / Record / Tuple: একটি সম্পূর্ণ entry; যেমন Rahim-এর record।
- Column / Field / Attribute: একটি নির্দিষ্ট বৈশিষ্ট্য; যেমন `name`।
- Schema: Table, column, data type, constraint ও relationship-এর সংজ্ঞা।
- Database instance: নির্দিষ্ট সময়ে database-এ থাকা actual data।

Exam tip: `name` হলো column; `Rahim` হলো column-এর value; পুরো Rahim-এর entry হলো row বা record।

## ৩. Primary Key, Foreign Key ও Constraints

### Primary Key (PK)

একটি table-এর প্রতিটি row-কে uniquely identify করে।

উদাহরণ: `customer_id`।

- Duplicate value থাকতে পারে না।
- `NULL` হতে পারে না।
- একটি table-এর primary key একটি column অথবা একাধিক column নিয়ে গঠিত হতে পারে।

### Foreign Key (FK)

একটি table-এর column যখন অন্য table-এর primary key বা unique key-কে reference করে, তখন সেটি foreign key হতে পারে।

উদাহরণ:

Customer table

| customer_id (PK) | name  |
| ---------------- | ----- |
| 101              | Rahim |
| 102              | Karim |

Recharge table

| recharge_id (PK) | customer_id (FK) | amount |
| ---------------- | ---------------- | ------ |
| 1                | 101              | 100    |
| 2                | 101              | 200    |
| 3                | 102              | 50     |

Recharge table-এর customer_id, Customer table-এর customer_id-কে reference করে।

### অন্যান্য গুরুত্বপূর্ণ constraints

| Constraint    | কাজ                                            |
| ------------- | ---------------------------------------------- |
| `NOT NULL`    | `NULL` value নিষিদ্ধ করে                       |
| `UNIQUE`      | Duplicate value নিষিদ্ধ করে                    |
| `CHECK`       | নির্দিষ্ট শর্ত যাচাই করে                       |
| `DEFAULT`     | Value না দিলে default value ব্যবহার করে        |
| `PRIMARY KEY` | Unique ও non-null পরিচয় নির্ধারণ করে           |
| `FOREIGN KEY` | Table-এর মধ্যে referential integrity বজায় রাখে |

## ৪. SQL Command — DDL, DML, DQL, DCL ও TCL

SQL command-এর শ্রেণিবিভাগ পরীক্ষায় প্রায়ই জিজ্ঞাসা করা হয়।

| Category | পূর্ণরূপ                     | Command-এর উদাহরণ                     |
| -------- | ---------------------------- | ------------------------------------- |
| DDL      | Data Definition Language     | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| DML      | Data Manipulation Language   | `INSERT`, `UPDATE`, `DELETE`          |
| DQL      | Data Query Language          | `SELECT`                              |
| DCL      | Data Control Language        | `GRANT`, `REVOKE`                     |
| TCL      | Transaction Control Language | `COMMIT`, `ROLLBACK`, `SAVEPOINT`     |

কিছু বইয়ে `SELECT`-কে DML-এর অন্তর্ভুক্তও দেখানো হয়। পরীক্ষায় তোমার syllabus বা প্রশ্নের convention অনুসরণ করবে।

### SQL-এর বাস্তব উদাহরণ

```
CREATE TABLE Customer (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(20) UNIQUE
);
```

Data insert:

```
INSERT INTO Customer (customer_id, name, phone)
VALUES (101, 'Rahim', '017XXXXXXXX');
```

Data read:

```
SELECT * FROM Customer;
```

শুধু নির্দিষ্ট column:

```
SELECT name, phone
FROM Customer
WHERE customer_id = 101;
```

Data update:

```
UPDATE Customer
SET name = 'Rahim Uddin'
WHERE customer_id = 101;
```

Data delete:

```
DELETE FROM Customer
WHERE customer_id = 101;
```

সতর্কতা: `UPDATE` বা `DELETE`-এ `WHERE` না দিলে অনেক ক্ষেত্রে table-এর সব row পরিবর্তিত বা মুছে যেতে পারে।

### DELETE বনাম TRUNCATE বনাম DROP

| Command    | কাজ                                     |
| ---------- | --------------------------------------- |
| `DELETE`   | Row মুছে দেয়; `WHERE` ব্যবহার করা যায়   |
| `TRUNCATE` | সাধারণত table-এর সব row দ্রুত সরিয়ে দেয় |
| `DROP`     | Table-এর database object-টিই সরিয়ে দেয়  |

এগুলোর rollback, trigger ও identity-reset আচরণ DBMS এবং transaction context অনুযায়ী আলাদা হতে পারে।

## ৫. SQL JOIN

JOIN ব্যবহার করে একাধিক table-এর সম্পর্কিত data একসঙ্গে query করা হয়।

ধরো, `Customer` ও `Recharge` table আগের মতোই আছে।

### INNER JOIN

যেসব customer-এর recharge record আছে, শুধু তাদের matching record দেখায়।

```
SELECT c.name, r.amount
FROM Customer c
INNER JOIN Recharge r
    ON c.customer_id = r.customer_id;
```

### LEFT JOIN

বাম পাশের table-এর সব row দেখায়। ডান পাশের table-এ match না থাকলে ডান পাশের column-গুলোতে `NULL` আসে।

```
SELECT c.name, r.amount
FROM Customer c
LEFT JOIN Recharge r
    ON c.customer_id = r.customer_id;
```

### JOIN-এর পার্থক্য

| JOIN              | ফলাফল                                        |
| ----------------- | -------------------------------------------- |
| `INNER JOIN`      | দুই table-এ matching row                     |
| `LEFT JOIN`       | Left table-এর সব row এবং matching right rows |
| `RIGHT JOIN`      | Right table-এর সব row এবং matching left rows |
| `FULL OUTER JOIN` | দুই table-এর matching ও non-matching row     |

মনে রাখবে: সব DBMS একই JOIN syntax বা feature সমানভাবে সমর্থন করে না। PostgreSQL `FULL OUTER JOIN` সমর্থন করে; MySQL-এ এর সরাসরি built-in `FULL OUTER JOIN` syntax নেই।

## ৬. Normalization

Normalization হলো relational database-এর table-গুলো এমনভাবে সাজানোর প্রক্রিয়া, যাতে অপ্রয়োজনীয় data duplication ও data anomaly কমে।

ধরো, একটি table-এ customer-এর নাম ও প্রতিটি recharge-এর amount বারবার রাখা হচ্ছে। Customer-এর নাম বদলালে অনেক row update করতে হতে পারে। Customer ও Recharge আলাদা table করলে এই duplication কমানো যায়।

### Normal Forms

### 1NF — First Normal Form

প্রতিটি field-এ একটি করে atomic value থাকবে; একটি cell-এ একাধিক পৃথক value রাখবে না।

উদাহরণ: `phone1, phone2`-এর তালিকা এক cell-এ রাখার বদলে উপযুক্ত পৃথক row বা table design করা।

### 2NF — Second Normal Form

Table 1NF-এ থাকবে এবং প্রতিটি non-prime attribute পুরো candidate key-এর ওপর নির্ভর করবে; composite key-এর অংশবিশেষের ওপর partial dependency থাকবে না।

### 3NF — Third Normal Form

Table 2NF-এ থাকবে এবং non-key attribute-এর মধ্যে অনুপযুক্ত transitive dependency থাকবে না।

### BCNF — Boyce–Codd Normal Form

প্রতিটি non-trivial functional dependency \\(X \rightarrow Y\\)-এর ক্ষেত্রে \\(X\\) একটি superkey হবে।

পরীক্ষার জন্য মূল কথা:

- 1NF → Atomic values।
- 2NF → Partial dependency দূর করা।
- 3NF → Transitive dependency দূর করা।
- BCNF → প্রতিটি determinant superkey।

## ৭. Database Index

Index হলো এমন একটি database structure, যা নির্দিষ্ট column-এর data দ্রুত খুঁজে পেতে সাহায্য করে।

```
CREATE INDEX idx_customer_name
ON Customer(name);
```

এখন `name` দিয়ে search অনেক ক্ষেত্রে দ্রুত হতে পারে:

```
SELECT *
FROM Customer
WHERE name = 'Rahim';
```

### Index-এর সুবিধা ও অসুবিধা

সুবিধা

- উপযুক্ত query-এর search speed বাড়াতে পারে।
- কিছু `JOIN`, `ORDER BY` ও filtering query-তে সহায়তা করতে পারে।

অসুবিধা

- অতিরিক্ত storage লাগে।
- `INSERT`, `UPDATE`, `DELETE`-এর সময় index update করতে হয়, ফলে write operation-এর overhead বাড়তে পারে।

Exam fact: Primary key তৈরি করলে সাধারণত সংশ্লিষ্ট DBMS স্বয়ংক্রিয়ভাবে unique index তৈরি করে। তবে index-এর ধরন ও আচরণ DBMS অনুযায়ী ভিন্ন হতে পারে।

## ৮. Transaction ও ACID Properties

Transaction হলো database operation-এর এমন একটি logical unit, যা সফলভাবে সম্পন্ন হবে অথবা প্রয়োজন অনুযায়ী বাতিল হবে।

টেলিকমের recharge system-এর উদাহরণ: একজন customer-এর balance থেকে 100 টাকা কমিয়ে recharge account-এ 100 টাকা যোগ করা। মাঝপথে একটি operation ব্যর্থ হলে database-এ অসামঞ্জস্য তৈরি হতে পারে।

### ACID

| Property | পূর্ণরূপ    | অর্থ                                                                        |
| -------- | ----------- | --------------------------------------------------------------------------- |
| A        | Atomicity   | সব operation হবে, নয়তো transaction ব্যর্থ হলে পুরো transaction rollback হবে |
| C        | Consistency | Transaction database-এর নির্ধারিত rules ও constraints বজায় রাখবে            |
| I        | Isolation   | Concurrent transaction একে অপরকে কীভাবে প্রভাবিত করে, তা নিয়ন্ত্রণ করে      |
| D        | Durability  | Commit সফল হলে পরিবর্তন স্থায়ী রাখার নিশ্চয়তা দেয়                           |

### SQL উদাহরণ

```
BEGIN;

UPDATE Account
SET balance = balance - 100
WHERE account_id = 1;

UPDATE Account
SET balance = balance + 100
WHERE account_id = 2;

COMMIT;
```

কোনো operation ব্যর্থ হলে উপযুক্ত error handling-এর মাধ্যমে transaction `ROLLBACK` করা যায়।

```
ROLLBACK;
```

মনে রাখবে: `COMMIT` transaction-এর পরিবর্তন নিশ্চিত করে; `ROLLBACK` transaction-এর uncommitted পরিবর্তন বাতিল করতে ব্যবহৃত হয়।

## ৯. Database-এর আরও গুরুত্বপূর্ণ Terms

- Candidate Key: যে minimal attribute set দিয়ে row uniquely identify করা যায়।
- Superkey: যে attribute set row-কে uniquely identify করে; এতে অতিরিক্ত attribute থাকতে পারে।
- Composite Key: একাধিক column নিয়ে গঠিত key।
- NULL: Value অনুপস্থিত বা অজানা বোঝাতে ব্যবহৃত marker; এটি শূন্য বা empty string-এর সমান নয়।
- View: Query-ভিত্তিক virtual table।
- Stored Procedure: Database-এ সংরক্ষিত ও চালানো যায় এমন routine।
- Trigger: নির্দিষ্ট database event-এ স্বয়ংক্রিয়ভাবে চালু হওয়া logic।
- Deadlock: একাধিক transaction পরস্পরের resource-এর জন্য অপেক্ষা করে অগ্রগতি থামিয়ে দিলে deadlock হতে পারে।

## ১০. Teletalk Technical Exam — MCQ Practice

## Lesson 14 Test

0/15 answered

1\. DBMS-এর পূর্ণরূপ কী?

A. Database Management System

B. Data Backup Management Service

C. Digital Base Memory System

D. Database Machine Software

2\. একটি table-এর প্রতিটি row uniquely identify করতে কোন key ব্যবহৃত হয়?

A. Foreign key

B. Primary key

C. Non-unique index

D. NULL key

3\. Foreign key-এর প্রধান উদ্দেশ্য কী?

A. সব column মুছে ফেলা

B. Table-এর মধ্যে referential relationship বজায় রাখা

C. সব data encrypt করা

D. Query বন্ধ করা

4\. কোন SQL command দিয়ে data retrieve করা হয়?

A. DROP

B. UPDATE

C. SELECT

D. GRANT

5\. কোনটি DDL command?

A. INSERT

B. CREATE

C. SELECT

D. COMMIT

6\. DELETE ও DROP-এর মধ্যে সঠিক পার্থক্য কোনটি?

A. দুটিই সবসময় table structure মুছে দেয়

B. DELETE row মুছে; DROP database object সরিয়ে দেয়

C. DROP শুধু একটি row মুছে

D. DELETE কখনো row মুছে না

7\. INNER JOIN কী ফেরত দেয়?

A. শুধু left table-এর সব row

B. শুধু right table-এর সব row

C. Matching row

D. কোনো matching ছাড়াই সব row

8\. Normalization-এর প্রধান লক্ষ্য কী?

A. Data duplication ও anomaly কমানো

B. সব table এক table-এ রাখা

C. সব column-কে text করা

D. Database-এর সব key মুছে ফেলা

9\. 1NF-এর গুরুত্বপূর্ণ শর্ত কোনটি?

A. প্রতিটি cell-এ atomic value

B. সব table-এ composite key

C. কোনো primary key থাকবে না

D. সব column unique হবে

10\. Database index-এর প্রধান সুবিধা কী?

A. সব query-কে সবসময় দ্রুত করা

B. উপযুক্ত search query দ্রুত করতে সাহায্য করা

C. সব backup মুছে ফেলা

D. Password তৈরি করা

11\. ACID-এর A-এর অর্থ কী?

A. Availability

B. Atomicity

C. Authentication

D. Authorization

12\. Transaction-এর পরিবর্তন নিশ্চিত করতে কোন command ব্যবহৃত হয়?

A. ROLLBACK

B. DROP

C. COMMIT

D. TRUNCATE

13\. Database-এ NULL কী বোঝায়?

A. অবশ্যই 0

B. অবশ্যই empty string

C. অনুপস্থিত বা অজানা value

D. সবসময় false

14\. একাধিক column নিয়ে গঠিত key-কে কী বলে?

A. Foreign server

B. Composite key

C. Single key

D. View key

15\. একাধিক transaction পরস্পরের resource-এর জন্য অপেক্ষা করে আটকে গেলে কী হতে পারে?

A. Normalization

B. Deadlock

C. Indexing

D. DNS resolution

Check Answers

## দ্রুত Revision Sheet

- DBMS: Database পরিচালনার software।
- Primary Key: Unique, non-null identifier।
- Foreign Key: Table-এর relationship বজায় রাখতে সাহায্য করে।
- DDL: `CREATE`, `ALTER`, `DROP`।
- DML: `INSERT`, `UPDATE`, `DELETE`।
- JOIN: একাধিক table-এর সম্পর্কিত data query করে।
- 1NF: Atomic values।
- 2NF: Partial dependency দূর করা।
- 3NF: Transitive dependency দূর করা।
- Index: Search দ্রুত করতে পারে; storage ও write overhead বাড়াতে পারে।
- ACID: Atomicity, Consistency, Isolation, Durability।
- COMMIT: Transaction নিশ্চিত করে।
- ROLLBACK: Uncommitted পরিবর্তন বাতিল করে।

পরবর্তী লেসন হবে লেসন ১৫ — Programming Fundamentals, OOP, Data Structures, Algorithms ও Big-O Complexity। Teletalk-এর technical exam-এর প্রস্তুতির জন্য এগুলোও গুরুত্বপূর্ণ।

# Teletalk Technical Exam Preparation — লেসন ১৫

## Programming Fundamentals, OOP, Data Structures, Algorithms ও Big-O Complexity

এই লেসনে Programming-এর মৌলিক ধারণা থেকে শুরু করে Object-Oriented Programming (OOP), Data Structures, Algorithms এবং Time Complexity শিখব। প্রতিটি topic-এর সঙ্গে সহজ উদাহরণ ও পরীক্ষায় কাজে লাগবে এমন তথ্য থাকবে।

## ১. Programming Fundamentals

Programming হলো computer-কে নির্দিষ্ট কাজ করানোর জন্য instruction বা নির্দেশনা লেখা।

### গুরুত্বপূর্ণ terms

| Term       | অর্থ                                                                 |
| ---------- | -------------------------------------------------------------------- |
| Algorithm  | কোনো সমস্যা সমাধানের ধাপে ধাপে পদ্ধতি                                |
| Flowchart  | চিহ্ন ব্যবহার করে algorithm-এর flow দেখানো                           |
| Pseudocode | Programming language-এর নির্দিষ্ট syntax ছাড়াই algorithm-এর ধাপ লেখা |
| Variable   | Data সংরক্ষণ করার নামযুক্ত স্থান                                     |
| Data type  | Data-এর ধরন নির্ধারণ করে                                             |
| Operator   | Calculation বা comparison করার symbol                                |
| Function   | নির্দিষ্ট কাজ করার জন্য reusable code block                          |
| Debugging  | Program-এর error খুঁজে বের করে ঠিক করা                               |

### Algorithm-এর উদাহরণ

দুটি সংখ্যার মধ্যে বড় সংখ্যা বের করা:

```
START
INPUT A, B
IF A > B
    PRINT A
ELSE IF B > A
    PRINT B
ELSE
    PRINT "Equal"
END
```

Algorithm ভাষা-নিরপেক্ষ হতে পারে। একই algorithm Python, C, C++ বা Java-তে implement করা যায়।

### Compiler বনাম Interpreter

| Compiler                                                                    | Interpreter                                                                               |
| --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| সাধারণত program-কে আগে machine code বা অন্য executable form-এ translate করে | সাধারণত program execution-এর সময় instruction বা intermediate representation interpret করে |
| উদাহরণ: C-এর প্রচলিত compilation process                                    | উদাহরণ: Python-এর সাধারণ execution model-এ interpreter ব্যবহৃত হয়                         |

পরীক্ষার জন্য: Python-কে প্রায়ই interpreted language বলা হয়; তবে CPython source code-কে bytecode-এ compile করে, তারপর virtual machine-এ execute করে। তাই বাস্তবে বিষয়টি শুধু “compiler অথবা interpreter”—এত সরল নয়।

## ২. Programming-এর Data Types ও Operators

সাধারণ data type-এর উদাহরণ:

| Data type  | Python উদাহরণ       | ব্যবহার                       |
| ---------- | ------------------- | ----------------------------- |
| Integer    | `10`                | পূর্ণসংখ্যা                   |
| Float      | `3.14`              | ভগ্নাংশসহ সংখ্যা              |
| String     | `"Teletalk"`        | Text                          |
| Boolean    | `True`, `False`     | Logical value                 |
| List       | `[10, 20, 30]`      | Ordered, mutable collection   |
| Tuple      | `(10, 20, 30)`      | Ordered, immutable collection |
| Dictionary | `{"name": "Rahim"}` | Key-value collection          |
| Set        | `{10, 20, 30}`      | Unique elements-এর collection |

### Operators

```
a = 10b = 3print(a + b)   # 13print(a // b)  # 3print(a % b)   # 1print(a ** b)  # 1000print(a > b)   # True
```

- `+` → যোগ
- `-` → বিয়োগ
- `*` → গুণ
- `/` → Division; Python-এ সাধারণত float result
- `//` → Floor division
- `%` → Remainder বা ভাগশেষ
- `**` → Power
- `==` → সমান কি না
- `!=` → সমান নয় কি না
- `and`, `or`, `not` → Logical operators

Exam trap: `=` হলো assignment operator; `==` হলো equality comparison operator।

## ৩. Control Flow — Condition ও Loop

Program-এ কোন code চলবে এবং কতবার চলবে, তা control flow নির্ধারণ করে।

### Conditional statement

```
marks = 75if marks >= 80:    print("A+")elif marks >= 70:    print("A")else:    print("Need improvement")
```

এখানে output হবে `A`।

### Loop

```
for i in range(1, 6):    print(i)
```

Output: `1, 2, 3, 4, 5`।

`while` loop-এর উদাহরণ:

```
count = 1while count <= 3:    print(count)    count += 1
```

গুরুত্বপূর্ণ keywords:

- `break` → Loop থেকে বের হয়ে যায়।
- `continue` → বর্তমান iteration-এর বাকি অংশ বাদ দিয়ে পরের iteration-এ যায়।
- `return` → Function থেকে value ফেরত দিতে বা function শেষ করতে ব্যবহৃত হয়।

## ৪. Object-Oriented Programming (OOP)

OOP হলো এমন programming paradigm, যেখানে data ও সেই data-র ওপর কাজ করা methods-কে object-এর মাধ্যমে সংগঠিত করা হয়।

### Class ও Object

- Class: Object তৈরির blueprint বা কাঠামো।
- Object: Class-এর instance।

```
class Employee:    def __init__(self, name, salary):        self.name = name        self.salary = salary    def show_info(self):        print(self.name, self.salary)employee1 = Employee("Rahim", 30000)employee1.show_info()
```

এখানে `Employee` হলো class এবং `employee1` হলো object।

### OOP-এর চারটি মূল ধারণা

### 1. Encapsulation

Data ও methods-কে একটি unit-এর মধ্যে সংগঠিত করা এবং access নিয়ন্ত্রণ করা।

উদাহরণ: Account class-এর balance পরিবর্তন করার জন্য নির্দিষ্ট method ব্যবহার করা।

### 2. Inheritance

একটি class অন্য class-এর বৈশিষ্ট্য ও behavior উত্তরাধিকারসূত্রে পেতে পারে।

উদাহরণ: `Admin` class, `User` class থেকে inherit করতে পারে।

### 3. Polymorphism

একই interface বা method বিভিন্ন object-এর ক্ষেত্রে ভিন্নভাবে কাজ করতে পারে।

উদাহরণ: ভিন্ন payment class-এ `pay()` method-এর ভিন্ন implementation।

### 4. Abstraction

প্রয়োজনীয় interface দেখিয়ে implementation-এর অপ্রয়োজনীয় detail আড়াল করা।

উদাহরণ: ব্যবহারকারী `pay()` call করেন; payment-এর internal processing আলাদা থাকে।

### OOP-এর আরও গুরুত্বপূর্ণ terms

- Constructor: Object তৈরি হওয়ার সময় initialization করে; Python-এ `__init__()` সাধারণত এই কাজে ব্যবহৃত হয়।
- Method: Class-এর সঙ্গে সম্পর্কিত function।
- Overriding: Subclass-এ inherited method-এর নতুন implementation দেওয়া।
- Overloading: একই নামের operation ভিন্ন parameter-এ ব্যবহার করার ধারণা; Python-এ traditional signature-based method overloading সরাসরি Java/C++-এর মতো নয়।

## ৫. Data Structures

Data Structure হলো computer memory-তে data সংগঠিত ও পরিচালনা করার পদ্ধতি।

| Data structure | প্রধান বৈশিষ্ট্য                       | সাধারণ ব্যবহার             |
| -------------- | -------------------------------------- | -------------------------- |
| Array          | Index দিয়ে element access              | Sequential data            |
| Linked List    | Node ও link দিয়ে গঠিত                  | Dynamic insertion/deletion |
| Stack          | LIFO — Last In, First Out              | Undo, function calls       |
| Queue          | FIFO — First In, First Out             | Scheduling, waiting line   |
| Hash Table     | Key দিয়ে দ্রুত lookup                  | Dictionary, cache          |
| Tree           | Hierarchical structure                 | File system, search tree   |
| Graph          | Vertex ও edge                          | Network topology, routes   |
| Heap           | Priority অনুযায়ী parent-child ordering | Priority queue             |

### Stack বনাম Queue

### Stack

LIFO

Top: 30

20

10

শেষে ঢোকে, আগে বের হয়

### Queue

FIFO

Front: 10

20

Rear: 30

আগে ঢোকে, আগে বের হয়

Exam tip: Stack-এর `push` দিয়ে element যোগ হয় এবং `pop` দিয়ে top element সরানো হয়। Queue-তে `enqueue` দিয়ে যোগ এবং `dequeue` দিয়ে সামনের element সরানো হয়।

## ৬. Algorithms ও Searching

Algorithm হলো কোনো সমস্যা সমাধানের সুনির্দিষ্ট ধাপে ধাপে পদ্ধতি।

### Linear Search

প্রতিটি element ধারাবাহিকভাবে পরীক্ষা করে target খোঁজা হয়।

```
def linear_search(items, target):    for i, value in enumerate(items):        if value == target:            return i    return -1print(linear_search([10, 20, 30, 40], 30))
```

Output: `2` — কারণ Python list-এর index শূন্য থেকে শুরু হয়।

- Best case: \\(O(1)\\)
- Worst case: \\(O(n)\\)

### Binary Search

Sorted data-কে বারবার অর্ধেক করে search space ছোট করে।

```
def binary_search(items, target):    left, right = 0, len(items) - 1    while left <= right:        mid = (left + right) // 2        if items[mid] == target:            return mid        elif items[mid] < target:            left = mid + 1        else:            right = mid - 1    return -1print(binary_search([10, 20, 30, 40, 50], 40))
```

Output: `3`।

অত্যন্ত গুরুত্বপূর্ণ: Binary Search-এর জন্য data sorted থাকতে হবে।

### Sorting Algorithms

| Algorithm      | Average time complexity  | বিশেষ বৈশিষ্ট্য                 |
| -------------- | ------------------------ | ------------------------------- |
| Bubble Sort    | \\(O(n^2)\\)             | পাশাপাশি element compare ও swap |
| Selection Sort | \\(O(n^2)\\)             | প্রতিবার minimum/maximum খোঁজে  |
| Insertion Sort | \\(O(n^2)\\)             | sorted অংশে element insert করে  |
| Merge Sort     | \\(O(n\log n)\\)         | Divide and conquer              |
| Heap Sort      | \\(O(n\log n)\\)         | Heap ব্যবহার করে                |
| Quick Sort     | \\(O(n\log n)\\) average | Worst case \\(O(n^2)\\)         |

Sorting-এর complexity implementation ও input-এর ওপর নির্ভর করতে পারে। উদাহরণস্বরূপ, optimized Bubble Sort-এর best case \\(O(n)\\) হতে পারে।

## ৭. Big-O Time ও Space Complexity

Big-O notation input-এর আকার বাড়লে algorithm-এর time বা memory usage কীভাবে বাড়তে পারে, তা বোঝাতে ব্যবহৃত হয়।

এটি সাধারণত growth rate প্রকাশ করে; নির্দিষ্ট execution time নয়।

| Complexity       | নাম          | উদাহরণ                               |
| ---------------- | ------------ | ------------------------------------ |
| \\(O(1)\\)       | Constant     | Array-এর নির্দিষ্ট index access      |
| \\(O(\log n)\\)  | Logarithmic  | Binary Search                        |
| \\(O(n)\\)       | Linear       | Linear Search-এর worst case          |
| \\(O(n\log n)\\) | Linearithmic | Merge Sort                           |
| \\(O(n^2)\\)     | Quadratic    | সাধারণ Bubble Sort-এর worst case     |
| \\(O(2^n)\\)     | Exponential  | কিছু brute-force recursive algorithm |
| \\(O(n!)\\)      | Factorial    | সব permutation তৈরি করার algorithm   |

সাধারণত input বড় হলে \\(O(n)\\) algorithm, \\(O(n^2)\\) algorithm-এর তুলনায় বেশি scalable হয়। তবে বাস্তবে constant factor, memory access এবং implementation-ও গুরুত্বপূর্ণ।

### একটি ছোট উদাহরণ

```
# O(1)print(items[0])# O(n)for item in items:    print(item)# O(n^2)for x in items:    for y in items:        print(x, y)
```

- প্রথম উদাহরণে list-এর size বাড়লেও একটি index access-এর কাজ constant থাকে।
- দ্বিতীয় উদাহরণে `n`টি item হলে loop প্রায় `n` বার চলে।
- তৃতীয় উদাহরণে দুটি nested loop-এর কারণে প্রায় \\(n^2\\) বার pair process হয়।

### Time Complexity বনাম Space Complexity

- Time Complexity: Input size-এর সঙ্গে কাজের পরিমাণ কীভাবে বাড়ে।
- Space Complexity: Algorithm চালাতে কত memory প্রয়োজন হয়।

উদাহরণ: কোনো algorithm যদি input size `n`-এর জন্য নতুন `n`-element list তৈরি করে, তবে সেই অতিরিক্ত list-এর space complexity \\(O(n)\\)।

## ৮. Recursion কী?

Recursion হলো কোনো function-এর নিজের ভেতর থেকে নিজেকেই call করা।

উদাহরণ — Factorial:

```
def factorial(n):    if n <= 1:        return 1    return n * factorial(n - 1)print(factorial(5))  # 120
```

এখানে:

\\[ 5! = 5\times4\times3\times2\times1=120 \\]

Recursion-এ দুটি বিষয় গুরুত্বপূর্ণ:

1. Base case: কখন recursion থামবে।
2. Recursive case: কীভাবে ছোট problem-এর মাধ্যমে একই problem সমাধান হবে।

Base case না থাকলে অনিয়ন্ত্রিত recursion হতে পারে এবং Python-এ `RecursionError` দেখা দিতে পারে।

## ৯. Programming Paradigms — সংক্ষেপে

| Paradigm        | বৈশিষ্ট্য                                               |
| --------------- | ------------------------------------------------------- |
| Procedural      | ধাপে ধাপে procedure/function দিয়ে কাজ সংগঠিত করে        |
| Object-oriented | Object ও class-এর মাধ্যমে program সংগঠিত করে            |
| Functional      | Function composition ও immutable data-র ওপর গুরুত্ব দেয় |
| Event-driven    | Event ঘটলে সংশ্লিষ্ট handler চালু হয়                    |

Python একাধিক programming paradigm সমর্থন করে।

## ১০. Teletalk Technical Exam — MCQ Practice

এবার ১৫টি প্রশ্নের উত্তর দাও। শেষে Check Answers চাপলে score এবং প্রতিটি উত্তরের ব্যাখ্যা দেখতে পাবে।

## Lesson 15 Test

0/15 answered

1\. Algorithm কী?

A. শুধু একটি programming language

B. সমস্যা সমাধানের ধাপে ধাপে পদ্ধতি

C. একটি database table

D. একটি operating system

2\. Python-এ কোন operator remainder বা ভাগশেষ দেয়?

A. //

B. \*\*

C. %

D. ==

3\. Python-এ কোনটি equality comparison operator?

A. =

B. ==

C. :=

D. !=

4\. Class-এর instance-কে কী বলা হয়?

A. Loop

B. Object

C. Operator

D. Module

5\. OOP-এ inheritance কী?

A. একটি class অন্য class-এর বৈশিষ্ট্য inherit করতে পারে

B. শুধু variable delete করা

C. Database index তৈরি করা

D. Program compile করা

6\. OOP-এর চারটি মূল ধারণার মধ্যে কোনটি আছে?

A. Encapsulation

B. Fragmentation

C. Multiplexing

D. Subnetting

7\. Stack কোন principle অনুসরণ করে?

A. FIFO

B. LIFO

C. Random only

D. Sorted order

8\. Queue কোন principle অনুসরণ করে?

A. LIFO

B. FIFO

C. FILO only

D. Binary search

9\. Binary Search-এর জন্য সাধারণত কী প্রয়োজন?

A. Data sorted থাকা

B. সব element unique হওয়া বাধ্যতামূলক

C. শুধু linked list থাকা

D. Data encrypted থাকা

10\. Linear Search-এর worst-case time complexity কত?

A. O(1)

B. O(log n)

C. O(n)

D. O(n log n)

11\. Merge Sort-এর সাধারণ worst-case time complexity কত?

A. O(n²)

B. O(n log n)

C. O(log n)

D. O(1)

12\. দুটি nested loop প্রতিটি n বার চললে সাধারণত time complexity কত?

A. O(1)

B. O(log n)

C. O(n)

D. O(n²)

13\. Big-O notation প্রধানত কী বোঝায়?

A. Programmer-এর নাম

B. Growth rate-এর asymptotic upper bound

C. শুধু program-এর exact seconds

D. শুধু file size

14\. Recursion-এ base case-এর কাজ কী?

A. Recursion বন্ধ হওয়ার শর্ত নির্ধারণ করা

B. Database তৈরি করা

C. Loop-কে সবসময় অসীম করা

D. Variable rename করা

15\. Python-এ factorial(5)-এর ফল কত?

A. 15

B. 25

C. 120

D. 720

Check Answers

## শেষ মুহূর্তের Revision Sheet

- Algorithm: সমস্যা সমাধানের ধাপ।
- Class: Object তৈরির blueprint।
- OOP: Encapsulation, Inheritance, Polymorphism, Abstraction।
- Stack: LIFO।
- Queue: FIFO।
- Binary Search: Sorted data; \\(O(\log n)\\)।
- Linear Search: Worst case \\(O(n)\\)।
- Merge Sort: \\(O(n\log n)\\)।
- Bubble Sort: Worst case \\(O(n^2)\\)।
- Recursion: Function নিজের মধ্যে নিজেকে call করে।
- Big-O: Input size বাড়লে algorithm-এর growth rate বোঝায়।

পরবর্তী লেসন হবে লেসন ১৬ — Operating Systems, Process, Thread, CPU Scheduling, Memory Management ও Deadlock। এগুলোও Computer Science ও technical recruitment পরীক্ষার গুরুত্বপূর্ণ বিষয়।


# লেসন ১৬: Operating System (OS), Process, Thread, CPU Scheduling, Memory Management ও Deadlock

এই লেসনে আমরা Teletalk Bangladesh Limited-এর টেকনিক্যাল পরীক্ষার জন্য গুরুত্বপূর্ণ Operating System (OS) বিষয়গুলো সহজ বাংলায় শিখব। প্রতিটি টপিকে থাকবে সংজ্ঞা, বাস্তব উদাহরণ এবং পরীক্ষায় মনে রাখার মতো তথ্য।

## ১. Operating System (OS) কী?

Operating System হলো System Software, যা Computer Hardware ও User/Application-এর মধ্যে সংযোগ স্থাপন করে এবং কম্পিউটারের বিভিন্ন Resource পরিচালনা করে।

User / Application Software

Browser, VS Code, Media Player

Operating System

Windows, Linux, macOS, Android

Computer Hardware

CPU, RAM, Disk, Keyboard, Network Card

### OS-এর প্রধান কাজ

- Process Management: কোন Program কখন CPU ব্যবহার করবে, তা পরিচালনা করা।
- Memory Management: RAM বরাদ্দ ও মুক্ত করা।
- File Management: ফাইল ও ডিরেক্টরি পরিচালনা করা।
- Device Management: Printer, Keyboard, Disk ইত্যাদি নিয়ন্ত্রণ করা।
- Security: User permission ও access নিয়ন্ত্রণ করা।
- Networking: Network communication-এর জন্য প্রয়োজনীয় সুবিধা দেওয়া।

### গুরুত্বপূর্ণ Operating System-এর ধরন

| ধরন                 | কাজ/বৈশিষ্ট্য                                          |
| ------------------- | ------------------------------------------------------ |
| Batch OS            | কাজগুলো Batch আকারে প্রসেস করে                         |
| Multiprogramming OS | একাধিক Program-কে Memory-তে রেখে CPU ব্যবহার উন্নত করে |
| Multitasking OS     | একাধিক কাজের মধ্যে দ্রুত CPU time ভাগ করে              |
| Multi-user OS       | একাধিক User-কে সিস্টেম ব্যবহার করতে দেয়                |
| Multiprocessing OS  | একাধিক CPU/Core ব্যবহার করে                            |
| Real-Time OS (RTOS) | নির্দিষ্ট সময়সীমার মধ্যে Response দেওয়ার জন্য তৈরি     |
| Distributed OS      | একাধিক কম্পিউটারের Resource সমন্বয় করতে পারে           |

মনে রাখবে: Linux একটি Operating System Kernel-ভিত্তিক OS family-এর অংশ; Android-ও Linux Kernel ব্যবহার করে।

## ২. Kernel, Shell ও System Call

[#kernel #linux #os #infrastructure | Khalil BEN ROMDHANE](https://images.openai.com/static-rsc-4/2WKr0_ge3TtKRfCRHakM8OAQmYo2Ix6ZR177LhAoiUicJnEF3CX5omvEah2-HKrWu3LzCWavsFvm_AXMLXwEBJKcg95z-z6-A4uC5ghw7kRA00vvhxetr49SKzkWwKapRcEFF7ErsWuw2S6NIo-QXv36K3vnsxfB8LPnpzTMxVM?purpose=inline)

Kernel

OS-এর মূল অংশ। CPU, Memory ও Hardware Resource পরিচালনা করে।

[Linux Overview (3.1) > Linux Operating System | Cisco Press](https://images.openai.com/static-rsc-4/0kqu5NyRbN-JEHOjnrmKpgH72vWM06wTpzR_xskjcsR-bPLIzRSE6e7rSuiMuUM6963O9MZgQZIywSSwdl1xOy7sCgHJE1d1rFMOI6yqMjOW4vuFDOKLSBGVgd08PKabjd6bZ9ijDm0GAPnQl6T0x8g2PC_W3XSwcM-CZYDmsRE?purpose=inline)

Shell

User-এর Command গ্রহণ করে এবং OS-এর সঙ্গে কাজ করার Interface দেয়। উদাহরণ: Bash, Zsh।

System Call

Application যখন OS Kernel-এর কাছ থেকে কোনো Service চায়, তখন System Call ব্যবহার করতে পারে। যেমন ফাইল খোলা, Process তৈরি করা বা Data পড়া।

পরীক্ষায় গুরুত্বপূর্ণ: Kernel হলো OS-এর Core; Shell হলো User ও OS-এর মধ্যে Command Interface।

## ৩. Program, Process ও Thread

এই তিনটির পার্থক্য প্রায়ই পরীক্ষায় আসে।

- Program: Disk-এ থাকা নির্দেশনার একটি ফাইল বা সেট।
- Process: কোনো Program Execution বা চলমান অবস্থায় থাকলে সেটি Process।
- Thread: Process-এর মধ্যে Execution-এর একটি ছোট Unit। একই Process-এর Thread-গুলো সাধারণত Code, Data ও Heap Memory Share করে; তবে প্রত্যেক Thread-এর নিজস্ব Stack ও Register State থাকে।

উদাহরণ: তোমার কম্পিউটারে Browser-এর executable file হলো Program। Browser চালু করলে একটি বা একাধিক Process তৈরি হতে পারে; সেই Process-এর ভেতরে বিভিন্ন Thread কাজ করতে পারে।

### Process-এর State

New

Process তৈরি হচ্ছে

Ready

CPU পাওয়ার অপেক্ষায়

Running

CPU-তে চলছে

Terminated

কাজ শেষ

Running Process I/O-এর জন্য অপেক্ষা করলে Waiting/Blocked State-এ যেতে পারে; I/O শেষ হলে সাধারণত Ready State-এ ফেরে।

### Process বনাম Thread

| বিষয়                    | Process                                    | Thread                                                         |
| ----------------------- | ------------------------------------------ | -------------------------------------------------------------- |
| Memory                  | সাধারণত আলাদা Address Space                | একই Process-এর Memory Share করে                                |
| Creation/Context Switch | তুলনামূলকভাবে বেশি Overhead হতে পারে       | একই Process-এর Thread-এ তুলনামূলক কম Overhead হতে পারে         |
| Communication           | IPC প্রয়োজন হতে পারে                       | Shared Memory-এর মাধ্যমে সহজে যোগাযোগ করতে পারে                |
| Failure                 | সাধারণত আলাদা Process-এর Memory আলাদা থাকে | একই Process-এর Thread-এর ভুল অন্য Thread-কে প্রভাবিত করতে পারে |

## ৪. CPU Scheduling Algorithms

CPU Scheduling হলো Ready Queue থেকে কোন Process-কে CPU দেওয়া হবে, তা নির্ধারণ করার পদ্ধতি।

### গুরুত্বপূর্ণ Scheduling Algorithm

১. FCFS — First Come, First Served

যে Process আগে আসে, সেটি আগে CPU পায়। এটি সাধারণত Non-preemptive।

উদাহরণ: P1 আগে এলে P1, তারপর P2, তারপর P3।

অসুবিধা: দীর্ঘ Process সামনে থাকলে ছোট Process-কে অনেক অপেক্ষা করতে হতে পারে।

২. SJF — Shortest Job First

যে Process-এর CPU Burst Time সবচেয়ে কম, সেটিকে আগে চালানো হয়।

সুবিধা: উপযুক্ত পরিস্থিতিতে Average Waiting Time কমায়। অসুবিধা: Burst Time আগে থেকে জানা কঠিন হতে পারে।

৩. SRTF — Shortest Remaining Time First

এটি Preemptive SJF। নতুন কোনো Process এলে তার Remaining Time চলমান Process-এর চেয়ে কম হলে CPU বদলাতে পারে।

৪. Round Robin (RR)

প্রত্যেক Process নির্দিষ্ট সময়ের একটি অংশ পায়, যাকে Time Quantum বলে। সময় শেষ হলে Process সম্পূর্ণ না হলেও CPU অন্য Process-কে দেওয়া হতে পারে।

Time-sharing System-এ খুব গুরুত্বপূর্ণ।

৫. Priority Scheduling

Priority অনুযায়ী Process নির্বাচন করা হয়। Priority বেশি হলে সাধারণত আগে CPU পায়—যদিও Priority-এর সংখ্যাগত নিয়ম OS অনুযায়ী ভিন্ন হতে পারে।

সমস্যা: Starvation। সমাধানের একটি পদ্ধতি হলো Aging—অপেক্ষার সময় বাড়ার সঙ্গে Priority উন্নত করা।

### Preemptive বনাম Non-preemptive

- Preemptive: OS চলমান Process থেকে CPU নিয়ে অন্য Process-কে দিতে পারে।
- Non-preemptive: Process CPU পেলে সাধারণত কাজ শেষ করা বা অপেক্ষায় যাওয়ার আগ পর্যন্ত CPU ধরে রাখে।

### পরীক্ষার জন্য দুটি Formula

\\[ \text{Turnaround Time}=\text{Completion Time}-\text{Arrival Time} \\]

\\[ \text{Waiting Time}=\text{Turnaround Time}-\text{CPU Burst Time} \\]

উদাহরণ: একটি Process-এর Arrival Time = 0, Completion Time = 10, CPU Burst Time = 6।

- Turnaround Time = 10 − 0 = 10
- Waiting Time = 10 − 6 = 4

এখানে Process-টি মোট ১০ ইউনিট সময়ের মধ্যে ৬ ইউনিট CPU ব্যবহার করেছে এবং ৪ ইউনিট অপেক্ষা করেছে।

## ৫. Memory Management

Operating System RAM-কে বিভিন্ন Process-এর মধ্যে পরিচালনা করে।

### Memory-এর ধরন

| Memory            | বৈশিষ্ট্য                                        |
| ----------------- | ------------------------------------------------ |
| Register          | CPU-এর ভেতরে খুব দ্রুত ছোট Storage               |
| Cache             | CPU-র কাছে থাকা দ্রুতগতির Memory                 |
| RAM               | চলমান Program ও Data রাখে; সাধারণত Volatile      |
| ROM               | Non-volatile Memory; বিদ্যুৎ বন্ধ হলেও Data থাকে |
| Secondary Storage | SSD/HDD-তে দীর্ঘমেয়াদে Data সংরক্ষণ              |

### Virtual Memory কী?

Virtual Memory এমন একটি ব্যবস্থা, যার মাধ্যমে OS Disk-এর একটি অংশসহ বিভিন্ন Memory Management কৌশল ব্যবহার করে Process-কে Physical RAM-এর চেয়ে বড় Address Space ব্যবহারের সুবিধা দেয়।

- Paging: Memory-কে নির্দিষ্ট আকারের Page ও Frame-এ ভাগ করা হয়।
- Page Table: Virtual Page ও Physical Frame-এর Mapping রাখে।
- Page Fault: প্রয়োজনীয় Page RAM-এ না থাকলে সেটি Handle করার জন্য OS-এর কাছে Trap/Exception হয়। তখন Page আনতে হতে পারে।
- Thrashing: অতিরিক্ত Page Fault ও ঘন ঘন Paging-এর কারণে System-এর কার্যকর কাজের গতি খুব কমে যাওয়া।

### Paging বনাম Segmentation

| Paging                                                                              | Segmentation                                                         |
| ----------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Fixed-size Page/Frame                                                               | Logical Segment; আকার ভিন্ন হতে পারে                                 |
| Page হলো নির্দিষ্ট আকারের Block                                                     | Segment হতে পারে Code, Data বা Stack                                 |
| Page Table দিয়ে Mapping                                                             | Segment Table দিয়ে Mapping                                           |
| Page-এর কারণে External Fragmentation সাধারণত হয় না; Internal Fragmentation হতে পারে | প্রচলিত Variable-size Segmentation-এ External Fragmentation হতে পারে |

মনে রাখবে: Virtual Memory মানে অতিরিক্ত RAM লাগানো নয়; এটি Memory Management-এর একটি কৌশল। Disk RAM-এর চেয়ে অনেক ধীর।

## ৬. Deadlock

Deadlock হলো এমন অবস্থা, যেখানে দুই বা তার বেশি Process একে অপরের ধরে রাখা Resource-এর জন্য অপেক্ষা করতে থাকে এবং কেউই এগোতে পারে না।

উদাহরণ:

- Process P1 Resource A ধরে রেখে Resource B-এর জন্য অপেক্ষা করছে।
- Process P2 Resource B ধরে রেখে Resource A-এর জন্য অপেক্ষা করছে।
- দুজনই অপেক্ষা করতে থাকলে Deadlock তৈরি হতে পারে।

### Deadlock-এর চারটি প্রয়োজনীয় শর্ত

1\. Mutual Exclusion

কোনো Resource এক সময়ে শুধু একটি Process ব্যবহার করতে পারে।

2\. Hold and Wait

Process একটি Resource ধরে রেখে অন্য Resource-এর জন্য অপেক্ষা করে।

3\. No Preemption

Process-এর কাছ থেকে Resource জোর করে কেড়ে নেওয়া যায় না—অন্তত ওই ব্যবস্থায়।

4\. Circular Wait

Process-গুলোর মধ্যে Resource-এর জন্য বৃত্তাকার অপেক্ষার সম্পর্ক থাকে।

Deadlock-এর জন্য চারটি শর্তই প্রয়োজনীয়। এর যেকোনো একটি প্রতিরোধ করতে পারলে Deadlock Prevention করা সম্ভব।

### Deadlock Handling-এর পদ্ধতি

- Prevention: চারটি শর্তের অন্তত একটি অসম্ভব করা।
- Avoidance: Resource বরাদ্দের আগে System Safe State-এ থাকবে কি না বিবেচনা করা। পরিচিত Algorithm: Banker's Algorithm।
- Detection and Recovery: Deadlock শনাক্ত করে Process বন্ধ করা বা Resource পুনরুদ্ধারের ব্যবস্থা করা।
- Ignore: কিছু General-purpose OS নির্দিষ্ট পরিস্থিতিতে Deadlock পুরোপুরি প্রতিরোধ বা Detect না-ও করতে পারে।

### Deadlock বনাম Starvation

| Deadlock                                              | Starvation                                            |
| ----------------------------------------------------- | ----------------------------------------------------- |
| Process-গুলো পরস্পরের জন্য অপেক্ষা করে আটকে যেতে পারে | কোনো Process দীর্ঘ সময় CPU বা Resource না-ও পেতে পারে |
| Circular Wait গুরুত্বপূর্ণ                            | Unfair Scheduling বা Priority-এর কারণে হতে পারে       |
| Resource Allocation কৌশলে প্রতিরোধ/সমাধান করা যায়     | Aging-এর মতো কৌশলে কমানো যায়                          |

## ৭. পরীক্ষার আগে দ্রুত Revision

| প্রশ্ন                                                   | সঠিক উত্তর                                    |
| -------------------------------------------------------- | --------------------------------------------- |
| OS-এর মূল অংশ কোনটি?                                     | Kernel                                        |
| চলমান Program কী?                                        | Process                                       |
| Process-এর Execution Unit কী?                            | Thread                                        |
| Time Quantum কোন Algorithm-এ ব্যবহৃত হয়?                 | Round Robin                                   |
| Shortest Job First-এর Preemptive Version কী?             | SRTF                                          |
| Priority Scheduling-এ দীর্ঘ অপেক্ষার সমস্যা কী?          | Starvation                                    |
| Virtual Memory-তে Page-এর Mapping কোথায় থাকে?            | Page Table                                    |
| অতিরিক্ত Paging-এর কারণে Performance কমে যাওয়াকে কী বলে? | Thrashing                                     |
| Deadlock Avoidance-এর পরিচিত Algorithm কী?               | Banker's Algorithm                            |
| Deadlock-এর প্রয়োজনীয় শর্ত কয়টি?                         | ৪টি                                           |
| Android কোন Kernel ব্যবহার করে?                          | Linux Kernel                                  |
| CPU Scheduling-এর উদ্দেশ্য কী?                           | CPU ও Process Execution দক্ষভাবে পরিচালনা করা |

## ৮. Lesson 16 — MCQ Practice Test

নিজে উত্তর নির্বাচন করো। শেষে Check Answers চাপলে Score ও প্রতিটি প্রশ্নের ব্যাখ্যা দেখতে পাবে।

## ১২টি MCQ

0/12 answered

প্রতিটি প্রশ্নের একটি সঠিক উত্তর রয়েছে।

1\. Operating System-এর মূল অংশ কোনটি?

A. Shell

B. Kernel

C. Compiler

D. Browser

2\. চলমান Program-কে কী বলা হয়?

A. Thread

B. File

C. Process

D. Folder

3\. কোন Scheduling Algorithm-এ Time Quantum ব্যবহৃত হয়?

A. FCFS

B. SJF

C. Round Robin

D. FIFO Page Replacement

4\. SJF-এর Preemptive Version কোনটি?

A. FCFS

B. SRTF

C. Round Robin

D. Priority Aging

5\. Priority Scheduling-এ দীর্ঘ সময় CPU না পাওয়ার সমস্যাকে কী বলে?

A. Thrashing

B. Starvation

C. Paging

D. Spooling

6\. Turnaround Time-এর Formula কোনটি?

A. Arrival − Completion

B. Completion − Arrival

C. Burst − Waiting

D. Waiting − Arrival

7\. Virtual Memory-তে Page Mapping কোথায় সংরক্ষিত হয়?

A. Page Table

B. CPU Register only

C. File System Table

D. DNS Table

8\. Thrashing সাধারণত কোন সমস্যার সঙ্গে সম্পর্কিত?

A. অতিরিক্ত Page Fault

B. দ্রুত CPU Clock

C. কম DNS Query

D. বেশি Printer

9\. নিচের কোনটি Deadlock-এর প্রয়োজনীয় শর্ত?

A. Circular Wait

B. High CPU Clock

C. Large RAM

D. Fast Internet

10\. Banker's Algorithm কোন কাজে পরিচিত?

A. Deadlock Avoidance

B. File Compression

C. DNS Resolution

D. CPU Cooling

11\. একই Process-এর Thread-গুলো সাধারণত কী Share করে?

A. নিজস্ব Stack সবসময়

B. Code ও Data/Heap Memory

C. সব Register State

D. আলাদা Address Space প্রত্যেকটি

12\. Android-এর Kernel কোনটি?

A. Windows NT

B. Linux Kernel

C. XNU

D. MS-DOS

Check Answers

পরবর্তী লেসন হবে Lesson 17: Software Engineering, SDLC, Agile, Scrum, Testing, Git ও Software Development-এর গুরুত্বপূর্ণ Interview/MCQ প্রশ্ন।

# লেসন ১৭: Software Engineering, SDLC, Agile, Scrum, Testing ও Git

এই লেসনে Teletalk Bangladesh Limited-এর টেকনিক্যাল পরীক্ষার জন্য Software Engineering-এর গুরুত্বপূর্ণ বিষয়গুলো শিখব। বিশেষ করে SDLC, Waterfall বনাম Agile, Scrum, Software Testing, Git এবং Software Development-এর মৌলিক ধারণা—এসব থেকে MCQ আসতে পারে।

## ১. Software Engineering কী?

Software Engineering হলো নির্দিষ্ট Engineering Principles, Methods ও Tools ব্যবহার করে পরিকল্পিতভাবে Software তৈরি, পরীক্ষা, রক্ষণাবেক্ষণ ও উন্নয়ন করার পদ্ধতি।

উদাহরণ: একটি Telecom Customer Management System তৈরি করতে শুধু Code লিখলেই হবে না। Requirements সংগ্রহ, Database Design, Development, Testing, Deployment ও Maintenance—সবই প্রয়োজন।

### Software Engineering-এর প্রধান লক্ষ্য

- Reliable ও Maintainable Software তৈরি করা।
- সময় ও খরচ নিয়ন্ত্রণ করা।
- Software-এর Quality ও Security নিশ্চিত করা।
- User-এর Requirements পূরণ করা।

## ২. SDLC — Software Development Life Cycle

SDLC হলো Software তৈরির শুরু থেকে Maintenance পর্যন্ত ধাপে ধাপে কাজ করার প্রক্রিয়া।

#### 1

### Planning

কেন ও কী তৈরি হবে?

#### 2

### Requirement Analysis

User-এর চাহিদা সংগ্রহ

#### 3

### System Design

Architecture, Database, UI Design

#### 4

### Implementation

Code লেখা

#### 5

### Testing

Bug ও Requirement যাচাই

#### 6

### Deployment

ব্যবহারকারীর জন্য Release

#### 7

### Maintenance

Bug Fix ও Update

বাস্তবে SDLC Model অনুযায়ী ধাপগুলোর ক্রম ও পুনরাবৃত্তি ভিন্ন হতে পারে।

### SDLC-এর গুরুত্বপূর্ণ ধাপ

| ধাপ                  | কী করা হয়?                           | সাধারণত কী পাওয়া যায়? |
| -------------------- | ------------------------------------ | --------------------- |
| Planning             | Scope, Cost, Time, Risk নির্ধারণ     | Project Plan          |
| Requirement Analysis | User কী চায় তা বোঝা                  | SRS                   |
| Design               | Architecture, Database, UI পরিকল্পনা | Design Specification  |
| Implementation       | Programming ও Code লেখা              | Source Code           |
| Testing              | Defect ও Requirement যাচাই           | Test Report           |
| Deployment           | Software Release করা                 | Running System        |
| Maintenance          | Bug Fix, Update, Improvement         | Updated Software      |

SRS = Software Requirements Specification। এতে Software-এর Functional ও Non-functional Requirements নথিভুক্ত থাকে।

- Functional Requirement: System কী কাজ করবে। যেমন, User Login করতে পারবে।
- Non-functional Requirement: System কেমনভাবে কাজ করবে। যেমন, নির্দিষ্ট Load-এ Response Time গ্রহণযোগ্য থাকবে, Security বজায় থাকবে।

## ৩. SDLC Models

### Waterfall Model

[7 Best Software Development Models And Their Application Areas | by Binmile | Binmile | Medium](https://images.openai.com/static-rsc-4/2lz8pwOTDsnNGRyrlElEte-7BPj5IbemoHYbeFyOJEHgJrdwvlvhjsGILarRqvweFSvmh_KPYFYVKpx1YIkucA8py3Se65fY4rS_0YfNUt2WpMNH-AkRNbEq1q1Ykr-YQuIwtqOc7ww4_WG0LZfsL5jyhWbHAvMWBQsP6u5Bc-Y?purpose=inline)

[medium.com](https://medium.com/binmile/7-best-software-development-models-and-their-applications-9141fb15bcdb)

Waterfall Model-এ কাজ সাধারণত ধারাবাহিক ধাপে এগোয়। একটি ধাপ শেষ করে পরের ধাপে যাওয়া হয়।

- Requirements শুরুতেই পরিষ্কার থাকলে কার্যকর হতে পারে।
- আগের ধাপে ফিরে পরিবর্তন করা তুলনামূলক কঠিন ও ব্যয়বহুল হতে পারে।
- Documentation ও নির্দিষ্ট Phase গুরুত্বপূর্ণ।

### Agile Model

[Product Management for Journalists – Media Innovation and Entrepreneurship](https://images.openai.com/static-rsc-4/qHDNhMrC96nMXnc29zLJTaDx2T2_s-V1xPAnRULFBXeB7hziLczKghEZWVSVfj4pkdkQK9SPaT9e9j-PcdnZ4_UslBsNMbmu6y_o-S3gYyIzMe8T4ILySmEJkKnssst-o8zzGw5dEBHWtJ8asZSKIEn0daK0vamIjKyxqDYV4f8?purpose=inline)

[press.rebus.community](https://press.rebus.community/media-innovation-and-entrepreneurship/chapter/product-management/)

Agile হলো Iterative ও Incremental Software Development-এর একটি পদ্ধতি, যেখানে ছোট ছোট ধাপে Software তৈরি করা হয় এবং নিয়মিত Feedback নেওয়া হয়।

- Requirement পরিবর্তনের সঙ্গে মানিয়ে নেওয়া যায়।
- ঘন ঘন Working Software Release করা যায়।
- Team Collaboration ও Customer Feedback গুরুত্বপূর্ণ।

### Waterfall বনাম Agile

| বিষয়               | Waterfall              | Agile                                                   |
| ------------------ | ---------------------- | ------------------------------------------------------- |
| Development        | ধারাবাহিক ধাপ          | ছোট Iteration/Increment                                 |
| Requirement Change | তুলনামূলক কঠিন         | তুলনামূলক সহজ                                           |
| Feedback           | সাধারণত নির্দিষ্ট ধাপে | নিয়মিত                                                  |
| Delivery           | প্রায়ই শেষে            | ছোট ছোট Increment-এ হতে পারে                            |
| Documentation      | সাধারণত Phase-based    | প্রয়োজন অনুযায়ী; Documentation বাদ দেওয়া বাধ্যতামূলক নয় |

### অন্যান্য গুরুত্বপূর্ণ Model

- Prototype Model: মূল Software-এর আগে নমুনা বা Prototype তৈরি করে Requirement বোঝা।
- Spiral Model: Iterative Development-এর সঙ্গে Risk Analysis-কে গুরুত্ব দেয়।
- V-Model: Development Phase-এর সঙ্গে সংশ্লিষ্ট Testing Phase-এর সম্পর্ক তুলে ধরে।
- Incremental Model: Software-কে একাধিক Functional অংশে তৈরি ও Release করা।

MCQ Tip: Risk Analysis-এর জন্য পরিচিত Model → Spiral Model। Sequential Model → Waterfall Model। Frequent Feedback ও Iteration → Agile।

## ৪. Agile ও Scrum

Scrum হলো Agile-এর একটি Framework। এটি Team-কে নির্দিষ্ট সময়ের Sprint-এ কাজ পরিকল্পনা, সম্পাদন ও Review করতে সাহায্য করে।

### Scrum-এর তিনটি প্রধান Accountability

[Scrum Artifacts Explained (With Real Talk) | by Simina F | Leadership Land | Medium](https://images.openai.com/static-rsc-4/ALa0UTO9_Kdhp1vD9hdx3CF8hS6THhe5hjp7V0o5KBtX7l8U4Ldc93TIMW5Ho2a6ykkmDwxmcK5lWc6xrD_545qdW7xBp18q9tEklXQD1eOBZWZWw3nrXHfU-rQM_i0NkD8r2nPhsX0mzilVLh5ofgnAoEPWwGcWloXCKSyGAQc?purpose=inline)

Product Owner

Product-এর Value সর্বাধিক করা এবং Product Backlog কার্যকরভাবে পরিচালনার জন্য দায়বদ্ধ।

[The Vital Role of the Scrum Master: A Crucial Component in Agile Teams | DailyBot Insights](https://images.openai.com/static-rsc-4/Mfxadb6r_unVxe37Rf49E2IsbaHVxmGJZJsgCBvax1YZ3aR1lWKxAQlsXm8Rnq1sil5Y3fyczKh_xiUjPVtYHJxrqiJC5RQJIqFtYpnDRu0ky-0BWY5eDYye__fw44leGvhX8Da533GHvWmF46gMLm4cWWEQ3gOCV2y_gSCv2cI?purpose=inline)

Scrum Master

Scrum বোঝা ও প্রয়োগে Team-কে সহায়তা করেন এবং কার্যকর Scrum-এ বাধা দূর করতে সাহায্য করেন।

[Reading code (out loud?). In the realm of computer programming… | by @boltaevt | Medium](https://images.openai.com/static-rsc-4/PUDTK9EVCww_kGllkxh_3N17a1jMIUvERvKT801RKr7BZGCSbHO37XdiMhzK6ktiPOrj5V7ZBeZoiL_82V7sxxIbyopUEbEwk79xjSKI5dcroGp-TlcFka3sN8cSAopoujH5dlNH5sdetLWTMV2PXsMMfcjgau1P7GmXz0CpdlA?purpose=inline)

Developers

প্রতিটি Sprint-এ একটি Usable Increment তৈরি করার জন্য পরিকল্পনা ও কাজ করেন।

### Scrum-এর গুরুত্বপূর্ণ Event

| Event                | উদ্দেশ্য                              |
| -------------------- | ------------------------------------- |
| Sprint               | নির্দিষ্ট সময়ের কাজের Cycle           |
| Sprint Planning      | Sprint-এর কাজ ও লক্ষ্য নির্ধারণ       |
| Daily Scrum          | অগ্রগতি পর্যালোচনা ও পরিকল্পনা সমন্বয় |
| Sprint Review        | Increment পর্যালোচনা ও Feedback নেওয়া |
| Sprint Retrospective | কাজের পদ্ধতি উন্নত করার সুযোগ খোঁজা   |

মনে রাখবে: Sprint সাধারণত এক মাস বা তার কম সময়ের হয়। Daily Scrum-এর সময় সাধারণত ১৫ মিনিট।

### Scrum-এর তিনটি Artifact

- Product Backlog: Product-এর প্রয়োজনীয় কাজের Ordered List।
- Sprint Backlog: Sprint Goal পূরণের জন্য নির্বাচিত কাজ এবং পরিকল্পনা।
- Increment: Sprint শেষে তৈরি হওয়া ব্যবহারযোগ্য Product-এর সংযোজিত অংশ।

## ৫. Software Testing

Software Testing হলো Software নির্দিষ্ট Requirements অনুযায়ী কাজ করছে কি না এবং Defect আছে কি না তা যাচাই করার প্রক্রিয়া।

### Testing-এর ধরন

| ধরন                 | অর্থ                                                  |
| ------------------- | ----------------------------------------------------- |
| Unit Testing        | ছোট Unit বা Function পরীক্ষা                          |
| Integration Testing | একাধিক Module একসঙ্গে ঠিকমতো কাজ করছে কি না           |
| System Testing      | সম্পূর্ণ System পরীক্ষা                               |
| Acceptance Testing  | User/Customer-এর Acceptance Criteria পূরণ হয়েছে কি না |
| Regression Testing  | পরিবর্তনের ফলে আগের কাজ ভেঙেছে কি না পরীক্ষা          |
| Smoke Testing       | গুরুত্বপূর্ণ Basic Functionality-এর প্রাথমিক পরীক্ষা  |
| Performance Testing | Speed, Response Time ও Load সামলানোর ক্ষমতা পরীক্ষা   |
| Security Testing    | Security Weakness খোঁজা                               |

### Black-box বনাম White-box Testing

- Black-box Testing: Internal Code না দেখে Input ও Output/Behavior পরীক্ষা করা।
- White-box Testing: Internal Code, Control Flow, Branch ও Logic বিবেচনা করে পরীক্ষা করা।

### Manual বনাম Automation Testing

- Manual Testing: Tester নিজে Test Case চালিয়ে যাচাই করেন।
- Automation Testing: Script বা Tool দিয়ে Test স্বয়ংক্রিয়ভাবে চালানো হয়।

### Verification বনাম Validation

- Verification: Software কি Specification অনুযায়ী তৈরি হচ্ছে? — Are we building the product right?
- Validation: Software কি User-এর প্রকৃত প্রয়োজন পূরণ করছে? — Are we building the right product?

### Error, Defect ও Failure

- Error: মানুষের ভুল, যেমন ভুল Logic লেখা।
- Defect/Bug: Software-এর Code বা Design-এ থাকা ত্রুটি।
- Failure: Software চলার সময় প্রত্যাশিত আচরণ না করা।

একটি Error থেকে Defect হতে পারে, আর Defect নির্দিষ্ট পরিস্থিতিতে Failure তৈরি করতে পারে।

## ৬. Software Development-এর আরও গুরুত্বপূর্ণ ধারণা

### SDLC ও STLC

- SDLC: Software Development-এর সম্পূর্ণ Life Cycle।
- STLC: Software Testing-এর পরিকল্পনা থেকে Test Closure পর্যন্ত Testing-কেন্দ্রিক Life Cycle।

### Debugging

Debugging হলো Program-এর Defect-এর কারণ খুঁজে বের করে তা সংশোধন করার প্রক্রিয়া। Testing-এ সমস্যা ধরা পড়তে পারে; Debugging-এ সাধারণত তার কারণ অনুসন্ধান করা হয়।

### API ও Documentation

- API (Application Programming Interface): এক Software Component-কে অন্য Component-এর সঙ্গে যোগাযোগের Interface দেয়।
- API Documentation: Endpoint, Request, Response, Authentication ও Error-এর বিবরণ দেয়।
- Swagger/OpenAPI: API-এর Documentation ও Specification তৈরি/দেখার জন্য বহুল ব্যবহৃত প্রযুক্তি।

### Version Control

Version Control System দিয়ে Code-এর পরিবর্তনের ইতিহাস রাখা, একাধিক Developer-এর কাজ সমন্বয় করা এবং আগের Version-এ ফিরে যাওয়া যায়।

সবচেয়ে পরিচিত Distributed Version Control System হলো Git।

## ৭. Git-এর গুরুত্বপূর্ণ Command

| Command                   | কাজ                                                |
| ------------------------- | -------------------------------------------------- |
| `git init`                | নতুন Local Git Repository তৈরি                     |
| `git clone URL`           | Repository Copy করে আনা                            |
| `git status`              | Working Tree-এর অবস্থা দেখা                        |
| `git add .`               | পরিবর্তিত ফাইল Stage করা                           |
| `git commit -m "message"` | Stage করা পরিবর্তনের Snapshot সংরক্ষণ              |
| `git log`                 | Commit History দেখা                                |
| `git branch`              | Branch দেখা                                        |
| `git switch -c feature`   | নতুন Branch তৈরি করে সেটিতে যাওয়া                  |
| `git merge feature`       | বর্তমান Branch-এ অন্য Branch-এর পরিবর্তন Merge করা |
| `git pull`                | Remote থেকে পরিবর্তন Fetch করে Integrate করা       |
| `git push`                | Local Commit Remote Repository-তে পাঠানো           |

### Git-এর তিনটি গুরুত্বপূর্ণ জায়গা

Working Directory

যেখানে তুমি ফাইল Edit করো

Staging Area

Commit-এর জন্য পরিবর্তন নির্বাচন

Local Repository

Commit History সংরক্ষিত থাকে

সাধারণ Workflow:

```
git status
git add .
git commit -m "Add login API"
git push origin main
```

গুরুত্বপূর্ণ পার্থক্য: Git হলো Version Control System; GitHub হলো Git Repository Host করার একটি Platform। `git add` পরিবর্তন Stage করে, আর `git commit` Local Repository-তে Commit তৈরি করে।

## ৮. Software Quality ও Design Principles

### DRY, KISS ও SOLID

| Principle | পূর্ণরূপ/অর্থ                                              |
| --------- | ---------------------------------------------------------- |
| DRY       | Don't Repeat Yourself — একই Logic অপ্রয়োজনে বারবার না লেখা |
| KISS      | Keep It Simple — সমাধান যতটা সম্ভব সহজ রাখা                |
| SOLID     | Object-Oriented Design-এর পাঁচটি গুরুত্বপূর্ণ Principle    |

SOLID-এর পাঁচটি Principle:

- S — Single Responsibility Principle: একটি Class বা Module-এর পরিবর্তনের জন্য একটি প্রধান দায়িত্ব থাকা উচিত।
- O — Open/Closed Principle: Extension-এর জন্য Open, Modification-এর জন্য Closed।
- L — Liskov Substitution Principle: Subclass-কে উপযুক্ত ক্ষেত্রে Base Class-এর বিকল্প হিসেবে ব্যবহার করা যাবে।
- I — Interface Segregation Principle: অপ্রয়োজনীয় Method-সমৃদ্ধ বড় Interface-এর বদলে ছোট, নির্দিষ্ট Interface ভালো।
- D — Dependency Inversion Principle: High-level Module যেন সরাসরি Low-level Implementation-এর ওপর নির্ভর না করে; Abstraction গুরুত্বপূর্ণ।

### Coupling ও Cohesion

- High Cohesion: একটি Module-এর কাজগুলো পরস্পরের সঙ্গে সম্পর্কযুক্ত।
- Low Coupling: একটি Module পরিবর্তন করলে অন্য Module-এর ওপর কম প্রভাব পড়ে।

সাধারণভাবে ভালো Software Design-এ High Cohesion ও Low Coupling কাম্য।

## ৯. পরীক্ষার জন্য দ্রুত Revision

| প্রশ্ন                                       | উত্তর                                           |
| -------------------------------------------- | ----------------------------------------------- |
| SRS-এর পূর্ণরূপ কী?                          | Software Requirements Specification             |
| Risk Analysis-এ পরিচিত SDLC Model কোনটি?     | Spiral Model                                    |
| Scrum কী?                                    | Agile Framework                                 |
| Daily Scrum সাধারণত কত মিনিট?                | ১৫ মিনিট                                        |
| Sprint-এর সময়সীমা সর্বোচ্চ কত?               | এক মাস                                          |
| Unit Testing কী পরীক্ষা করে?                 | ছোট Unit/Function                               |
| Regression Testing কেন করা হয়?               | পরিবর্তনে পুরোনো Functionality নষ্ট হয়েছে কি না |
| Black-box Testing-এ কী দেখা হয়?              | Internal Code না দেখে External Behavior         |
| Git-এর Stage করার Command কী?                | `git add`                                       |
| Commit History দেখার Command কী?             | `git log`                                       |
| Git Repository Host করার পরিচিত Platform কী? | GitHub                                          |
| DRY-এর পূর্ণরূপ কী?                          | Don't Repeat Yourself                           |
| ভালো Design-এ কেমন Coupling কাম্য?           | Low Coupling                                    |
| Verification কী যাচাই করে?                   | Specification অনুযায়ী তৈরি হচ্ছে কি না          |
| Validation কী যাচাই করে?                     | User-এর প্রয়োজন পূরণ হচ্ছে কি না                |

## ১০. Lesson 17 — MCQ Practice Test

## ১২টি MCQ

0/12 answered

1\. SDLC-এর Requirement Specification-এর পরিচিত Document কোনটি?

A. SRS

B. CPU

C. DNS

D. HTML

2\. কোন SDLC Model Risk Analysis-কে বিশেষ গুরুত্ব দেয়?

A. Waterfall

B. Spiral

C. V-Model only

D. Big Bang only

3\. Agile-এর একটি Framework কোনটি?

A. Scrum

B. TCP

C. SQL

D. DNS

4\. Daily Scrum সাধারণত কত মিনিটের Event?

A. ৫ মিনিট

B. ১৫ মিনিট

C. ৬০ মিনিট

D. ১২০ মিনিট

5\. Product Backlog-এর দায়িত্বে প্রধানত কে থাকেন?

A. Product Owner

B. End User only

C. Database Server

D. Compiler

6\. কোন Testing ছোট Function বা Unit পরীক্ষা করে?

A. System Testing

B. Unit Testing

C. Acceptance Testing

D. Load Testing

7\. পরিবর্তনের পরে আগের Functionality ঠিক আছে কি না কোন Testing যাচাই করে?

A. Regression Testing

B. Smoke only

C. Acceptance only

D. Static Typing

8\. Black-box Testing-এর বৈশিষ্ট্য কোনটি?

A. শুধু Internal Code পরীক্ষা

B. External Behavior পরীক্ষা

C. শুধু Database Schema তৈরি

D. শুধু Code Compile

9\. Git-এ পরিবর্তন Stage করার Command কোনটি?

A. git push

B. git add

C. git log

D. git clone

10\. Git-এর Commit History দেখার Command কোনটি?

A. git status

B. git init

C. git log

D. git merge

11\. DRY Principle-এর অর্থ কী?

A. Do Repeat Yourself

B. Don't Repeat Yourself

C. Deploy Rapidly Yearly

D. Data Runs Yesterday

12\. ভালো Software Design-এ সাধারণত কোনটি কাম্য?

A. High Coupling, Low Cohesion

B. Low Coupling, High Cohesion

C. High Coupling, High Duplication

D. Low Cohesion only

Check Answers

পরবর্তী লেসন: Lesson 18 — Data Structures & Algorithms, Time Complexity, Searching, Sorting এবং গুরুত্বপূর্ণ Programming MCQ।

# লেসন ১৮: Data Structures & Algorithms (DSA), Time Complexity, Searching ও Sorting

এই লেসনে Teletalk Bangladesh Limited-এর টেকনিক্যাল পরীক্ষার জন্য গুরুত্বপূর্ণ Programming ও DSA বিষয়গুলো শিখব। বিশেষভাবে Array, Linked List, Stack, Queue, Tree, Graph, Big-O Notation, Searching এবং Sorting Algorithms নিয়ে আলোচনা করব।

## ১. Data Structure কী?

Data Structure হলো Computer Memory-তে Data সাজিয়ে রাখা ও কার্যকরভাবে ব্যবহার করার পদ্ধতি।

উদাহরণ: একটি Telecom System-এ হাজার হাজার Customer-এর তথ্য রাখতে Array, Hash Table বা Database Index-এর মতো Structure ব্যবহার করা যেতে পারে।

### গুরুত্বপূর্ণ Data Structures

[The 12 Data Structures Every Developer Should Master Before an Interview | by Noah Byteforge | Medium](https://images.openai.com/static-rsc-4/nMOVlA37CoDtd2JmhTyhZwyzhl67a1VCW-0dMnqIMFNw4zvGDEKINWG4wYUPmZAgdAAdzXX0ghGHIFxnRLtT43P3WDcICtBQcda590lvq_-tx_JCKaaERS0W1gYXftOdJnd0fsXwxKY8M4YowqPoq1Yi2C25ZfeDGvLo8DwWaOg?purpose=inline)

1\. Array

একই ধরনের বা নির্দিষ্ট ধরনের Element-কে Index দিয়ে Access করা যায়। সাধারণ Array-তে Index Access সাধারণত \\(O(1)\\)।

[Understanding Linked Lists: A Complete Guide | Medium](https://images.openai.com/static-rsc-4/Pk6HJuljk4nqqIsOmazaOAyhnmv7tfK7UBZMFhyjC99yj0B-ARZ786d1WyUeGiotTyUPJ_s37BDJKGyk3lUFAdvyP6i8RExPRomx_NVr9qp4NGcAr6nkssUg0nO95f-Hq2arRiFR0_nO2S5dD-KnCEBcW05unMcg6INScHUqda8?purpose=inline)

2\. Linked List

Node দিয়ে গঠিত; প্রতিটি Node-এ Data এবং পরবর্তী Node-এর Reference/Pointer থাকে। নির্দিষ্ট Position খুঁজতে সাধারণত \\(O(n)\\) লাগে।

[Java Collections Framework - A Quick and In-Depth Look (Part - 1) - DEV Community](https://images.openai.com/static-rsc-4/NX3-BSVECwqnBlGMG3rBuGkD6GAmAexSfHAKyPw1zeILXmm1zRGxXKZYjTw9_pCUMbRuHtouNTPDS8XiwOovCk4XtqZuRpEiMhdEpr9A7b456daRiUxm0p4EShihUpZ2nAPm4Tx0Au63MNnXldwOyvMQczaxAk8vPN9w5aFofB4?purpose=inline)

3\. Stack

LIFO — Last In, First Out। সর্বশেষে রাখা Element আগে বের হয়। উদাহরণ: Browser-এর Back/Undo Operation।

[Queue Data Structure - Types, Applications, JavaScript Implementation](https://images.openai.com/static-rsc-4/Pzrs8MANW5kdBh4DM8wvrBiuEjnd5N9FVDphhxq0MdUBg_U8JRSWydIqeOgKw07OhYkb0YUwTdkjzGteZySfbQImWfgq0R7lAe1XezHYxsVvR4XBRSMk4aTW0F2oPqrZpAIq9owMbBPFkQ4ha-sEcGetPqecRq5QzaHb0CwOfVw?purpose=inline)

4\. Queue

FIFO — First In, First Out। যে Element আগে আসে, সেটি আগে বের হয়। উদাহরণ: Printer Queue।

### Stack বনাম Queue

| বিষয়   | Stack          | Queue        |
| ------ | -------------- | ------------ |
| নিয়ম   | LIFO           | FIFO         |
| Insert | Push           | Enqueue      |
| Remove | Pop            | Dequeue      |
| উদাহরণ | Undo Operation | Waiting Line |

## ২. Tree, Graph, Hash Table ও Heap

[대표적인 자료구조: 트리 - 파이썬과 컴퓨터 사이언스(자료구조) | 잔재미코딩](https://images.openai.com/static-rsc-4/8G2IkAlTILHhb5j-_hpIWTaXI9Qm0ShuTZjvST-jllA4OARSvKqoENkNZp6inBQTqRKcqkLrCcy3XgjmCvmIrwr9FOpBJXCOahhb-7vfN_s7XyLUYUnclRhjcvc8gtJCm7FMXEvosKmV0PJht3zjjTeGhlLQheBomE4JA00IzLc?purpose=inline)

[fun-coding.org](https://www.fun-coding.org/post/Chapter10-tree.html)

Tree

Hierarchical Data Structure। এতে Root, Parent, Child ও Leaf Node থাকে। Binary Tree-তে প্রতিটি Node-এর সর্বোচ্চ দুটি Child থাকতে পারে।

[Graph Data Structure Cheat Sheet - Brian Vander Plaats](https://images.openai.com/static-rsc-4/X6eK9lPJgmze-B3_kO-dlNFEE2FCYe9Pk54XIEz_ML9VImYTBRXzneaoFeVtg5ndX5P262Ud4rBmAp4zEV767bgERz6a0pBnZ4Il8M9zxfi3uK3_QZ5u3ZTp2H71bKBklehrziXNRGUswU1a11DgswEvt56WJgMInHkp20BFqjk?purpose=inline)

[brianvanderplaats.com](https://brianvanderplaats.com/cheat-sheets/Graph-Data-Structure-Cheat-Sheet.html)

Graph

Vertex/Node এবং Edge দিয়ে তৈরি। Telecom Network Topology, Road Network ও Social Network বোঝাতে ব্যবহার করা যায়।

Hash Table

Key-কে Hash Function দিয়ে Index/Bucket-এ Map করে। Average Case-এ Search, Insert ও Delete প্রায়ই \\(O(1)\\), তবে Worst Case \\(O(n)\\) হতে পারে।

Heap

একটি বিশেষ Tree-based Structure। Max-Heap-এ Parent-এর Value Child-এর সমান বা বড়; Min-Heap-এ Parent-এর Value Child-এর সমান বা ছোট। Priority Queue বাস্তবায়নে ব্যবহৃত হয়।

## ৩. Algorithm ও Time Complexity

Algorithm হলো কোনো সমস্যা সমাধানের ধাপে ধাপে নির্দিষ্ট পদ্ধতি।

Time Complexity বোঝায় Input Size বাড়লে Algorithm-এর কাজের পরিমাণ কীভাবে বাড়ে। এটি সরাসরি সেকেন্ড মাপার পদ্ধতি নয়; সাধারণত Input Size \\(n\\)-এর তুলনায় Growth Rate বোঝায়।

### Big-O Notation

| Complexity       | নাম          | উদাহরণ                               |
| ---------------- | ------------ | ------------------------------------ |
| \\(O(1)\\)       | Constant     | Array Index Access                   |
| \\(O(\log n)\\)  | Logarithmic  | Binary Search                        |
| \\(O(n)\\)       | Linear       | Array-তে Linear Search               |
| \\(O(n\log n)\\) | Linearithmic | Merge Sort                           |
| \\(O(n^2)\\)     | Quadratic    | সাধারণ Bubble Sort-এর Worst Case     |
| \\(O(2^n)\\)     | Exponential  | কিছু Brute-force Recursive Algorithm |
| \\(O(n!)\\)      | Factorial    | সব Permutation পরীক্ষা করা           |

সাধারণভাবে Input Size বড় হলে \\(O(1)\\) ও \\(O(\log n)\\) তুলনামূলক দক্ষ; \\(O(n^2)\\), \\(O(2^n)\\) ও \\(O(n!)\\) বড় Input-এ দ্রুত ব্যয়বহুল হয়ে ওঠে।

### উদাহরণ: \\(O(1)\\) বনাম \\(O(n)\\)

```
# O(1): একটি নির্দিষ্ট Index Accessnumbers = [10, 20, 30, 40]print(numbers[2])  # 30
```

```
# O(n): প্রতিটি Element পরীক্ষা করতে পারেdef find_number(numbers, target):    for number in numbers:        if number == target:            return True    return False
```

দ্বিতীয় Function-এর Worst Case-এ সব \\(n\\)টি Element পরীক্ষা করতে হতে পারে।

### Big-O, Big-Ω ও Big-Θ

- Big-O: Asymptotic Upper Bound বোঝায়।
- Big-Ω (Omega): Asymptotic Lower Bound বোঝায়।
- Big-Θ (Theta): Asymptotically Tight Bound বোঝায়।

পরীক্ষায় সাধারণত Big-O বেশি দেখা যায়। তবে Big-O-কে সব পরিস্থিতিতে “Worst Case”-এর সমার্থক বলা সঠিক নয়; এটি একটি Upper Bound, যা Worst-case Analysis-এ প্রায়ই ব্যবহার করা হয়।

## ৪. Searching Algorithms

Searching হলো Data Collection থেকে নির্দিষ্ট Element খোঁজার পদ্ধতি।

### Linear Search

প্রথম Element থেকে একে একে খোঁজা হয়। Data Sorted হওয়া বাধ্যতামূলক নয়।

```
def linear_search(items, target):    for index, item in enumerate(items):        if item == target:            return index    return -1print(linear_search([7, 12, 19, 25], 19))  # 2
```

- Best Case: \\(O(1)\\)
- Worst Case: \\(O(n)\\)
- Sorted Data প্রয়োজন? না।

### Binary Search

প্রতিবার Search Space-এর প্রায় অর্ধেক বাদ দেওয়া হয়। Array/List অবশ্যই Sorted থাকতে হবে—এটি Binary Search-এর সবচেয়ে গুরুত্বপূর্ণ শর্ত।

```
def binary_search(items, target):    left, right = 0, len(items) - 1    while left <= right:        mid = (left + right) // 2        if items[mid] == target:            return mid        elif items[mid] < target:            left = mid + 1        else:            right = mid - 1    return -1print(binary_search([7, 12, 19, 25, 31], 25))  # 3
```

- Best Case: \\(O(1)\\)
- Worst Case: \\(O(\log n)\\)
- Sorted Data প্রয়োজন? হ্যাঁ।

### Linear বনাম Binary Search

| বিষয়             | Linear Search   | Binary Search                              |
| ---------------- | --------------- | ------------------------------------------ |
| Data Sorted হওয়া | প্রয়োজন নেই     | প্রয়োজন                                    |
| Worst-case Time  | \\(O(n)\\)      | \\(O(\log n)\\)                            |
| পদ্ধতি           | একে একে পরীক্ষা | মাঝের Element থেকে Search Space অর্ধেক করা |

## ৫. Sorting Algorithms

Sorting হলো Data-কে Ascending বা Descending Order-এ সাজানো।

উদাহরণ: `[40, 10, 30, 20]` → Ascending Order: `[10, 20, 30, 40]`

[The Best Task Prioritization Strategies for Maximum Productivity - Akiflow](https://images.openai.com/static-rsc-4/5VbS2z7GhwcIbcqBrHDIfjiC1cM9RkzZfehmIHMNc2VsXADQrD64GFHws2Fm7e5Rbb6oIYgs1x30zHJN9gQxR3_5Y4I3JY7FkmUpZv8u4KAE87oaAZgXP1oxFpFnC-zVF6P3tjNyFwaZEpog6qCIfl0nKhPhN5gSyO4Fmbtb4o0?purpose=inline)

[akiflow.com](https://akiflow.com/blog/prioritize-tasks-manage-time)

1\. Bubble Sort

পাশাপাশি থাকা Element তুলনা করে ভুল ক্রমে থাকলে Swap করা হয়।

- Average/Worst Case: \\(O(n^2)\\)
- Optimized Best Case: \\(O(n)\\)
- সহজ, তবে বড় Data-তে ধীর।

[Learn Algorithms by Stories. Series 6: Basic Sorting Algorithms | by Babek Naghiyev | Medium](https://images.openai.com/static-rsc-4/MY3tcWiARIX0vDIKsXia9iNmqQohNKsp-t9WUzOVsWfCgbc3yPgLsuICsxO2rpSPTI3R8MAilhibnxw32DKOhYGh3T6oiO6for0qQieXGZZzTT-SPdvF-F5rlkn0ga-WZJs6_rYx2EB13NOPulL5s3rxCmB0OzBkRfESUSEugAE?purpose=inline)

[nagibaba.medium.com](https://nagibaba.medium.com/learn-algorithms-by-stories-series-6-basic-sorting-algorithms-a1272ae4ae21)

2\. Selection Sort

প্রতিবার Unsorted অংশ থেকে সবচেয়ে ছোট Element খুঁজে সামনে বসানো হয়।

- Best/Average/Worst Case: \\(O(n^2)\\)
- সাধারণ In-place Implementation-এ অতিরিক্ত Memory: \\(O(1)\\)।

[Insertion Sort - Data Structure and Algorithm - DSA](https://images.openai.com/static-rsc-4/3zDiChbYEJ5fS8Zgb2UAQSH7v1sjp47OeJ49kL8BoRmHuydmRe0k6YDPTKSCvKQGYwETot17WJvOvBavlMpo3h6IvQQJeCFko7YwS7v5a0IGgpyF8J8uL1ENeA376Ttxrkz-o-xOVN4X9gtTAPFLab5RB1BMo_PPG70ZyfqCP2U?purpose=inline)

[saralcode.com](https://www.saralcode.com/dsa/insertion-sort-in-data-structure-and-algorithm)

3\. Insertion Sort

প্রতিটি Element-কে আগের Sorted অংশের সঠিক জায়গায় Insert করা হয়।

- Best Case: \\(O(n)\\)
- Average/Worst Case: \\(O(n^2)\\)
- ছোট বা প্রায় Sorted Data-তে কার্যকর।

[DSCI 221: Data Structures and Algorithms for Data Science – Merge Sort and Recurrence Forms](https://images.openai.com/static-rsc-4/nRzR9-ztrfaYDQkHspVjsBo9mKnZs-iMY63WXyCIEzhvTN4mzBgYMnUa86I_LaCQq22nFt9ieEJS0YON6Miy_3HfLz3Y6ErFZE-utZtztDVKI54cJMb1h68Ya45pIcfU_oH2N5MNx1eM3nI-3648NTsqncKBjRliW_BBdfHYwQU?purpose=inline)

[ubc-cs.github.io](https://ubc-cs.github.io/dsci221/slides/04_mon_mergesort.html)

4\. Merge Sort

Data-কে ছোট অংশে ভাগ করে Sort করে আবার Merge করা হয়।

- Best/Average/Worst Case: \\(O(n\log n)\\)
- Array-এর সাধারণ Implementation-এ অতিরিক্ত Memory \\(O(n)\\) লাগে।
- সাধারণত Stable Sorting Algorithm।

[Introduction to Algorithms Handbook – with JavaScript Examples](https://images.openai.com/static-rsc-4/J5XypDJTQk3ZeAUXyvn0ObDTaEH0yy47jkfBqo4xey5kBwOEnvV1gNZnZ1zdGH5HXVq8DmQYOirPHtQ_GjruVl_Mb9eBN5oYEOmv3510AToXBGBPTeAF-hVOG5hU5SeZjY-8Jj8LMl9CagXXu2EJf_cyS1b_zNdVs1F8f3sHqsc?purpose=inline)

[freecodecamp.org](https://www.freecodecamp.org/news/introduction-to-algorithms-with-javascript-examples/)

5\. Quick Sort

Pivot নির্বাচন করে Element-গুলোকে Pivot-এর তুলনায় Partition করা হয়।

- Average Case: \\(O(n\log n)\\)
- Worst Case: \\(O(n^2)\\)
- In-place Implementation প্রচলিত; Recursive Stack-এর Memory লাগে।

### Sorting Complexity এক নজরে

| Algorithm               | Best Case        | Average Case     | Worst Case       |
| ----------------------- | ---------------- | ---------------- | ---------------- |
| Bubble Sort (optimized) | \\(O(n)\\)       | \\(O(n^2)\\)     | \\(O(n^2)\\)     |
| Selection Sort          | \\(O(n^2)\\)     | \\(O(n^2)\\)     | \\(O(n^2)\\)     |
| Insertion Sort          | \\(O(n)\\)       | \\(O(n^2)\\)     | \\(O(n^2)\\)     |
| Merge Sort              | \\(O(n\log n)\\) | \\(O(n\log n)\\) | \\(O(n\log n)\\) |
| Quick Sort              | \\(O(n\log n)\\) | \\(O(n\log n)\\) | \\(O(n^2)\\)     |

পরীক্ষার জন্য মনে রাখবে:

- সাধারণ Merge Sort-এর Worst Case → \\(O(n\log n)\\)
- Quick Sort-এর Worst Case → \\(O(n^2)\\)
- Binary Search → \\(O(\log n)\\), Sorted Data প্রয়োজন
- Bubble Sort → Adjacent Element Swap
- Selection Sort → বারবার Minimum/Maximum নির্বাচন
- Insertion Sort → Sorted অংশে Element Insert

## ৬. Recursion ও Divide and Conquer

Recursion: কোনো Function নিজের মধ্যেই নিজেকে Call করে।

```
def factorial(n):    if n <= 1:          # Base Case        return 1    return n * factorial(n - 1)print(factorial(5))  # 120
```

এখানে `factorial(5)` হিসাব করতে ছোট Input-এর `factorial(4)`-সহ পরবর্তী Call-গুলো ব্যবহার করে।

- Base Case: যে শর্তে Recursion থামে।
- Recursive Case: যে অংশে Function আবার নিজেকে Call করে।
- Base Case না থাকলে অনন্ত Recursion বা Recursion Depth Error হতে পারে।

Divide and Conquer: Problem-কে ছোট Subproblem-এ ভাগ করা, সেগুলো সমাধান করা এবং প্রয়োজনমতো ফলাফল একত্র করা।

উদাহরণ: Merge Sort ও Binary Search।

## ৭. Teletalk Technical Exam — Quick Revision

| প্রশ্ন                                    | উত্তর              |
| ----------------------------------------- | ------------------ |
| Stack-এর নিয়ম কী?                         | LIFO               |
| Queue-এর নিয়ম কী?                         | FIFO               |
| Binary Search-এর Worst-case Complexity?   | \\(O(\log n)\\)    |
| Linear Search-এর Worst-case Complexity?   | \\(O(n)\\)         |
| Merge Sort-এর Worst-case Complexity?      | \\(O(n\log n)\\)   |
| Quick Sort-এর Worst-case Complexity?      | \\(O(n^2)\\)       |
| Hash Table-এর Average Search Complexity?  | সাধারণত \\(O(1)\\) |
| Heap কোথায় ব্যবহৃত হয়?                    | Priority Queue     |
| Graph-এর প্রধান উপাদান কী?                | Vertex ও Edge      |
| Recursion থামায় কী?                       | Base Case          |
| কোন Sort পাশাপাশি থাকা Element তুলনা করে? | Bubble Sort        |
| কোন Search-এ Sorted Data লাগে?            | Binary Search      |

## ৮. MCQ Practice Test

## ১২টি MCQ

0/12 answered

আগে নিজে উত্তর দাও, তারপর Check Answers চাপো।

1\. Stack কোন নীতি অনুসরণ করে?

A. FIFO

B. LIFO

C. FILO নয়

D. Random only

2\. Queue কোন নীতি অনুসরণ করে?

A. LIFO

B. FIFO

C. FILO

D. Sorted order

3\. Binary Search করার জন্য সাধারণত কী প্রয়োজন?

A. Sorted Data

B. শুধু Linked List

C. Unsorted Data

D. Hash Function বাধ্যতামূলক

4\. Linear Search-এর Worst-case Time Complexity কত?

A. O(1)

B. O(log n)

C. O(n)

D. O(n log n)

5\. Merge Sort-এর Worst-case Complexity কোনটি?

A. O(n)

B. O(n²)

C. O(log n)

D. O(n log n)

6\. Quick Sort-এর Worst-case Complexity কত?

A. O(n²)

B. O(1)

C. O(log n)

D. O(n)

7\. Bubble Sort কীভাবে কাজ করে?

A. শুধু Hash করে

B. Adjacent Element তুলনা ও প্রয়োজনে Swap করে

C. সবসময় Tree তৈরি করে

D. শুধু Minimum একবার নেয়

8\. Selection Sort-এ সাধারণত কী করা হয়?

A. প্রতিবার Minimum/Maximum নির্বাচন

B. Binary Search চালানো

C. Queue তৈরি

D. Recursion বন্ধ করা

9\. Hash Table-এর Average-case Search সাধারণত কত?

A. O(n²)

B. O(log n)

C. O(1)

D. O(n!)

10\. Heap-এর গুরুত্বপূর্ণ ব্যবহার কোনটি?

A. Priority Queue

B. শুধু Text Editing

C. DNS-এর একমাত্র Structure

D. File Extension

11\. Recursion-এ Base Case-এর কাজ কী?

A. Function-কে সবসময় চালানো

B. Recursion থামানোর শর্ত দেওয়া

C. সব Variable মুছে ফেলা

D. Sorting করা

12\. কোনটি Divide and Conquer Algorithm-এর উদাহরণ?

A. Merge Sort

B. শুধু Linear Search

C. শুধু Queue

D. শুধু Hash Table

Check Answers

পরবর্তী লেসন: Lesson 19 — Computer Architecture, CPU, RAM/ROM, Cache, Number System, Binary Arithmetic ও Logic Gates। এগুলোও Technical MCQ পরীক্ষার গুরুত্বপূর্ণ ভিত্তি।
# লেসন ১৯: Computer Architecture, CPU, Memory, Number System ও Logic Gates

এই লেসনে Teletalk Bangladesh Limited-এর Technical Exam-এর জন্য Computer Fundamentals-এর গুরুত্বপূর্ণ বিষয়গুলো শিখব। বিশেষভাবে CPU, RAM/ROM, Cache Memory, Number System Conversion, Binary Arithmetic এবং Logic Gates নিয়ে আলোচনা করব।

## ১. Computer Architecture কী?

Computer Architecture হলো Computer-এর প্রধান অংশগুলো কীভাবে কাজ করে এবং একে অপরের সঙ্গে যোগাযোগ করে, তার ধারণা ও নকশা।

একটি সাধারণ Computer System-এর প্রধান অংশ:

Input Unit

Keyboard, Mouse, Scanner

CPU — Central Processing Unit

ALU

Arithmetic ও Logic

CU

Control Unit

Registers

দ্রুত Storage

Memory

RAM, ROM, Cache

Storage

SSD, HDD

Output Unit

Monitor, Printer, Speaker

## ২. CPU-এর প্রধান অংশ

CPU (Central Processing Unit) নির্দেশনা Execute করে এবং Computer-এর বিভিন্ন Operation নিয়ন্ত্রণ করে।

- ALU — Arithmetic Logic Unit: যোগ, বিয়োগ, তুলনা এবং AND/OR-এর মতো Logical Operation করে।
- CU — Control Unit: নির্দেশনা Fetch ও Decode করে এবং Execution-এর জন্য প্রয়োজনীয় Control Signal সমন্বয় করে।
- Registers: CPU-এর ভেতরে থাকা অতি দ্রুত ছোট Storage, যেখানে বর্তমান কাজের Data, Address বা Intermediate Result রাখা যায়।

### গুরুত্বপূর্ণ Register

| Register                      | কাজ                                                  |
| ----------------------------- | ---------------------------------------------------- |
| PC — Program Counter          | পরবর্তী Fetch করার নির্দেশনার Address রাখে           |
| IR — Instruction Register     | বর্তমানে প্রক্রিয়াধীন Instruction রাখে               |
| MAR — Memory Address Register | Memory Access-এর Address রাখে                        |
| MDR/MBR                       | Memory থেকে আসা বা Memory-তে যাওয়ার Data রাখে        |
| Accumulator                   | কিছু Architecture-এ Arithmetic/Logic Result ধরে রাখে |

### Instruction Cycle

সাধারণভাবে CPU Instruction Cycle-কে এভাবে বোঝানো যায়:

1. Fetch: Memory থেকে Instruction আনা।
2. Decode: Instruction-এর অর্থ ও প্রয়োজনীয় Operation নির্ধারণ।
3. Execute: Instruction অনুযায়ী কাজ সম্পন্ন করা।

কিছু Architecture-এ এর পাশাপাশি Memory Access ও Write-back-এর মতো অতিরিক্ত ধাপ থাকে।

MCQ Tip: ALU → Arithmetic ও Logic; CU → Control; PC → পরবর্তী Instruction-এর Address।

## ৩. RAM, ROM, Cache ও Secondary Storage

কম্পিউটারের সব Memory একই কাজ করে না।

[Close-up of a green computer RAM module with black memory chips on a white background](https://images.openai.com/static-rsc-4/BE8itLpGbf8BqugZjQSc-1h-eEr-r9K0-khCxDJn0WYQd4xQjwbDD4bfXq8cKtU7pe3qcyFDLJnGHliQmzme_gBF6GUUc6v1MjvOhZ6XlZE89un_l2A4B7UicOLsrFl_NGJbXhCbHvhunD9INCxkElKziT7gx4luubjj1dRZp4qyHrhgGZN8JZaHfUpB-skb?purpose=inline)

RAM — Random Access Memory

চলমান Program ও Data সাময়িকভাবে রাখে। এটি সাধারণত Volatile, অর্থাৎ বিদ্যুৎ চলে গেলে এর Data থাকে না।

[Category:Mask ROM - Wikimedia Commons](https://images.openai.com/static-rsc-4/THdoVD_UtfodBZ3Xwcd5tlnpA0roCrvZLAdx9l5QBWoUReT8h1_nLjvOWXbsUvy2UK7xu5mFoZW7VeJAWfidRWrDBTfvbBx1v9KLtZSzbda3gFyP-rhOqHElZNl-faG2NTGNs5FXNUquJpIB6ERFQazKDOuffrJGtbtR893Mdl0?purpose=inline)

ROM — Read-Only Memory

Non-volatile Memory। বিদ্যুৎ বন্ধ হলেও Data থাকে। Firmware সংরক্ষণে ROM ও সংশ্লিষ্ট Non-volatile Memory Technology ব্যবহৃত হয়।

[Pikuma: Exploring How Cache Memory Really Works](https://images.openai.com/static-rsc-4/EXAKqR2YRNrkbfoHrBTFL9lUdNLsjPzXADsWf976a-sUyJ02iDKqy_0i8r3JQCqN5MObr7VrJnlxblJfIUhOkn8jt7PJEzdEJNrDzv3bqWv428PQftsxbbz5qK0zgZu2puscGhNsQKlZPibZ8W6tN4J8Y25UN3EgxeDiU6oo60Y?purpose=inline)

Cache Memory

CPU-র কাছে থাকা দ্রুতগতির Memory। বারবার প্রয়োজন হতে পারে এমন Data ও Instruction রেখে Average Access Time কমাতে সাহায্য করে।

[SSD vs HDD: Wybór prawego napędu](https://images.openai.com/static-rsc-4/WtOoqi2IShqr-PJXRcCb4KWDoRuVlAG7Tme98t2hfnk29Y5qCe9-DYVJlqWfYgcqsX0m1flv-pLfye-lC0OapOpco08ykKG-yilAKyrw98iDCxg-PJ4gljRo2KI5hq39Ej0IdIsZmxE0VZe5LymOi3D4NeDeZuVY0vfgSWpZkzE?purpose=inline)

Secondary Storage

SSD ও HDD-এর মতো Storage-এ দীর্ঘমেয়াদে File ও Program রাখা হয়। সাধারণত বিদ্যুৎ বন্ধ হলেও Data সংরক্ষিত থাকে।

### Memory তুলনা

| বৈশিষ্ট্য  | RAM                | ROM           | Cache                | SSD/HDD               |
| ---------- | ------------------ | ------------- | -------------------- | --------------------- |
| প্রধান কাজ | চলমান Program/Data | Firmware/Data | CPU Access দ্রুত করা | দীর্ঘমেয়াদি Storage   |
| Volatile?  | সাধারণত হ্যাঁ      | না            | সাধারণত হ্যাঁ        | না                    |
| গতি        | দ্রুত              | ধরনভেদে ভিন্ন | সাধারণত খুব দ্রুত    | RAM/Cache-এর চেয়ে ধীর |
| Capacity   | সাধারণত GB         | ধরনভেদে       | তুলনামূলক ছোট        | সাধারণত বেশি          |

### Cache Level

- L1 Cache: সাধারণত সবচেয়ে ছোট ও দ্রুত।
- L2 Cache: L1-এর তুলনায় সাধারণত বড়।
- L3 Cache: অনেক Processor-এ L2-এর চেয়ে বড় এবং একাধিক Core-এর মধ্যে Shared হতে পারে।

সাধারণ ধারণা:

Registers → L1 Cache → L2 Cache → L3 Cache → RAM → SSD/HDD

উপরের দিকে সাধারণত গতি বেশি এবং Capacity কম; তবে নির্দিষ্ট Architecture অনুযায়ী বৈশিষ্ট্য ভিন্ন হতে পারে।

## ৪. Computer Architecture-এর ধরন

### Von Neumann Architecture

Instruction ও Data একই প্রধান Memory System-এ রাখা হয় এবং সাধারণত একই Bus ব্যবস্থা ব্যবহার করে আদান-প্রদান করা হয়।

### Harvard Architecture

Instruction ও Data-এর জন্য আলাদা Memory এবং আলাদা Access Path ব্যবহার করা হয়।

| বিষয়                      | Von Neumann        | Harvard                                          |
| ------------------------- | ------------------ | ------------------------------------------------ |
| Instruction ও Data Memory | সাধারণত একই        | আলাদা                                            |
| Access Path               | সাধারণত Shared     | আলাদা হতে পারে                                   |
| সম্ভাব্য সুবিধা           | সহজ ও নমনীয় Design | Instruction ও Data Access একসঙ্গে সম্ভব হতে পারে |

Von Neumann Bottleneck: Instruction ও Data একই Memory Path ব্যবহার করার কারণে সেই Path-এর Bandwidth Performance সীমিত করতে পারে।

### 32-bit বনাম 64-bit

- 64-bit Architecture সাধারণভাবে 32-bit-এর তুলনায় বড় Address ও Data নিয়ে কাজ করার সুবিধা দিতে পারে।
- 64-bit System বেশি Memory Address করতে পারে—তবে বাস্তব সীমা Processor, OS ও Hardware Implementation-এর ওপর নির্ভর করে।
- 64-bit মানেই সব কাজ দ্বিগুণ দ্রুত হবে, এমন নয়।

## ৫. Number System

Computer Fundamentals-এর পরীক্ষায় Decimal, Binary, Octal ও Hexadecimal খুব গুরুত্বপূর্ণ।

| Number System | Base | ব্যবহৃত Digit |
| ------------- | ---- | ------------- |
| Binary        | 2    | 0, 1          |
| Octal         | 8    | 0–7           |
| Decimal       | 10   | 0–9           |
| Hexadecimal   | 16   | 0–9, A–F      |

Hexadecimal-এ A = 10, B = 11, C = 12, D = 13, E = 14 এবং F = 15।

### Binary থেকে Decimal

উদাহরণ: \\((1011)\_2\\)

প্রতিটি Digit-কে তার Position অনুযায়ী \\(2\\)-এর Power দিয়ে গুণ করতে হয়।

\\[ (1011)\_2 = 1(2^3)+0(2^2)+1(2^1)+1(2^0) \\]

\\[ =8+0+2+1=\boxed{11} \\]

অর্থাৎ, \\((1011)\_2=(11)\_{10}\\)।

### Decimal থেকে Binary

উদাহরণ: \\((13)\_{10}\\)

2 দিয়ে বারবার ভাগ করে Remainder লিখি:

| ভাগ    | ভাগফল | Remainder |
| ------ | ----- | --------- |
| 13 ÷ 2 | 6     | 1         |
| 6 ÷ 2  | 3     | 0         |
| 3 ÷ 2  | 1     | 1         |
| 1 ÷ 2  | 0     | 1         |

Remainder নিচ থেকে ওপরে পড়লে পাওয়া যায় \\(1101\\)।

অতএব, \\((13)\_{10}=(1101)\_2\\)।

### Binary থেকে Octal

Binary সংখ্যাকে ডান দিক থেকে ৩ Bit করে Group করো।

\\[ (110101)\_2=(110\ 101)\_2 \\]

- \\(110_2=6\\)
- \\(101_2=5\\)

অতএব, \\((110101)\_2=(65)\_8\\)।

### Binary থেকে Hexadecimal

Binary সংখ্যাকে ডান দিক থেকে ৪ Bit করে Group করো।

\\[ (11010110)\_2=(1101\ 0110)\_2 \\]

- \\(1101_2=D\\)
- \\(0110_2=6\\)

অতএব, \\((11010110)\_2=(D6)\_{16}\\)।

## ৬. Binary Arithmetic

### Binary Addition

Binary-তে শুধু 0 ও 1 ব্যবহার করা হয়।

| যোগ       | ফল                  |
| --------- | ------------------- |
| 0 + 0     | 0                   |
| 0 + 1     | 1                   |
| 1 + 0     | 1                   |
| 1 + 1     | 10 (Sum 0, Carry 1) |
| 1 + 1 + 1 | 11 (Sum 1, Carry 1) |

উদাহরণ:

```
   101
 + 011
 -----
  1000
```

যাচাই: \\(5+3=8\\), আর \\(1000_2=8\_{10}\\)।

### Binary Subtraction

| বিয়োগ | ফল             |
| ----- | -------------- |
| 0 − 0 | 0              |
| 1 − 0 | 1              |
| 1 − 1 | 0              |
| 0 − 1 | Borrow নিতে হয় |

উদাহরণ:

```
   110
 - 011
 -----
   011
```

যাচাই: \\(6-3=3\\), অর্থাৎ \\(011_2=3\_{10}\\)।

### 1's Complement ও 2's Complement

- 1's Complement: প্রতিটি Bit উল্টে দেওয়া—0 হলে 1, 1 হলে 0।
- 2's Complement: প্রথমে 1's Complement, তারপর 1 যোগ করা।

উদাহরণ: 4-bit Binary \\(0101\\)।

```
Original:       0101
1's Complement: 1010
2's Complement: 1011
```

Fixed-width Signed Binary-তে 2's Complement ঋণাত্মক সংখ্যা প্রকাশের বহুল ব্যবহৃত পদ্ধতি।

গুরুত্বপূর্ণ: \\(n\\)-bit 2's Complement-এ Signed Integer-এর Range হলো:

\\[ -2^{n-1}\ \text{থেকে}\ 2^{n-1}-1 \\]

যেমন 8-bit Signed 2's Complement-এর Range: \\(-128\\) থেকে \\(127\\)।

## ৭. Logic Gates

Logic Gate হলো Digital Circuit-এর মৌলিক অংশ, যা Binary Input নিয়ে Logical Output তৈরি করে।

AND Gate

সব Input 1 হলে Output 1।

Boolean Expression: \\(Y=A\cdot B\\)

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

OR Gate

অন্তত একটি Input 1 হলে Output 1।

Boolean Expression: \\(Y=A+B\\)

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

NOT Gate

Input-এর বিপরীত Output দেয়।

Boolean Expression: \\(Y=\overline A\\)

| A | Y |
| - | - |
| 0 | 1 |
| 1 | 0 |

NAND Gate

AND Gate-এর Output উল্টে দেয়। Output শুধু তখন 0, যখন উভয় Input 1।

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

NOR Gate

OR Gate-এর Output উল্টে দেয়। Output 1 শুধু তখন, যখন উভয় Input 0।

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

XOR Gate

দুই Input আলাদা হলে Output 1।

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

XNOR Gate

দুই Input একই হলে Output 1। এটি XOR-এর Complement।

| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

MCQ Tip: NAND ও NOR হলো Universal Gates—শুধু NAND অথবা শুধু NOR ব্যবহার করে যেকোনো Boolean Function বাস্তবায়ন করা সম্ভব।

## ৮. দ্রুত Revision — পরীক্ষার আগে মনে রাখবে

| প্রশ্ন                                           | উত্তর                                                    |
| ------------------------------------------------ | -------------------------------------------------------- |
| CPU-এর পূর্ণরূপ কী?                              | Central Processing Unit                                  |
| ALU-এর কাজ কী?                                   | Arithmetic ও Logical Operation                           |
| CU-এর কাজ কী?                                    | Control ও Instruction Execution সমন্বয়                   |
| কোন Memory Volatile?                             | RAM                                                      |
| কোনটি সাধারণত সবচেয়ে দ্রুত?                      | CPU Register; এরপর Cache Hierarchy                       |
| L1, L2, L3 কী?                                   | Cache Memory Level                                       |
| Binary Number System-এর Base কত?                 | 2                                                        |
| Octal Number System-এর Base কত?                  | 8                                                        |
| Hexadecimal Number System-এর Base কত?            | 16                                                       |
| Hexadecimal-এ F-এর Decimal Value কত?             | 15                                                       |
| 2's Complement কীভাবে পাওয়া যায়?                 | 1's Complement-এর সঙ্গে 1 যোগ করে                        |
| AND Gate কখন 1 দেয়?                              | সব Input 1 হলে                                           |
| XOR Gate কখন 1 দেয়?                              | Input-গুলো আলাদা হলে                                     |
| Universal Gate কোন দুটি?                         | NAND ও NOR                                               |
| Von Neumann Architecture-এর প্রধান বৈশিষ্ট্য কী? | Instruction ও Data সাধারণত একই Memory System ব্যবহার করে |

## ৯. Lesson 19 — MCQ Practice Test

## ১২টি MCQ

0/12 answered

নিজে উত্তর নির্বাচন করে শেষে Check Answers চাপো।

1\. CPU-এর Arithmetic ও Logical Operation কোন অংশটি করে?

A. Control Unit

B. ALU

C. RAM

D. SSD

2\. কোনটি সাধারণত Volatile Memory?

A. RAM

B. SSD

C. HDD

D. ROM

3\. CPU-এর পরবর্তী Instruction-এর Address কোন Register-এ থাকে?

A. PC

B. IR

C. MDR

D. Accumulator সব Architecture-এ

4\. Binary 1011-এর Decimal মান কত?

A. 9

B. 10

C. 11

D. 12

5\. Decimal 13-এর Binary রূপ কোনটি?

A. 1010

B. 1101

C. 1110

D. 1001

6\. Hexadecimal-এ F-এর Decimal মান কত?

A. 10

B. 12

C. 14

D. 15

7\. Binary 110101-এর Octal রূপ কোনটি?

A. 65

B. 53

C. 61

D. 75

8\. 4-bit 2's Complement-এ Signed Integer-এর Range কত?

A. −7 থেকে 7

B. −8 থেকে 7

C. −8 থেকে 8

D. 0 থেকে 15

9\. AND Gate-এর Output কখন 1 হয়?

A. যেকোনো একটি Input 1 হলে

B. সব Input 0 হলে

C. সব Input 1 হলে

D. Input আলাদা হলে

10\. XOR Gate-এর Output কখন 1 হয়?

A. দুই Input একই হলে

B. দুই Input আলাদা হলে

C. সব Input 0 হলে

D. সবসময়

11\. Universal Gate কোন দুটি?

A. AND ও OR

B. XOR ও XNOR

C. NAND ও NOR

D. NOT ও AND

12\. Von Neumann Architecture-এর বৈশিষ্ট্য কোনটি?

A. Instruction ও Data-এর জন্য সবসময় আলাদা Memory

B. Instruction ও Data সাধারণত একই Memory System ব্যবহার করে

C. এতে CPU থাকে না

D. এটি শুধু Analog Computer-এর জন্য

Check Answers

পরবর্তী লেসন হবে Lesson 20: Digital Electronics, Boolean Algebra, Flip-Flops, Registers, Counters ও Microprocessor Basics—যা Computer Hardware ও Digital Logic-এর প্রস্তুতিকে আরও শক্ত করবে।

# Lesson 20: Digital Electronics, Boolean Algebra, Flip-Flops, Registers, Counters ও Microprocessor Basics

এই লেসনে Teletalk Bangladesh Limited-এর Technical Exam-এর প্রস্তুতির জন্য Digital Electronics-এর গুরুত্বপূর্ণ বিষয়গুলো সহজ বাংলায় শিখব। প্রতিটি টপিকে থাকবে সংজ্ঞা, উদাহরণ, পরীক্ষায় মনে রাখার মতো তথ্য এবং শেষে MCQ পরীক্ষা।

## 1. Digital Electronics কী?

Digital Electronics হলো এমন একটি ইলেকট্রনিকস শাখা যেখানে তথ্য সাধারণত দুটি বাইনারি মান দিয়ে প্রকাশ করা হয়:

- Logic 0 — LOW
- Logic 1 — HIGH

উদাহরণ: Computer, digital clock, calculator, mobile phone ও microprocessor-ভিত্তিক সিস্টেম।

Analog বনাম Digital

| বিষয়            | Analog                  | Digital                         |
| --------------- | ----------------------- | ------------------------------- |
| Signal          | Continuous              | Discrete                        |
| উদাহরণ          | Analog thermometer      | Digital thermometer             |
| Noise-এর প্রভাব | তুলনামূলক বেশি হতে পারে | অনেক ক্ষেত্রে noise সামলানো সহজ |
| তথ্য প্রকাশ     | Continuous value        | সাধারণত binary 0 ও 1            |

## 2. Boolean Algebra

Boolean Algebra-তে ভেরিয়েবলের মান সাধারণত 0 অথবা 1 হয়। Digital circuit-এর logic বিশ্লেষণ ও সরলীকরণে এটি ব্যবহার করা হয়।

এখানে:

- AND-কে লেখা হয় \\(A \cdot B\\)
- OR-কে লেখা হয় \\(A+B\\)
- NOT-কে লেখা হয় \\(\overline{A}\\)

### গুরুত্বপূর্ণ Boolean Laws

| Law               | সূত্র                                            |
| ----------------- | ------------------------------------------------ |
| Identity          | \\(A+0=A\\), \\(A\cdot1=A\\)                     |
| Null / Domination | \\(A+1=1\\), \\(A\cdot0=0\\)                     |
| Idempotent        | \\(A+A=A\\), \\(A\cdot A=A\\)                    |
| Complement        | \\(A+\overline A=1\\), \\(A\cdot\overline A=0\\) |
| Double Negation   | \\(\overline{\overline A}=A\\)                   |
| Commutative       | \\(A+B=B+A\\)                                    |
| Associative       | \\(A+(B+C)=(A+B)+C\\)                            |
| Distributive      | \\(A(B+C)=AB+AC\\)                               |

### De Morgan’s Theorem

পরীক্ষায় খুবই গুরুত্বপূর্ণ:

\\[ \overline{A\cdot B}=\overline A+\overline B \\]

\\[ \overline{A+B}=\overline A\cdot\overline B \\]

অর্থাৎ, AND-এর ওপর NOT দিলে OR হয় এবং প্রতিটি ইনপুটের ওপরও NOT বসে। একইভাবে OR-এর ওপর NOT দিলে AND হয়।

উদাহরণ: \\(\overline{A+B}\\) সরল করলে পাওয়া যায় \\(\overline A\cdot\overline B\\)।

## 3. Combinational বনাম Sequential Circuit

### Combinational Circuit

Output নির্ভর করে বর্তমান input-এর ওপর; সাধারণভাবে আগের state মনে রাখে না।

উদাহরণ: Adder, Subtractor, Multiplexer, Decoder, Encoder।

### Sequential Circuit

Output বর্তমান input-এর পাশাপাশি আগের state বা stored information-এর ওপরও নির্ভর করতে পারে।

উদাহরণ: Flip-flop, Register, Counter।

পরীক্ষার কৌশল: Memory বা state সংরক্ষণ করতে পারে — Sequential Circuit।

## 4. Flip-Flops

Flip-flop হলো একটি bistable digital circuit, যা সাধারণত ১ bit তথ্য সংরক্ষণ করতে পারে।

[File:SR (NAND) Flip-flop.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/iUi7AlDWT9Q8iyLfcgVlwpkFU48PNoqYKP4g_36v1xzaxjQmRYpvnnIdU-tVzWE1_xlfROlMJA92yvqHlgOMXhNSuQpQM8F5niCn2tMTGGL4kUrL6Ocag-xJz2pFWfJTL1Uq_QzGrmqkw3ZYcHqK8ZmAOXtg05KjON6umdvJSoY?purpose=inline)

SR Flip-Flop

S = Set, R = Reset। সাধারণ SR latch/flip-flop-এ দুই input একসঙ্গে active হলে কী হবে, তা নির্ভর করে circuit-এর ধরন ও implementation-এর ওপর; basic NOR-based SR latch-এ \\(S=R=1\\) হলো invalid condition।

[D Flip Flop: Definition, Working, Truth Table & Applications in Digital Electronics](https://images.openai.com/static-rsc-4/-zXbSysbJ_3OgaSSTJGn6FOqpx3eWJTrkKpBHldPhfiw5CXBgl4C1BxIy6LrnK6IZjfT44R3xSVxhYfVmDIW-tYuAXaVkAGI1tt_mt6Eiw0bVQclT1cncK3MxFMI7ZFOS2NZ_mzk8UJAkWRAC1RVbtdJ7YZOMSbyvlF8MhBBLTw?purpose=inline)

D Flip-Flop

D = Data। Active clock edge-এ input \\(D\\) সাধারণত output \\(Q\\)-তে সংরক্ষিত হয়। Register তৈরিতে ব্যবহৃত হয়।

[File:JK Flip-flop (Simple) Symbol.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/oQ-CHqoI-vEHi1lM6XllbyU6IWZ99UKN4VJosp7iDCLRGT83S--NcInY6vUAx2tjEdTGGjTlYQSrlR4B0GzulJqoI7xlg0v25YPKtY4Ije5NhVVWu8FwPiP5a7uONQtf2rDE2bsjqNNzhodVzpMs41h--BVAiPvp1yiYU1un4xE?purpose=inline)

JK Flip-Flop

SR-এর উন্নত সংস্করণ হিসেবে শেখানো হয়। \\(J=K=1\\) হলে output toggle করে।

[File:T-Type Flip-flop.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/0gY7EQrHjyP3Kd7jOHlij01fGX-gFSOr5P0naOgLmBKIAUKP_gxJgpJ00MxkhrOD6YVAF644SCGjUXnojt9uOu7uklzhmTb4D6vdZZ6wCFfj3EmE-2Hkeu3s06V-JrjIpk6oIOj02TsJXh7GHaYX8QM0fGaoCClox1rZdUBz1SQ?purpose=inline)

T Flip-Flop

T = Toggle। \\(T=1\\) হলে active clock edge-এ output আগের অবস্থার বিপরীত হয়। Counter-এ গুরুত্বপূর্ণ।

মনে রাখবে: একটি flip-flop সাধারণত ১ bit সংরক্ষণ করে; ৮টি bit সংরক্ষণের জন্য ৮-bit register-এ সাধারণত ৮টি flip-flop লাগে।

## 5. Registers

Register হলো একাধিক flip-flop-এর সমন্বয়ে তৈরি একটি ছোট, দ্রুত storage unit, যা CPU বা digital circuit-এর মধ্যে binary data ধরে রাখে।

উদাহরণ: 8-bit register সাধারণত 8টি bit সংরক্ষণ করতে পারে।

### Register-এর ধরন

| Register                      | কাজ                                               |
| ----------------------------- | ------------------------------------------------- |
| Accumulator (ACC)             | Arithmetic ও logic operation-এর ফল রাখে           |
| Program Counter (PC)          | পরবর্তী instruction-এর address ধরে রাখে           |
| Instruction Register (IR)     | বর্তমানে execute হওয়া instruction ধরে রাখে        |
| Memory Address Register (MAR) | Memory-তে যে address access করা হবে তা ধরে রাখে   |
| Memory Data Register (MDR)    | Memory থেকে আসা বা memory-তে যাওয়ার data ধরে রাখে |
| Shift Register                | Bit-কে বাম বা ডান দিকে shift করে                  |

### Shift Register-এর ধরন

- SISO: Serial In, Serial Out
- SIPO: Serial In, Parallel Out
- PISO: Parallel In, Serial Out
- PIPO: Parallel In, Parallel Out

মনে রাখবে: Serial মানে একবারে একটি bit; Parallel মানে একাধিক bit একসঙ্গে।

## 6. Counters

Counter হলো এমন একটি sequential circuit, যা clock pulse-এর সঙ্গে নির্দিষ্ট ক্রমে state পরিবর্তন করে গণনা করে।

[PPT - Digital Counter Operations: Asynchronous and Synchronous Design PowerPoint Presentation - ID:9519720](https://images.openai.com/static-rsc-4/GHqxmvcpUo-zk9PqcC3glNJwSSZ6y9YiybszBuVeXtAh-tvmmE7CO-Mb0QRzxcM2yPXKBNrcni0v97dOHo7Ti8viCuAF8zQB4DIydbBmmFqL6VIolKCZWuoCqTTI4i0wMe9q1k_3Y_wdF3QRyaZMqzNWhXp5ZE5mbpqn1O2eJk8?purpose=inline)

[4 BIT up Counter and BCD  Using Discrete Transistor](https://images.openai.com/static-rsc-4/MSzjwhsOzME2vPRYFuaRKaQQG8fzPK55Ve1gxZYwId8rh--TzC09E3Zqc3vy0n4S_DDIw_egLxrDrbbGdOK7exCE5aB-SR6VWvnZuF6KFIyfXsI3pepv-jqTTGTciO34ObTmVqiYMOVxxHjobgO5eTjN1kq0nW9XhYn2KPFTfvE?purpose=inline)

[Synchronous Counter | Tutorials on Electronics | Next Electronics](https://images.openai.com/static-rsc-4/1EvzogBeTA9sf3sRtoczuQee6HzqMRGpiVKOSqY3YbQ1vo623iUkI4U4VprQKjWkyBOgsO-1v7CMXlZBlC7ARnbbjPddnFatQpBSiZ4pKDodOWqVfTyMDBSV_56stwBNjvRpq-69kcZm8wiTFyUmq2EDHZQjZZEDbikuhhHYOFk?purpose=inline)

9

### Counter-এর ধরন

| ধরন                           | বৈশিষ্ট্য                                                     |
| ----------------------------- | ------------------------------------------------------------- |
| Asynchronous / Ripple Counter | সব flip-flop একই clock সরাসরি পায় না; পরিবর্তন ধাপে ধাপে ছড়ায় |
| Synchronous Counter           | সব flip-flop একই clock signal পায়                             |
| Up Counter                    | সংখ্যা বাড়ায়                                                  |
| Down Counter                  | সংখ্যা কমায়                                                   |
| Up/Down Counter               | দুই দিকেই গণনা করতে পারে                                      |
| Ring Counter                  | Shift register-এর state ঘুরিয়ে গণনা করে                       |
| Johnson Counter               | Inverted feedback ব্যবহার করে state পরিবর্তন করে              |

### গুরুত্বপূর্ণ Formula

\\(n\\)টি flip-flop দিয়ে সর্বোচ্চ binary state-এর সংখ্যা:

\\[ \boxed{2^n} \\]

উদাহরণ:

- 1-bit counter: \\(2^1=2\\) states
- 2-bit counter: \\(2^2=4\\) states
- 3-bit counter: \\(2^3=8\\) states
- 4-bit counter: \\(2^4=16\\) states

একটি সাধারণ 4-bit binary up counter-এর গণনা:

`0000 → 0001 → 0010 → 0011 → ... → 1111 → 0000`

MCQ মনে রাখবে: 4-bit binary counter-এর মোট state = 16।

## 7. Multiplexer, Demultiplexer, Encoder ও Decoder

Multiplexer (MUX)

অনেক input থেকে নির্বাচিত একটি input-কে output-এ পাঠায়।

উদাহরণ: 4-to-1 MUX-এ 4টি input থাকে এবং 1টি output থাকে।

[ƎXCLUSIVE ARCHITECTURE](https://images.openai.com/static-rsc-4/ANp_8r7o3zM1P6L6RUdI7QV4bPIGgWWsOI7z1lNok8iWuCv-T42ZC4bP4L6lgOA4B_WnRTjH2CdYy3dtWcdbTC9RJdF-CLvM_SsaskIW5zq2E5fbA_yNDhBlImb8MdvdcG-lsrqr9y9UgXfotvshfhOPuY3Zv2YF7KYCSa75Yt8?purpose=inline)

Demultiplexer (DEMUX)

একটি input-কে নির্বাচিত output line-এ পাঠায়।

উদাহরণ: 1-to-4 DEMUX-এ 1টি input এবং 4টি output থাকে।

[Encoder and Decoder | THE INSTRUMENT GURU](https://images.openai.com/static-rsc-4/1rvsCiegmmgN3VOL-o7VMXtB1Un19xYgYfSAgUDhYJEDvbGXeSvUxHZPAMUfkhgoeC1jC_Z6lrcmG-k5GAwyuS_8mhqdfUkCyLJqfZLrcFnIxSvrNSPLGsEY0NB7UoQgP_VRReZxZjSmAMB7MKQu9c0tuCy452nhJ8FckI5Q9Uw?purpose=inline)

Encoder

Input line-এর তথ্যকে coded binary output-এ রূপান্তর করে।

উদাহরণ: 8-to-3 encoder-এর 8টি input line-এর জন্য 3-bit code।

[Full Adder function using 3:8 Decoder - Study Guide with 74LS20 and 74LS138 | DeldSim - Online Electronics Simulator](https://images.openai.com/static-rsc-4/bOEO5t5QEzoRrnY_2lrUFRhpiDmdkWx2wb_8dWBnYV6p-J5L-hVp4NT3zdJapmlnm5-gmu4a6U436A0KcxzcBx71XjCBvMMuQRZpWSx8jWdHdo4yggZStY8lLaEj0qQuU_OEJabM-EtfgboggS41VGGVu8p49GCI1gkmgGFRNZg?purpose=inline)

Decoder

Binary input code অনুযায়ী নির্দিষ্ট output line সক্রিয় করে।

উদাহরণ: 3-to-8 decoder-এ 3টি input দিয়ে 8টি output-এর একটি নির্বাচন করা যায়।

Formula: \\(n\\)টি select/input bit দিয়ে সর্বোচ্চ \\(2^n\\)টি ভিন্ন selection বা code তৈরি করা যায়।

## 8. Microprocessor Basics

Microprocessor হলো একটি programmable electronic device, যেখানে CPU-এর প্রধান processing functions একটি integrated circuit-এ বাস্তবায়িত থাকে।

[Paper 1 Lesson 2.3 - CPU Architecture | Graded IB Computer Science Notes](https://images.openai.com/static-rsc-4/uYxUr1zokbPtHF0KRYPPr8BFiAQ2Y5d5mgm8xpjEGnIVitI87Ok4o_gpIUzOLFYb_Fkq3DXUC51fkjXY0-7IhabkTyWPoAmPA7Fsid-FlR6QXFxKA1Uj9YWVyVpitKsbKoSHh_4H4i0vE5qmE3jPsSYL82aM1hle4GvSwPzNG8M?purpose=inline)

[graded-cs-resources.github.io](https://graded-cs-resources.github.io/IB-Computer-Science-Notes/paper1/np2.3_architecture.html)

### প্রধান অংশ

- ALU (Arithmetic Logic Unit): যোগ, বিয়োগ, তুলনা ও logic operation করে।
- Control Unit (CU): Instruction execution নিয়ন্ত্রণ করে।
- Registers: CPU-এর ভেতরে দ্রুত data ও instruction-সংক্রান্ত তথ্য ধরে রাখে।
- Clock: নির্দিষ্ট timing অনুযায়ী operation সমন্বয় করে।
- Buses: CPU, memory ও অন্যান্য component-এর মধ্যে data, address এবং control signal বহন করে।

### Data Bus, Address Bus ও Control Bus

| Bus         | কাজ                                                     |
| ----------- | ------------------------------------------------------- |
| Data Bus    | Data বহন করে                                            |
| Address Bus | কোন memory location বা device access হবে তা নির্দেশ করে |
| Control Bus | Read, Write ইত্যাদি control signal বহন করে              |

পরীক্ষার গুরুত্বপূর্ণ নিয়ম:

- \\(n\\)-bit address bus দিয়ে সর্বোচ্চ \\(2^n\\)টি address তৈরি করা যায়।
- 16-bit address bus → \\(2^{16}=65,536\\)টি address।
- Byte-addressable memory হলে এটি 65,536 bytes বা 64 KiB address করতে পারে।
- 8-bit data bus একবারে 8 bit data বহন করতে পারে।

### Microprocessor বনাম Microcontroller

| Microprocessor                            | Microcontroller                                |
| ----------------------------------------- | ---------------------------------------------- |
| সাধারণত CPU processing-কেন্দ্রিক          | CPU, memory ও peripheral একই chip-এ থাকতে পারে |
| বাইরের memory/peripheral প্রয়োজন হতে পারে | Embedded control-এর জন্য অনেক কিছু chip-এ থাকে |
| উদাহরণ: Intel Core processor family       | উদাহরণ: ATmega328P, STM32 family               |

Microcontroller সাধারণত embedded systems-এ ব্যবহৃত হয়, যেমন sensor control, washing machine, smart meter ও IoT device।

## 9. দ্রুত Revision: পরীক্ষায় মনে রাখবে

| প্রশ্ন                                   | উত্তর                        |
| ---------------------------------------- | ---------------------------- |
| 1 flip-flop কত bit রাখে?                 | 1 bit                        |
| 8-bit register-এ সাধারণত কয়টি flip-flop? | 8                            |
| \\(J=K=1\\) হলে JK flip-flop কী করে?     | Toggle                       |
| \\(T=1\\) হলে T flip-flop কী করে?        | Toggle                       |
| 4-bit counter-এর state কয়টি?             | 16                           |
| 4-to-1 MUX-এ কয়টি input?                 | 4                            |
| 3-to-8 decoder-এ কয়টি output?            | 8                            |
| PC-এর পূর্ণরূপ কী?                       | Program Counter              |
| ALU-এর কাজ কী?                           | Arithmetic ও logic operation |
| Data bus কী বহন করে?                     | Data                         |
| Address bus কী নির্দেশ করে?              | Address                      |
| De Morgan’s theorem কোন বিষয়ে?           | Boolean expression সরলীকরণ   |

## Lesson 20: MCQ Test

প্রতিটি প্রশ্নের সঠিক উত্তর নির্বাচন করো। শেষে Check Answers চাপলে স্কোর ও ব্যাখ্যা দেখতে পারবে।

## ১২টি MCQ

0/12 answered

1\. একটি flip-flop সাধারণত কত bit সংরক্ষণ করে?

A. 1 bit

B. 2 bits

C. 4 bits

D. 8 bits

2\. J = K = 1 হলে JK flip-flop-এর output কী হয়?

A. সবসময় 0

B. সবসময় 1

C. Toggle করে

D. কোনো clock লাগে না

3\. 4-bit binary counter-এর মোট state কয়টি?

A. 4

B. 8

C. 16

D. 32

4\. কোন register পরবর্তী instruction-এর address ধরে রাখে?

A. IR

B. PC

C. MDR

D. ACC

5\. কোন circuit অনেক input থেকে একটি input নির্বাচন করে output-এ পাঠায়?

A. Decoder

B. Encoder

C. Multiplexer

D. Demultiplexer

6\. De Morgan’s theorem অনুযায়ী NOT(A + B) সমান কোনটি?

A. NOT A + NOT B

B. NOT A AND NOT B

C. A AND B

D. A OR B

7\. ALU-এর প্রধান কাজ কী?

A. ফাইল সংরক্ষণ

B. Network routing

C. Arithmetic ও logic operation

D. শুধু instruction decode

8\. 8-to-3 encoder-এর output কয় bit?

A. 2

B. 3

C. 8

D. 11

9\. Data bus-এর কাজ কী?

A. শুধু address পাঠানো

B. Data বহন করা

C. Clock তৈরি করা

D. বিদ্যুৎ উৎপাদন করা

10\. 16-bit address bus দিয়ে কতটি পৃথক address তৈরি করা যায়?

A. 16

B. 256

C. 32,768

D. 65,536

11\. নিচের কোনটি sequential circuit?

A. Adder

B. Multiplexer

C. Decoder

D. Counter

12\. SIPO-এর পূর্ণরূপ কী?

A. Serial In Parallel Out

B. Serial In Serial Out

C. Single Input Parallel Operation

D. Shift In Process Out

Check Answers

পরের ধাপ: Lesson 21 — Computer Networks Advanced, TCP/IP, Routing Protocols, Switching, VLAN, Subnetting ও Network Troubleshooting-এর পরীক্ষাভিত্তিক Revision।

# Lesson 21: Computer Networking — Advanced Revision

Teletalk Bangladesh Limited Technical Exam Preparation

এই লেসনে আমরা Computer Networking-এর গুরুত্বপূর্ণ বিষয়গুলো শিখব: TCP/IP, Routing Protocols, Switching, VLAN, Subnetting এবং Network Troubleshooting। প্রতিটি অংশে থাকবে সহজ ব্যাখ্যা, উদাহরণ, পরীক্ষার গুরুত্বপূর্ণ তথ্য ও MCQ।

## 1. TCP/IP Model

TCP/IP Model হলো network communication-এর জন্য ব্যবহৃত একটি layered model। প্রচলিতভাবে এর ৪টি layer শেখানো হয়।

4\. Application Layer

HTTP/HTTPS, DNS, DHCP, SMTP, FTP, SSH

3\. Transport Layer

TCP, UDP — Port number

2\. Internet Layer

IPv4, IPv6, ICMP, IP routing

1\. Network Access Layer

Ethernet, Wi-Fi, MAC address, physical transmission

### TCP বনাম UDP

| বৈশিষ্ট্য          | TCP                                                           | UDP                                                        |
| ------------------ | ------------------------------------------------------------- | ---------------------------------------------------------- |
| Connection         | Connection-oriented                                           | Connectionless                                             |
| Delivery guarantee | Acknowledgment ও retransmission দিয়ে নির্ভরযোগ্য delivery দেয় | Delivery guarantee দেয় না                                  |
| Ordering           | Data order বজায় রাখতে পারে                                    | Order guarantee করে না                                     |
| Overhead           | তুলনামূলক বেশি                                                | তুলনামূলক কম                                               |
| উদাহরণ             | HTTPS, SSH, email transfer                                    | DNS-এর সাধারণ query, real-time voice/video-তে বহুল ব্যবহৃত |

মনে রাখবে: TCP-এর 3-way handshake হলো `SYN → SYN-ACK → ACK`।

## 2. গুরুত্বপূর্ণ Network Port

| Port    | Protocol / Service   |
| ------- | -------------------- |
| 20/21   | FTP data / control   |
| 22      | SSH                  |
| 23      | Telnet               |
| 25      | SMTP                 |
| 53      | DNS                  |
| 67/68   | DHCP server / client |
| 80      | HTTP                 |
| 110     | POP3                 |
| 123     | NTP                  |
| 143     | IMAP                 |
| 161/162 | SNMP query / trap    |
| 443     | HTTPS                |
| 587     | SMTP submission      |
| 993     | IMAPS                |
| 995     | POP3S                |

পরীক্ষায় সবচেয়ে বেশি মনে রাখার মতো: 22 = SSH, 53 = DNS, 67/68 = DHCP, 80 = HTTP, 443 = HTTPS।

## 3. Switching: Layer 2 ও Layer 3

[Ethernet | CompTIA Network+ Certification Guide](https://images.openai.com/static-rsc-4/Q708xqCHyxlZLwdCA_DLECDGNbCWuZxtSsP1d7qvgL6w_IsSAPlxUb0aEObAibraHzwzfKEnY-HDwVlYGa__pvwr9ps9qrxYY3pLioAttW2m2zTaHzHLbwLoKkg8F_i5VnJVqSKWHWdEC2prFbSlGHBPfpoU_eaxGT4HIYOTy3U?purpose=inline)

Layer 2 Switch

- Data Link Layer-এ কাজ করে।
- MAC address ব্যবহার করে Ethernet frame forward করে।
- সাধারণত একই LAN-এর device-গুলোর মধ্যে communication করায়।

[Understanding the Difference Between Layer 2 and Layer 3 Switches](https://images.openai.com/static-rsc-4/BrIiqfUekUsFG8Q1QTfZqM-GggWd4xbDZPO8y3WumRtKNDWJcLY-uAd28QNK9cD7M8VkSpcpLPEjrnInjtHq6qFSJtkFDTiXahbxXsF9X1OCKCVYL1hi0bXXk43IGIF4yM4nQK7vtsKaZclet_kPpLRO5tR8jCu2ogX5p3kXT2Y?purpose=inline)

Layer 3 Switch

- Switching-এর পাশাপাশি IP routing করতে পারে।
- VLAN-এর মধ্যে communication করাতে পারে, যদি routing ও policy configure করা থাকে।
- বড় LAN-এ inter-VLAN routing-এ ব্যবহৃত হয়।

### MAC Address কী?

MAC address হলো network interface-এর Data Link Layer-এ ব্যবহৃত address। Ethernet MAC address সাধারণত 48 bit বা 6 byte।

উদাহরণ: `00:1A:2B:3C:4D:5E`

- Switch MAC address দেখে frame forward করে।
- Router IP address ও routing table ব্যবহার করে packet forward করে।
- ARP IPv4 network-এ local link-এর IP address-এর সঙ্গে MAC address মেলাতে সাহায্য করে।

## 4. VLAN (Virtual LAN)

VLAN হলো একটি physical switched network-কে একাধিক logical Layer 2 broadcast domain-এ ভাগ করার পদ্ধতি।

[802.1Q Trunking Explained | CCNA 200-301](https://images.openai.com/static-rsc-4/dhRHZ6Icgz73vIcWwh1uJyhJ4ArIfMlkX4woe8eFT91rM1aGOFkR60MtUbhtF550-iyWwfgWz2T8wdyUZL8G6itSduYvXVWhRBaRKTsDNYylUURe7ANxUou9s0uP1mzRd83_1cUEHbP0MFbm7Sp7Q__EOSmQAWqote3Vba3DY-k?purpose=inline)

[pingmynetwork.com](https://pingmynetwork.com/network/ccna-200-301/802-1q-trunking)

ধরা যাক একটি অফিসে:

- VLAN 10 = Accounts Department
- VLAN 20 = IT Department
- VLAN 30 = CCTV Network

VLAN ব্যবহার করলে আলাদা logical network তৈরি করা যায়। তবে আলাদা VLAN-এর মধ্যে communication-এর জন্য সাধারণত router বা Layer 3 switch প্রয়োজন।

### Access Port বনাম Trunk Port

| Access Port                                             | Trunk Port                           |
| ------------------------------------------------------- | ------------------------------------ |
| সাধারণত একটি নির্দিষ্ট VLAN-এর untagged traffic বহন করে | একাধিক VLAN-এর traffic বহন করতে পারে |
| End-device যেমন PC-এর জন্য ব্যবহৃত হয়                   | Switch-to-switch link-এ বহুল ব্যবহৃত |
| সাধারণত end device-কে একটি VLAN-এ যুক্ত করে             | IEEE 802.1Q tagging বহুল ব্যবহৃত     |

Exam fact: IEEE 802.1Q হলো Ethernet frame-এ VLAN tagging-এর প্রচলিত standard।

## 5. IP Subnetting

Subnetting হলো একটি IP network-কে ছোট ছোট network বা subnet-এ ভাগ করা।

IPv4 address হলো 32 bit। যেমন:

`192.168.1.10/24`

এখানে:

- IP address: `192.168.1.10`
- `/24` হলো CIDR prefix
- Subnet mask: `255.255.255.0`
- Network address: `192.168.1.0`
- Broadcast address: `192.168.1.255`
- সাধারণ usable host range: `192.168.1.1 – 192.168.1.254`

### Common Subnet Mask Table

| CIDR  | Subnet Mask     | মোট Address | সাধারণ Usable Host |
| ----- | --------------- | ----------- | ------------------ |
| `/24` | 255.255.255.0   | 256         | 254                |
| `/25` | 255.255.255.128 | 128         | 126                |
| `/26` | 255.255.255.192 | 64          | 62                 |
| `/27` | 255.255.255.224 | 32          | 30                 |
| `/28` | 255.255.255.240 | 16          | 14                 |
| `/29` | 255.255.255.248 | 8           | 6                  |
| `/30` | 255.255.255.252 | 4           | 2                  |

এগুলো সাধারণ IPv4 subnet-এর হিসাব; বিশেষ ক্ষেত্রে usable address-এর নিয়ম আলাদা হতে পারে।

### Subnetting Formula

যদি host bit-এর সংখ্যা \\(h\\) হয়, তাহলে সাধারণ subnet-এ:

\\[ \text{Total addresses}=2^h \\]

\\[ \text{Usable hosts}=2^h-2 \\]

উদাহরণ: `/26`-এ host bit = \\(32-26=6\\)।

\\[ 2^6=64 \\]

সাধারণ usable host = \\(64-2=\boxed{62}\\)।

### Private IPv4 Address Ranges

| Range                           | CIDR             |
| ------------------------------- | ---------------- |
| `10.0.0.0 – 10.255.255.255`     | `10.0.0.0/8`     |
| `172.16.0.0 – 172.31.255.255`   | `172.16.0.0/12`  |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` |

এই address-গুলো private network-এ ব্যবহৃত হয়। Internet-এ সরাসরি public IPv4 address হিসেবে routable নয়; সাধারণত NAT-এর মতো ব্যবস্থা প্রয়োজন হয়।

## 6. Routing ও Routing Protocols

Router এক network থেকে অন্য network-এ IP packet forward করে। কোন পথে packet যাবে, তা নির্ধারণে routing table ব্যবহৃত হয়।

### Static বনাম Dynamic Routing

| Static Routing                           | Dynamic Routing                         |
| ---------------------------------------- | --------------------------------------- |
| Administrator route configure করেন       | Router routing protocol দিয়ে route শেখে |
| ছোট ও স্থিতিশীল network-এ কার্যকর        | বড় বা পরিবর্তনশীল network-এ সুবিধাজনক   |
| Route পরিবর্তনে manual update লাগতে পারে | Protocol অনুযায়ী route update হতে পারে  |

### গুরুত্বপূর্ণ Routing Protocol

| Protocol | বৈশিষ্ট্য                                                                           |
| -------- | ----------------------------------------------------------------------------------- |
| RIP      | Distance-vector; hop count ব্যবহার করে; সর্বোচ্চ 15 hop usable                      |
| OSPF     | Link-state; shortest-path calculation-এর জন্য SPF algorithm ব্যবহার করে             |
| BGP      | Autonomous System-এর মধ্যে routing-এর জন্য ব্যবহৃত; Internet routing-এ গুরুত্বপূর্ণ |
| EIGRP    | Advanced distance-vector/hybrid বৈশিষ্ট্যসম্পন্ন Cisco-উদ্ভূত protocol              |

Exam facts:

- RIP-এর maximum usable hop count = 15; 16 hop-কে unreachable হিসেবে গণ্য করা হয়।
- OSPF-এর পূর্ণরূপ = Open Shortest Path First।
- BGP-এর পূর্ণরূপ = Border Gateway Protocol।
- Default gateway হলো local network-এর বাইরে traffic পাঠানোর জন্য ব্যবহৃত router বা Layer 3 interface।

## 7. Network Troubleshooting Commands

Network সমস্যা হলে ধাপে ধাপে পরীক্ষা করতে হয়।

### প্রয়োজনীয় Commands

1\. `ping 8.8.8.8`

IP connectivity এবং response time পরীক্ষা করে। Ping reply না পেলেই যে network পুরোপুরি বন্ধ, তা নিশ্চিত নয়।

2\. `ip addr`

Linux-এ network interface ও IP address দেখায়।

3\. `ip route`

Linux routing table এবং default route দেখায়।

4\. `traceroute google.com`

Destination পর্যন্ত পথে থাকা network hops শনাক্ত করতে সাহায্য করে।

5\. `nslookup google.com`

DNS query করে domain name-এর সঙ্গে সংশ্লিষ্ট record পরীক্ষা করে।

6\. `ss -tuln`

Linux-এ listening TCP/UDP socket ও সংশ্লিষ্ট port দেখায়।

7\. `ip neigh`

Linux-এ local network-এর neighbor/ARP তথ্য দেখায়।

### বাস্তব উদাহরণ: Website খুলছে না

এই ক্রমে পরীক্ষা করতে পারো:

1. `ip addr` — ডিভাইসের IP address আছে কি?
2. `ip route` — default gateway আছে কি?
3. `ping <gateway-ip>` — local gateway-তে পৌঁছানো যাচ্ছে কি?
4. `ping 8.8.8.8` — IP connectivity আছে কি?
5. `nslookup google.com` — DNS resolution হচ্ছে কি?
6. `traceroute google.com` — পথে কোথায় সমস্যা হতে পারে?

এগুলো troubleshooting-এর সহায়ক পরীক্ষা; firewall, ICMP filtering বা network policy-এর কারণে কিছু command-এর ফল বিভ্রান্তিকর হতে পারে।

## 8. Network Security-এর অতিরিক্ত Revision

- Firewall: Network traffic নির্দিষ্ট rule অনুযায়ী allow বা block করে।
- VPN: Encrypted tunnel ব্যবহার করে network traffic সুরক্ষিতভাবে বহন করতে পারে।
- HTTPS: HTTP-এর সঙ্গে TLS ব্যবহার করে communication সুরক্ষিত করে।
- SNMP: Network device monitoring ও management-এ ব্যবহৃত হয়।
- NTP: Device-এর clock time synchronize করতে ব্যবহৃত হয়।
- QoS: Network traffic-কে priority বা policy অনুযায়ী পরিচালনা করে।
- NAT: IP address translation করে; IPv4 network-এ বহুল ব্যবহৃত।

## Lesson 21: MCQ Test

## Networking Quiz

0/12 answered

1\. TCP/IP model-এর প্রচলিত layer কয়টি?

A. 3

B. 4

C. 5

D. 7

2\. HTTPS-এর default port কোনটি?

A. 21

B. 22

C. 80

D. 443

3\. Layer 2 switch প্রধানত কোন address ব্যবহার করে?

A. IP address

B. MAC address

C. Port number

D. Domain name

4\. VLAN-এর প্রধান উদ্দেশ্য কী?

A. CPU speed বাড়ানো

B. একটি switched network-কে logical broadcast domain-এ ভাগ করা

C. IP address-কে domain name-এ রূপান্তর করা

D. Data compress করা

5\. /26 subnet-এ সাধারণ usable host কয়টি?

A. 30

B. 32

C. 62

D. 64

6\. RIP-এর সর্বোচ্চ usable hop count কত?

A. 7

B. 15

C. 16

D. 255

7\. Internet-এর inter-AS routing-এ কোন protocol গুরুত্বপূর্ণ?

A. ARP

B. DHCP

C. BGP

D. FTP

8\. DNS query পরীক্ষা করতে কোন command ব্যবহার করা যায়?

A. nslookup

B. mkdir

C. chmod

D. whoami

9\. DHCP server/client-এর সাধারণ UDP port কোন জোড়া?

A. 20/21

B. 22/23

C. 67/68

D. 80/443

10\. Linux-এ routing table দেখতে কোন command ব্যবহার করা যায়?

A. ip route

B. ip addr

C. pwd

D. cat /etc/passwd

11\. OSPF কোন ধরনের routing protocol?

A. Link-state

B. শুধু path-vector

C. Application protocol

D. Transport protocol

12\. IPv4 private address range কোনটি?

A. 8.8.8.0/24

B. 172.16.0.0/12

C. 1.1.1.0/24

D. 224.0.0.0/4

Check Answers

পরবর্তী লেসন: Lesson 22 — Telecom Core Network, LTE/4G Architecture, EPC, VoLTE, 5G Core ও গুরুত্বপূর্ণ Telecom MCQ।

# Lesson 22: Telecom Core Network — LTE/4G, EPC, VoLTE ও 5G Core

Teletalk Bangladesh Limited Technical Exam Preparation

এই লেসনে মোবাইল অপারেটরের Core Network কীভাবে কাজ করে, 4G LTE-তে কোন network element কী দায়িত্ব পালন করে, VoLTE কীভাবে voice call পরিচালনা করে এবং 5G Core-এর গুরুত্বপূর্ণ component-গুলো শিখব।

## 1. Mobile Network-এর সামগ্রিক Architecture

একটি মোবাইল নেটওয়ার্ককে সহজভাবে চারটি অংশে বোঝা যায়।

UE — User Equipment

Mobile phone, SIM, modem

Radio Access Network (RAN)

BTS / NodeB / eNodeB / gNodeB

Core Network

Authentication, mobility, session ও data routing

External Networks

Internet, অন্য operator, PSTN

- UE: ব্যবহারকারীর mobile device।
- RAN: মোবাইলের সঙ্গে radio communication করে।
- Core Network: ব্যবহারকারীকে authenticate করে, mobility ও connection পরিচালনা করে এবং service access নিশ্চিত করে।
- External Network: Internet বা অন্য telephone network।

মনে রাখবে: RAN হলো radio access-এর অংশ; Core Network হলো service, control ও connectivity পরিচালনার কেন্দ্রীয় অংশ।

## 2. 2G, 3G, 4G ও 5G-এর গুরুত্বপূর্ণ Network Elements

| Generation | Radio Access Element | গুরুত্বপূর্ণ Core Elements    |
| ---------- | -------------------- | ----------------------------- |
| 2G GSM     | BTS, BSC             | MSC, HLR, VLR, AuC            |
| 3G UMTS    | NodeB, RNC           | MSC, SGSN, GGSN               |
| 4G LTE     | eNodeB               | MME, SGW, PGW, HSS            |
| 5G NR      | gNodeB               | AMF, SMF, UPF, UDM, AUSF, PCF |

Exam shortcut:

- 2G → BTS
- 3G → NodeB
- 4G → eNodeB
- 5G → gNodeB

4G LTE-তে সাধারণত EPC (Evolved Packet Core) ব্যবহৃত হয়। 5G Standalone network-এ 5G Core (5GC) ব্যবহৃত হয়।

## 3. LTE ও EPC Architecture

LTE হলো 4G mobile communication-এর একটি গুরুত্বপূর্ণ technology। এর packet-based core architecture-এর নাম Evolved Packet Core (EPC)।

[LTE EPC Core Network Components and Functionality | Shah Yar Hussaini posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/QxSMYCY54XU_dMqfUmJ3H5l6h9FwDI8KQTNdvrh_dOrLOdWvx0MTIxihMuhpRyRAqM3btEP1AppmSkdI70qtZp1Qh_9onFjUgpS4PvmqSgohiVH6Ft5GFZrZfNbSTqqQGnmZ8zHgQ9EPmbb_SaF9c69qVLP572YOyUrPfFcHPkY?purpose=inline)

[linkedin.com](https://www.linkedin.com/posts/shahyars_lte-epc-evolved-packet-core-is-the-activity-7424482044010852353-Rzdp)

### EPC-এর প্রধান Component

[Network sharing explained! - Community](https://images.openai.com/static-rsc-4/K-JTbz3QRzB2gZVbsewwNy7OfTwWmZdn1N68UyAhXlqmJiyGYFduXWFL-DmSS1pGRQD90vCQ4vaVPFkuan9TsSUsJdGXapAA9sYOhxDcf0Q1VvxwniuhzzzWPVLnRmWZbT4uJQGKsewhn82PbM-1uz5nU4HWdPZ9Ni5B9xTWzeg?purpose=inline)

MME — Mobility Management Entity

Control-plane component। UE-এর mobility management, NAS signalling এবং authentication-related signalling সমন্বয় করে।

[Block Diagram Of Lte System Architecture Lte Network Core Ar](https://images.openai.com/static-rsc-4/hOO0lLguVgEt_saYnDIVsF4egmGfvcrX6udj4oz82TRLHDUrJcA8qVBT9_vS0z0nvqBr-oweMMtCXwcDvtw83UkExT_BUjoVc9w4RZeV6aMs8IRUF-hUswHOKDzI8jONxzdgnVE9-oN5RoMFxV9oMSWTZz7TeFE5I_mVwf4JfSs?purpose=inline)

SGW — Serving Gateway

LTE radio access network ও EPC-এর মধ্যে user-plane traffic forward করে এবং mobility-সংক্রান্ত traffic handling-এ অংশ নেয়।

[Edge Router vs Firewall: What's the Real Difference?](https://images.openai.com/static-rsc-4/OzgTcRkvVSSGZHHLZ7Vgce88_0btEafZGqZJj777I_gYdJ6M2ALpbKGvjsFq6iswoLoG_nbsKsD2fhsKoBf5BrCFLwrxx0PbwFCQjtb-wvXWyxeNWU4hIzygwrIyxYxAgC_WpTaKinPrGlF3g1qzgC8XUUTtRrDLxT-DwZhJn_4?purpose=inline)

PGW / P-GW — PDN Gateway

External packet data network, যেমন Internet-এর সঙ্গে connectivity দেয়। IP address allocation ও policy/charging enforcement-এও ভূমিকা রাখে।

[LTE architecture: access network (eUTRAN) and core network (EPC) entities  | Download Scientific Diagram](https://images.openai.com/static-rsc-4/U77Ia9bKvbvI110gyHMc54HZYgcPj1fgXZEtq19fz4ZSsmQmKMS5_zWeCF28rit7zKk3iybFCRiDkegHWSkLLav7eCzzJA1aK64AyI0ik2YfSLqLG4aG0dTvG6Py-ktQa9W1Si5vEyCPR-JOBqOZvetgYkASTDvnOWRdcXnw7C8?purpose=inline)

HSS — Home Subscriber Server

Subscriber-এর পরিচয়, subscription ও authentication-সংক্রান্ত তথ্য সংরক্ষণ করে।

### Control Plane বনাম User Plane

- Control Plane: Signalling, registration, authentication ও mobility/session control।
- User Plane: ব্যবহারকারীর প্রকৃত data packet, যেমন web browsing ও video traffic।

খুব গুরুত্বপূর্ণ: MME মূলত control plane-এর অংশ; SGW ও PGW user-plane traffic পরিচালনায় গুরুত্বপূর্ণ ভূমিকা পালন করে।

## 4. LTE Interface ও Protocol

পরীক্ষায় network element-এর নামের পাশাপাশি তাদের মধ্যে communication-এর interface-ও আসতে পারে।

| Interface | সংযোগ                         | প্রধান ব্যবহার                                      |
| --------- | ----------------------------- | --------------------------------------------------- |
| Uu        | UE ↔ eNodeB                   | Radio interface                                     |
| S1-MME    | eNodeB ↔ MME                  | Control-plane signalling                            |
| S1-U      | eNodeB ↔ SGW                  | User-plane data                                     |
| S5/S8     | SGW ↔ PGW                     | User-plane forwarding ও সংশ্লিষ্ট control           |
| S6a       | MME ↔ HSS                     | Subscriber data ও authentication-related signalling |
| SGi       | PGW ↔ external packet network | Internet/PDN connectivity                           |

মনে রাখবে:

- S1-MME = Control
- S1-U = User data
- S6a = MME–HSS

## 5. VoLTE কী?

VoLTE-এর পূর্ণরূপ Voice over LTE। এটি LTE network-এর ওপর IP-based voice service প্রদান করে।

আগের network-এ voice call-এর জন্য circuit-switched ব্যবস্থা ব্যবহৃত হতো। VoLTE-তে voice packet হিসেবে LTE network দিয়ে চলাচল করে এবং সাধারণত IMS (IP Multimedia Subsystem) voice service নিয়ন্ত্রণ করে।

[IMS | ShareTechnote](https://images.openai.com/static-rsc-4/18C4BxAaWAF7hmv1mMyTsTx-sOu0KoQqw067_70DcJMoHqfEKcyIQpb_YBBabunPENi_h-6xjelDCJ7MvQn1Q85dTs_gLuGmaEIEBweFcHDiZIfDdP4Fl-yjOrUT0B9wdCAMML9vw6uuotxeLGmvfJkCHQvVt3CvkQWZmSlt_S0?purpose=inline)

[sharetechnote.com](https://sharetechnote.com/html/IMS_SIP_OverallDatapath.html)

### VoLTE-এর সুবিধা

- HD Voice সমর্থন করতে পারে।
- Call setup দ্রুত হতে পারে।
- Voice call-এর সময় LTE data connection ব্যবহার করা যায়।
- IMS-এর মাধ্যমে voice ও multimedia service পরিচালিত হয়।

### IMS-এর গুরুত্বপূর্ণ Component

| Component | কাজ                                                                          |
| --------- | ---------------------------------------------------------------------------- |
| P-CSCF    | IMS-এর সঙ্গে UE-এর প্রথম signalling contact point                            |
| I-CSCF    | Incoming SIP signalling-এর উপযুক্ত serving network element খুঁজতে সহায়তা করে |
| S-CSCF    | SIP session control ও subscriber service handling                            |
| HSS       | Subscriber profile ও authentication-related তথ্য                             |
| SIP       | Session setup, modification ও termination signalling                         |

Exam fact: SIP-এর পূর্ণরূপ Session Initiation Protocol। VoLTE-তে SIP signalling-এর জন্য ব্যবহৃত হয়।

## 6. 5G Core Network (5GC)

5G Core হলো 5G Standalone (SA) network-এর core architecture। এটি service-based architecture (SBA) ব্যবহার করে।

[What Is 5G Network Architecture? | Digi International](https://images.openai.com/static-rsc-4/YVjufWaP8mrXzQ8bSEA65lnbIkImycSXueJ3GdPYv4kjQ6dyXAxOgffhU_3wIgay-3hfrColZlwLZJfyilC_R077JYxP7QJeyFM3Pt4FvOOnC_HQNwxz-qUqA42K8HyHm6gLHbcElz4fEBy7eXGjSJIHxNuxiHFNR688oedvifI?purpose=inline)

[digi.com](https://www.digi.com/blog/post/5g-network-architecture)

### 5G Core-এর গুরুত্বপূর্ণ Network Functions

| Component | পূর্ণরূপ                                | প্রধান কাজ                                                     |
| --------- | --------------------------------------- | -------------------------------------------------------------- |
| AMF       | Access and Mobility Management Function | Registration, access ও mobility management                     |
| SMF       | Session Management Function             | PDU session পরিচালনা ও UPF control                             |
| UPF       | User Plane Function                     | User data packet forwarding                                    |
| UDM       | Unified Data Management                 | Subscriber data management                                     |
| AUSF      | Authentication Server Function          | Authentication service                                         |
| PCF       | Policy Control Function                 | Policy rules ও decision                                        |
| NRF       | Network Repository Function             | Network function discovery                                     |
| NSSF      | Network Slice Selection Function        | উপযুক্ত network slice নির্বাচন                                 |
| NEF       | Network Exposure Function               | নির্দিষ্ট network capability নিরাপদভাবে expose করতে সহায়তা করে |

### 4G বনাম 5G Core

| 4G EPC             | 5G Core                                         |
| ------------------ | ----------------------------------------------- |
| MME                | AMF-এর কিছু দায়িত্বের সঙ্গে তুলনীয়              |
| SGW/PGW user plane | UPF                                             |
| HSS                | UDM এবং সংশ্লিষ্ট authentication functions      |
| EPC architecture   | Service-based architecture                      |
| LTE access         | 5G NR access-এর সঙ্গে SA architecture-এ ব্যবহৃত |

এগুলো দায়িত্বের তুলনা; 4G component-কে 5G component-এর সম্পূর্ণ এক-এক সমতুল্য ধরে নেওয়া ঠিক নয়।

গুরুত্বপূর্ণ পার্থক্য: 5G NSA (Non-Standalone) network LTE anchor ও EPC ব্যবহার করতে পারে; 5G SA (Standalone) network 5G Core ব্যবহার করে।

## 7. Telecom Signalling ও Subscriber Identity

| Term     | পূর্ণরূপ / অর্থ                                          | কাজ                                                               |
| -------- | -------------------------------------------------------- | ----------------------------------------------------------------- |
| IMSI     | International Mobile Subscriber Identity                 | Subscriber identity                                               |
| IMEI     | International Mobile Equipment Identity                  | Mobile equipment identity                                         |
| MSISDN   | Mobile Station International Subscriber Directory Number | ব্যবহারকারীর dialable phone number                                |
| SIM      | Subscriber Identity Module                               | Subscriber credentials ও সংশ্লিষ্ট তথ্য                           |
| HLR      | Home Location Register                                   | 2G/3G subscriber ও location-related database                      |
| VLR      | Visitor Location Register                                | Serving area-তে subscriber-এর অস্থায়ী তথ্য                        |
| HSS      | Home Subscriber Server                                   | LTE/EPC subscriber database                                       |
| SS7      | Signalling System No. 7                                  | Traditional telecom signalling system                             |
| Diameter | Telecom signalling protocol                              | LTE/EPC-তে authentication ও policy-সংক্রান্ত signalling-এ ব্যবহৃত |

মনে রাখবে:

- IMSI → Subscriber
- IMEI → Equipment
- MSISDN → Phone number
- SS7 → Traditional telecom signalling
- Diameter → LTE/EPC-তে গুরুত্বপূর্ণ signalling protocol

## 8. Teletalk Technical Exam: দ্রুত Revision

| প্রশ্ন                                      | সঠিক উত্তর          |
| ------------------------------------------- | ------------------- |
| LTE-এর radio base station কী?               | eNodeB              |
| EPC-এর পূর্ণরূপ কী?                         | Evolved Packet Core |
| MME কোন plane-এ কাজ করে?                    | Control plane       |
| LTE user-plane gateway কোনগুলো?             | SGW ও PGW           |
| LTE subscriber database কী?                 | HSS                 |
| VoLTE-এর পূর্ণরূপ কী?                       | Voice over LTE      |
| VoLTE-তে session signalling-এর protocol কী? | SIP                 |
| 5G Core-এর mobility function কী?            | AMF                 |
| 5G Core-এর session management function কী?  | SMF                 |
| 5G Core-এর user-plane function কী?          | UPF                 |
| 5G subscriber data function কী?             | UDM                 |
| 5G authentication function কী?              | AUSF                |
| IMSI কী শনাক্ত করে?                         | Subscriber          |
| IMEI কী শনাক্ত করে?                         | Mobile equipment    |
| 5G SA কোন core ব্যবহার করে?                 | 5G Core             |

## Lesson 22: MCQ Test

নিজে উত্তর দাও, তারপর Check Answers চাপো। প্রতিটি উত্তরের সঙ্গে ব্যাখ্যাও দেখতে পারবে।

## Telecom Core Network Quiz

0/12 answered

1\. LTE-এর base station-কে কী বলা হয়?

A. BTS

B. NodeB

C. eNodeB

D. gNodeB

2\. EPC-এর পূর্ণরূপ কী?

A. Enhanced Packet Connection

B. Evolved Packet Core

C. Electronic Protocol Control

D. Evolved Public Connection

3\. LTE-তে প্রধানত কোনটি control-plane component?

A. MME

B. SGW

C. PGW

D. UPF

4\. LTE-তে Internet connectivity প্রদানে কোন gateway গুরুত্বপূর্ণ?

A. HSS

B. MME

C. PGW

D. AuC

5\. VoLTE-এর পূর্ণরূপ কী?

A. Voice over Local Ethernet

B. Video over LTE

C. Voice over LTE

D. Virtual Operator LTE

6\. IMS-এ session signalling-এর জন্য কোন protocol ব্যবহৃত হয়?

A. SIP

B. FTP

C. ARP

D. DHCP

7\. 5G Core-এ Access and Mobility Management Function কোনটি?

A. SMF

B. AMF

C. UPF

D. PCF

8\. 5G Core-এ user-plane packet forwarding-এর দায়িত্ব কোনটির?

A. UDM

B. AUSF

C. UPF

D. NRF

9\. 5G Core-এ session management function কোনটি?

A. SMF

B. AMF

C. HSS

D. PCF

10\. IMSI কী শনাক্ত করে?

A. Mobile equipment

B. Subscriber

C. Wi-Fi network

D. Cell tower

11\. LTE interface S1-U প্রধানত কী বহন করে?

A. User-plane data

B. Subscriber billing record only

C. DNS query only

D. SIP registration only

12\. 5G Standalone architecture কোন core ব্যবহার করে?

A. শুধু 2G core

B. শুধু 3G core

C. EPC বাধ্যতামূলক

D. 5G Core

Check Answers

পরবর্তী লেসন: Lesson 23 — Optical Fiber Communication, GPON/FTTH, OLT/ONT, Optical Power Budget, Attenuation, Splicing ও Telecom Transmission MCQ।

# Lesson 23: Optical Fiber Communication, GPON/FTTH, OLT/ONT ও Optical Power Budget

Teletalk Bangladesh Limited Technical Exam Preparation

এই লেসনে শিখব কীভাবে optical fiber দিয়ে data পাঠানো হয়, FTTH/GPON network কীভাবে কাজ করে, OLT ও ONT-এর পার্থক্য কী, এবং optical power budget ও attenuation-এর হিসাব কীভাবে করতে হয়।

## 1. Optical Fiber Communication কী?

Optical Fiber Communication হলো এমন একটি communication technology যেখানে optical fiber-এর মধ্য দিয়ে আলোর signal ব্যবহার করে তথ্য পাঠানো হয়।

[PC101 G FTTH Design and Network Basics Mark](https://images.openai.com/static-rsc-4/s7iuSYkSQ6GJrio8D7r-xPVw-zN17uoZzaFIs0NR1KvcA1vgGOMPmt7G-tEOL-0-P3ON5LC_AgiyZW-LiI3Ag_C14c3G6p4_dOQKKSUECHPeQE-f_2Gk5-nnOcvlpMSkz0Dw_uhprVii6mCPgallfXWJt1wE3jJ3ZbgA5SNNySA?purpose=inline)

[Optical Fiber communication | PPTX](https://images.openai.com/static-rsc-4/tw0NqrC84X5wyo7EbGHs9i5LuFzrUp09V8kOpgrafk3WdISesHzCDWa_YsCtE6DGkgAWD3DbCmS26TrtWemD6mx2MoaDnNT2-9NBXd1SweD2tnUBce1qbCiRkJxoYEtQi7ImWNMVr4Aj_NgvkdKdTW2o5a_yNrntv91F7LNWNaE?purpose=inline)

[Fiber Bragg Grating Bend Sensor – Ansys Optics](https://images.openai.com/static-rsc-4/e0ne1W_ptD1iFXNZlmis8VXBAcfblf9b8kAGsSdvzPZpNGH-fgUPKJxSd6yM9MADLFNriDrVumpUOO9_tGkSqrAZv_Xrfej1cercQcop4txpzHYg1ba-jyJjuZpZO7dVEITkgJmJH3ZX99BjBL5b-qxzDEohjx40fxGHIYoGlDU?purpose=inline)

6

একটি optical fiber-এর প্রধান অংশ:

- Core: যে অংশের ভেতর দিয়ে আলো চলাচল করে।
- Cladding: Core-কে ঘিরে থাকে; refractive index-এর উপযুক্ত পার্থক্যের মাধ্যমে আলোকে core-এর মধ্যে guide করতে সাহায্য করে।
- Coating: Fiber-কে physical damage ও পরিবেশগত প্রভাব থেকে সুরক্ষা দেয়।

### Total Internal Reflection (TIR)

Fiber-এর core ও cladding-এর refractive index এমনভাবে নির্বাচন করা হয় যেন আলো core-এর মধ্যে guide হতে পারে। উপযুক্ত incidence angle-এ total internal reflection-এর মাধ্যমে আলো fiber বরাবর চলতে থাকে।

মনে রাখবে:

- Core-এর refractive index সাধারণত cladding-এর চেয়ে বেশি।
- Optical fiber-এ electrical signal সরাসরি নয়, optical signal হিসেবে পরিবাহিত হয়।
- Optical fiber electromagnetic interference (EMI)-এর প্রতি সাধারণত প্রতিরোধী।

## 2. Single-Mode বনাম Multi-Mode Fiber

[Single Mode vs Multimode Fiber: What’s the Difference & Which Should You Use?](https://images.openai.com/static-rsc-4/T4Z6UaRpRoCwGreWOymyGUqnY09baBH3uR2Sn_sfY9f0TFq8hz2us5RT1Q7HIYWsVsyq01sIkyq616XayzVjLUcAXWPmzYx1k1TYmGrX508LqLEgRg3KmvO3_6Oby9x41BafDy-kBgDb4KVcLrWNj2yEKre41FyxDD7V_NmVSX4?purpose=inline)

[Single mode fiber vs Multimode Fiber](https://images.openai.com/static-rsc-4/bytRdUPKnKaEiZR7QkeW-VFYUSsTqbmXW_Ld4cwHli9IVyBu5G-yEyXFPbcYPll8jBo5E9iPB4phsF8CPuhN01eqzMrfcdUqh77LDBL3pP7Bp_GO7xkbfvuqxOVsLFWQbQ3QaOu2w7iWkmDI4NHzuVpke1XGK772f8TO_f2haak?purpose=inline)

[Introduction and application of Single Mode and Multimode Fiber Cable  – Splicer Market](https://images.openai.com/static-rsc-4/90oyF_e4FJn5IDGhWrcv59MegQN06x1nlNDETpSwTqc5A2jXQV4liNE2j27CeOoT7lln_cN_unIx7MIrDlOR5C4ti_NUU4LN8cKp94r3OQRB6jWBH2EamYaqd0GcAtB7QwWKQLULTeNPG17W7j4biVOGcFfPj_myNnS6s_DfNvc?purpose=inline)

6

| বিষয়              | Single-Mode Fiber (SMF)              | Multi-Mode Fiber (MMF)                 |
| ----------------- | ------------------------------------ | -------------------------------------- |
| Core              | ছোট, সাধারণত প্রায় 8–10 µm           | সাধারণত 50 বা 62.5 µm                  |
| Light propagation | মূলত একটি spatial mode               | একাধিক mode                            |
| ব্যবহার           | দীর্ঘ দূরত্ব, telecom backbone, FTTH | স্বল্প দূরত্বের LAN ও data center link |
| Modal dispersion  | তুলনামূলকভাবে কম                     | তুলনামূলকভাবে বেশি                     |
| সাধারণ wavelength | 1310 nm, 1550 nm                     | 850 nm, 1300 nm                        |

Exam shortcut: Long-distance telecom transmission → সাধারণত Single-Mode Fiber।

## 3. FTTH ও GPON

FTTH = Fiber to the Home। অর্থাৎ, optical fiber সরাসরি গ্রাহকের বাসা পর্যন্ত পৌঁছায়।

GPON = Gigabit-capable Passive Optical Network। এটি একটি passive optical access network technology, যা একটি optical distribution network-এর মাধ্যমে একাধিক গ্রাহককে service দিতে পারে।

[Ziņas — Ceļš uz optiskās šķiedras pieslēguma līdz mājām (FTTH) popularizēšanu un izaicinājumi](https://images.openai.com/static-rsc-4/RZ12W3E4jJHZCCiZLuWQgbUH7hTd6rt8Fj8kK2cYW_kpeEFOGryANAQlAuMpb60rIyEzGZEC6d64ZygSpolC8K_tuEmFIf52Fe1L8_aEOnA0hNqNkuZS3kzNuzYSACHkJGcSasINrAg0ji3J4xiP76k9J-sXRjV8rgFQZim4IlQ?purpose=inline)

[oyii.net](https://www.oyii.net/lv/news/the-road-to-popularization-and-challenges-of-fiber-to-the-home-ftth/)

### GPON Network-এর প্রধান অংশ

OLT

Optical Line Terminal — operator side

Optical Distribution Network (ODN)

Fiber, connectors, splices ও passive splitter

ONT 1

গ্রাহক ১

ONT 2

গ্রাহক ২

ONT N

গ্রাহক N

### OLT, ONT ও ONU-এর পার্থক্য

| Device   | পূর্ণরূপ                 | কাজ                                                                              |
| -------- | ------------------------ | -------------------------------------------------------------------------------- |
| OLT      | Optical Line Terminal    | Operator-এর central office/exchange side-এ থাকে; PON access network পরিচালনা করে |
| ONT      | Optical Network Terminal | গ্রাহকের স্থানে optical signal-কে service interface-এ রূপান্তর করে               |
| ONU      | Optical Network Unit     | গ্রাহক বা distribution point-এর পাশে optical network termination unit            |
| Splitter | Passive Optical Splitter | Optical signal-কে একাধিক output branch-এ ভাগ করে                                 |

ONT হলো ONU-এর একটি customer-premises ধরনের implementation; industry-তে শব্দ দুটি কখনো কাছাকাছি অর্থে ব্যবহৃত হয়।

গুরুত্বপূর্ণ: Passive splitter-এর জন্য আলাদা electrical power প্রয়োজন হয় না। তবে OLT ও সাধারণত ONT-এর power প্রয়োজন হয়।

## 4. GPON-এর Wavelength ও Data Rate

GPON-এর প্রচলিত wavelength:

| Direction / Service       | Wavelength |
| ------------------------- | ---------- |
| Downstream data           | 1490 nm    |
| Upstream data             | 1310 nm    |
| Optional RF video overlay | 1550 nm    |

GPON-এর প্রচলিত ITU-T G.984 configuration-এ nominal line rate হতে পারে:

- Downstream: 2.48832 Gbit/s
- Upstream: 1.24416 Gbit/s

মনে রাখবে, এগুলো GPON-এর nominal line rates; কোনো একজন গ্রাহক সবসময় এই পুরো bandwidth পান না। Split ratio, service profile, shared capacity ও protocol overhead-এর কারণে প্রকৃত throughput আলাদা হয়।

### Downstream ও Upstream কী?

- Downstream: Operator থেকে গ্রাহকের দিকে data।
- Upstream: গ্রাহক থেকে operator-এর দিকে data।

GPON-এ downstream transmission সাধারণত broadcast-ভিত্তিক; upstream transmission-এ একাধিক ONT-এর transmission সমন্বয়ের জন্য time-division multiple access (TDMA) ব্যবহৃত হয়।

## 5. Optical Attenuation ও Power Budget

Attenuation হলো transmission-এর সময় signal power কমে যাওয়া। Fiber, connector, splice ও splitter—সবগুলোই optical loss তৈরি করতে পারে।

Loss সাধারণত dB-তে প্রকাশ করা হয়, আর optical power সাধারণত dBm-এ প্রকাশ করা হয়।

- dB: দুই power level-এর অনুপাত বোঝায়।
- dBm: 1 mW reference-এর তুলনায় absolute power level বোঝায়।
- dBm ও dB এক নয়।

### Optical Loss Formula

Fiber-এর loss:

\\[ L\_{\text{fiber}}=\alpha \times D \\]

যেখানে:

- \\(\alpha\\) = attenuation coefficient (dB/km)
- \\(D\\) = fiber length (km)

সম্পূর্ণ link-এর আনুমানিক loss:

\\[ L\_{\text{total}} = L\_{\text{fiber}}+L\_{\text{connectors}} +L\_{\text{splices}}+L\_{\text{splitter}} \\]

Optical power budget:

\\[ \text{Received Power} = \text{Transmit Power}-L\_{\text{total}} \\]

এখানে transmit ও received power dBm-এ, আর loss dB-তে।

### Worked Example

ধরা যাক:

- Transmit power = \\(+3\\) dBm
- Fiber loss = \\(4\\) dB
- Connector loss = \\(1\\) dB
- Splice loss = \\(0.5\\) dB
- Splitter loss = \\(13\\) dB

তাহলে:

\\[ L\_{\text{total}}=4+1+0.5+13=18.5\text{ dB} \\]

\\[ P\_{\text{received}}=3-18.5 =\boxed{-15.5\text{ dBm}} \\]

এটি গ্রহণযোগ্য কি না, তা নির্ভর করে সংশ্লিষ্ট optical module-এর receiver sensitivity এবং PON-এর নির্দিষ্ট optical class-এর ওপর।

## 6. Optical Splitter Loss

Splitter-এর output বাড়ার সঙ্গে সঙ্গে ideal optical power প্রতিটি output-এ কমে যায়।

Ideal splitting loss:

\\[ L\_{\text{ideal}}=10\log\_{10}(N)\text{ dB} \\]

এখানে \\(N\\) হলো output branch-এর সংখ্যা।

| Split Ratio | Ideal Splitting Loss (প্রায়) |
| ----------- | ---------------------------- |
| 1:2         | 3.01 dB                      |
| 1:4         | 6.02 dB                      |
| 1:8         | 9.03 dB                      |
| 1:16        | 12.04 dB                     |
| 1:32        | 15.05 dB                     |
| 1:64        | 18.06 dB                     |

বাস্তবে splitter-এর excess loss ও অন্যান্য link loss যোগ হওয়ায় প্রকৃত loss ideal value-এর চেয়ে বেশি হয়।

পরীক্ষার কৌশল: Split ratio 1:32 হলে ideal splitting loss প্রায় 15 dB।

## 7. Fiber Splicing ও Connector

[Semel Internet Fibra - Internet de Alta Velocidade](https://images.openai.com/static-rsc-4/kOaE_fkMF8-um_FZgdEhCMsFLGSY61OMEgUoemtEkGDClm92Wu6NOakquPkK6XwNx_IOBIKG68wpBgDKdcI37iv-cjC1yDBzyUCzvNMjyk5X5GGioqZs_6-56eDb1tuKDGxq7KIx5w48isOHOj5uQdW3LBbTWsPgbjCWv8YaYog?purpose=inline)

[APC, UPC, PC Fiber Connector Types Comparison and Selection](https://images.openai.com/static-rsc-4/h0WkUgOKH7chexvgViNhgSzoWZXw9zDLJKIdgARXAndAKQRGhwdTXRkxIOnpPTDKVQNeyY04vwMbNpdY4BAQyBtMTxgdUE7AAIxxVB84q3pEF9WaWXlhpx7Bl_5AfVvIHGhItgDbwbK35sWwmne0FEk7XiSjBqX-W9TAtf004pA?purpose=inline)

[💡 Fiber Optics 101: Understanding UPC 🆚 APC Connectors  Ever wonder what the difference is between the blue and green connectors on fiber optic cables? It's not just a color choice—it's crucial for… | Wajahat Khan](https://images.openai.com/static-rsc-4/-0qZ0e9IKfP_7OSOhUrWhzNYd0Ivdsc_M0vG3o_g9uMTS__85xH8KowoHecSOvEojZK5lcxZf8HLuNwpPp0enRT18oIrOZR_1t2lBGt403E0-YNFhELtThWaKHz2NQHg6W2azKMn3UjqHoRQv-RY0BsQ7eZ7I179rD2cV5Zm0f0?purpose=inline)

7

### Fusion Splicing

দুটি optical fiber-এর প্রান্ত align করে electric arc বা fusion splicer-এর সাহায্যে জোড়া লাগানো হয়।

- সাধারণত কম splice loss পাওয়া যায়।
- Fiber backbone ও distribution network-এ বহুল ব্যবহৃত।
- ভালো alignment ও পরিষ্কার fiber end-face গুরুত্বপূর্ণ।

### Mechanical Splicing

একটি alignment mechanism ব্যবহার করে দুই fiber-এর প্রান্ত কাছাকাছি স্থাপন করা হয়। Fusion splicing-এর তুলনায় এর loss ও স্থায়িত্ব ভিন্ন হতে পারে।

### Connector-এর উদাহরণ

- SC: Square push-pull connector; PON-এ বহুল ব্যবহৃত।
- LC: ছোট form-factor connector; dense equipment-এ ব্যবহৃত।
- APC: Angled physical contact; সাধারণত সবুজ connector দিয়ে চেনা যায়।
- UPC: Ultra physical contact; সাধারণত নীল connector দিয়ে চেনা যায়।

সতর্কতা: Optical connector-এর end-face পরিষ্কার রাখা জরুরি। Fiber-এর আলো চোখে দেখা না গেলেও live fiber-এর প্রান্তে সরাসরি তাকানো উচিত নয়।

## 8. Optical Fiber Troubleshooting

Fiber link down হলে নিচের বিষয়গুলো পরীক্ষা করা হয়:

1. OLT/ONT-এর LOS ও PON indicator।
2. Patch cord ও connector পরিষ্কার এবং ঠিকভাবে সংযুক্ত কি না।
3. Fiber bend radius ঠিক আছে কি না।
4. Optical power meter দিয়ে received optical power।
5. OTDR দিয়ে fiber distance, break, splice ও reflection-related event।
6. Splitter, splice closure ও distribution point-এর connection।

### OTDR বনাম Optical Power Meter

| Instrument          | কাজ                                                                |
| ------------------- | ------------------------------------------------------------------ |
| Optical Power Meter | Optical power level মাপে                                           |
| Light Source        | নির্দিষ্ট wavelength-এ test signal দেয়                             |
| OTDR                | Fiber বরাবর loss/reflection event ও আনুমানিক distance বিশ্লেষণ করে |
| Fusion Splicer      | Fiber fusion করে জোড়া লাগায়                                        |

মনে রাখবে: OTDR fiber-এর fault location শনাক্ত করতে সাহায্য করে; optical power meter মূলত নির্দিষ্ট point-এ power level মাপে।

## 9. Teletalk Technical Exam — Quick Revision

| প্রশ্ন                                               | উত্তর                                   |
| ---------------------------------------------------- | --------------------------------------- |
| FTTH-এর পূর্ণরূপ কী?                                 | Fiber to the Home                       |
| GPON-এর পূর্ণরূপ কী?                                 | Gigabit-capable Passive Optical Network |
| OLT কোথায় থাকে?                                      | Operator side                           |
| ONT কোথায় থাকে?                                      | সাধারণত গ্রাহকের premises-এ             |
| GPON downstream wavelength কত?                       | 1490 nm                                 |
| GPON upstream wavelength কত?                         | 1310 nm                                 |
| GPON downstream nominal rate কত?                     | 2.48832 Gbit/s                          |
| GPON upstream nominal rate কত?                       | 1.24416 Gbit/s                          |
| 1:32 splitter-এর ideal loss কত?                      | প্রায় 15.05 dB                          |
| Optical power কোন unit-এ মাপা হয়?                    | dBm                                     |
| Link loss কোন unit-এ প্রকাশ করা হয়?                  | dB                                      |
| Fiber fault location খুঁজতে কোন instrument?          | OTDR                                    |
| Fiber জোড়া লাগানোর বহুল ব্যবহৃত পদ্ধতি?              | Fusion splicing                         |
| Long-distance transmission-এ কোন fiber বেশি ব্যবহৃত? | Single-mode fiber                       |
| Passive splitter-এর জন্য আলাদা power লাগে?           | না                                      |

## Lesson 23: MCQ Test

## Optical Fiber Quiz

0/12 answered

1\. FTTH-এর পূর্ণরূপ কী?

A. Fiber Through Hub

B. Fiber to the Home

C. Fast Transmission to Home

D. Frequency Transfer to Home

2\. GPON-এর downstream wavelength সাধারণত কত?

A. 850 nm

B. 1310 nm

C. 1490 nm

D. 1550 nm

3\. GPON-এর upstream wavelength সাধারণত কত?

A. 1310 nm

B. 1490 nm

C. 1550 nm

D. 1625 nm

4\. Operator-side PON device কোনটি?

A. ONT

B. ONU

C. OLT

D. Router only

5\. Optical power সাধারণত কোন unit-এ প্রকাশ করা হয়?

A. dBm

B. km

C. Mbps

D. Ohm

6\. 1:8 ideal splitter loss প্রায় কত?

A. 3 dB

B. 6 dB

C. 9 dB

D. 18 dB

7\. Fiber-এর loss মাপার ক্ষেত্রে dB কী বোঝায়?

A. Absolute power reference

B. Power ratio বা loss

C. Fiber length

D. Wavelength

8\. Fiber fault-এর distance ও event শনাক্ত করতে কোন instrument ব্যবহৃত হয়?

A. Multimeter

B. OTDR

C. Oscilloscope only

D. DHCP server

9\. দুটি fiber fusion করে জোড়া লাগানোর পদ্ধতি কোনটি?

A. Modulation

B. Fusion splicing

C. Multiplexing

D. Routing

10\. Long-distance telecom transmission-এ সাধারণত কোন fiber ব্যবহৃত হয়?

A. Single-mode fiber

B. Multi-mode fiber only

C. Copper coaxial cable

D. Twisted pair only

11\. Passive optical splitter-এর জন্য আলাদা electrical power লাগে কি?

A. সবসময় লাগে

B. সাধারণত লাগে না

C. শুধু upstream-এ লাগে

D. শুধু 5G-তে লাগে

12\. GPON-এর প্রচলিত downstream nominal line rate কোনটি?

A. 1.24416 Gbit/s

B. 2.48832 Gbit/s

C. 10 Mbit/s

D. 100 Gbit/s

Check Answers

পরবর্তী লেসন — Lesson 24: Telecom Transmission, Microwave Link, LOS, Fresnel Zone, SDH/PDH, WDM, Synchronization ও Link Budget-এর numerical problem।

# Lesson 24: Telecom Transmission — Microwave Link, LOS, Fresnel Zone, SDH/PDH, WDM ও Link Budget

Teletalk Bangladesh Limited Technical Exam Preparation

এই লেসনে শিখব কীভাবে telecom network-এ tower থেকে tower-এ data পাঠানো হয়, microwave link কীভাবে কাজ করে, Fresnel Zone কেন গুরুত্বপূর্ণ, SDH/PDH ও WDM কী এবং link budget-এর numerical problem কীভাবে সমাধান করতে হয়।

## 1. Microwave Communication কী?

Microwave communication হলো electromagnetic wave ব্যবহার করে এক স্থান থেকে অন্য স্থানে wireless data বা communication signal পাঠানোর পদ্ধতি।

[LOS Requirements in Microwave Communication: Clear Path Needed for Signal Integrity | Shah Yar Hussaini posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/kDyS1OXrWuJbX-gx7xDrL7NDaUSKUldQmrCE--fhv5B4tAtjwAisJKW_NuyB1PEN6sRngHyyaxZzUClvNqw3dZZr71mnC2oDEV0HloAYIi1XVRsswutMdzMHgrXrJ3Onfqb17KDQa5WR5-T34AhgSeooArVhsfNPAlW1hys4DEI?purpose=inline)

[linkedin.com](https://www.linkedin.com/posts/shahyars_in-microwave-communication-los-line-activity-7420114074052501505-ra6d)

Telecom network-এ microwave link ব্যবহার করা হয়:

- Mobile tower-কে অন্য tower বা aggregation site-এর সঙ্গে সংযুক্ত করতে।
- Fiber না থাকা স্থানে backhaul connectivity দিতে।
- Network-এর বিভিন্ন site-এর মধ্যে voice ও data traffic বহন করতে।

### Microwave Link-এর প্রধান অংশ

| Component          | কাজ                                                                |
| ------------------ | ------------------------------------------------------------------ |
| Antenna / Dish     | Radio wave transmit ও receive করে                                  |
| Transmitter        | Radio signal তৈরি ও transmit করে                                   |
| Receiver           | Signal গ্রহণ করে                                                   |
| Radio / IDU / ODU  | Equipment architecture অনুযায়ী signal processing ও RF handling করে |
| Feeder / Waveguide | Radio equipment ও antenna-এর মধ্যে signal বহন করতে পারে            |
| Tower              | Antenna-কে প্রয়োজনীয় উচ্চতায় স্থাপন করে                            |

মনে রাখবে: Microwave link-এর জন্য সাধারণত উপযুক্ত antenna alignment এবং clear propagation path প্রয়োজন।

## 2. LOS — Line of Sight

LOS-এর পূর্ণরূপ Line of Sight। দুটি antenna-র মধ্যে radio wave চলাচলের জন্য পর্যাপ্ত unobstructed path থাকা প্রয়োজন।

[File:Line of sight mw transmission.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/fJaHBVNGA88dS7CUXVo8PtA3-9r3RTd6NmZnYHon5Q5tRI7UTys2Nps8lruvJoI3Mf2906ODpqVaFHvOytJSE-gngFYTGDrcyvG88hMo_X7wNOtwE1r1uSOAKBRv69NhkJgTfUZlVKjMKVEYFovS4rdojCxQ7-SzNpCR8o-XB8I?purpose=inline)

[commons.wikimedia.org](https://commons.wikimedia.org/wiki/File%3ALine_of_sight_mw_transmission.svg)

ধরা যাক, দুটি telecom tower-এর মাঝখানে উঁচু ভবন বা পাহাড় আছে। এতে signal দুর্বল হতে পারে বা link বাধাগ্রস্ত হতে পারে।

LOS পরিকল্পনার সময় বিবেচনা করতে হয়:

- দুই antenna-র উচ্চতা।
- মাঝখানের ভবন, গাছ বা পাহাড়।
- পৃথিবীর বক্রতা।
- Fresnel Zone clearance।
- আবহাওয়া ও propagation condition।

### Radio Horizon-এর আনুমানিক Formula

Standard atmospheric refraction ধরে প্রচলিত engineering approximation:

\\[ d\_{\text{km}}\approx 4.12 \left(\sqrt{h_1}+\sqrt{h_2}\right) \\]

এখানে:

- \\(h_1,h_2\\) = দুই antenna-এর উচ্চতা, meter-এ।
- \\(d\\) = আনুমানিক radio horizon distance, kilometer-এ।

উদাহরণ: দুটি antenna-র উচ্চতা যথাক্রমে 25 m ও 36 m হলে,

\\[ d\approx4.12(5+6) \\]

\\[ d\approx45.32\text{ km} \\]

এটি আনুমানিক radio horizon; এটি নিশ্চিত microwave link distance নয়। Fresnel clearance, terrain, antenna characteristics ও link budget আলাদাভাবে যাচাই করতে হয়।

## 3. Fresnel Zone কী?

Fresnel Zone হলো transmitter ও receiver-এর মধ্যবর্তী radio propagation path-এর চারপাশের একটি ellipsoidal region। শুধু সরাসরি LOS দেখা গেলেই সবসময় ভালো link নিশ্চিত হয় না; Fresnel Zone-এ বাধা থাকলেও signal-এর performance কমতে পারে।

[#kingsat #fresnelzone #rfengineering #wirelesscommunication #microwavelinks #satellitecommunication #microwaveantenna #radiopropagation | Alex Kang | 15 comments](https://images.openai.com/static-rsc-4/XgtZCcSexOSWtLKlvEvldRg9hXgYjwMXu9VR8wDtmSnSIfQqJ-AuFNWfTaI4guQXvFcsBqsupZaHjFdldIF8ZJMpZV4tV8dobKfIdizBiMhl1uIqC4ikwWiMNS5O6r8_cH6TfG-2beYa4IH14IlTKKo_1wPmUf9ODat6j3uVI24?purpose=inline)

[linkedin.com](https://www.linkedin.com/feed/update/urn%3Ali%3Aactivity%3A7406548254278172672/)

প্রথম Fresnel Zone (First Fresnel Zone) সবচেয়ে বেশি গুরুত্বপূর্ণভাবে বিবেচনা করা হয়।

### First Fresnel Zone-এর Radius Formula

\\[ r_1=17.32\sqrt{\frac{d_1d_2}{fD}} \\]

যেখানে:

- \\(r_1\\) = প্রথম Fresnel Zone-এর radius, meter-এ।
- \\(d_1,d_2\\) = obstruction থেকে দুই প্রান্তের দূরত্ব, kilometer-এ।
- \\(D=d_1+d_2\\) = মোট link distance, kilometer-এ।
- \\(f\\) = frequency, GHz-এ।

### Numerical Example

ধরা যাক:

- মোট link distance = 10 km
- মাঝখানে obstruction আছে, তাই \\(d_1=5\\) km এবং \\(d_2=5\\) km
- Frequency = 6 GHz

তাহলে,

\\[ r_1=17.32\sqrt{\frac{5\times5}{6\times10}} \\]

\\[ r_1=17.32\sqrt{0.4167} \\]

\\[ \boxed{r_1\approx11.18\text{ m}} \\]

সাধারণ planning guideline অনুযায়ী প্রথম Fresnel Zone-এর প্রায় 60% clearance রাখা একটি প্রচলিত লক্ষ্য।

\\[ 0.6\times11.18\approx6.71\text{ m} \\]

অর্থাৎ midpoint-এ obstruction থেকে প্রয়োজনীয় clearance আনুমানিক 6.71 m। বাস্তব পরিকল্পনায় terrain profile, Earth curvature ও refractivity-ও বিবেচনা করতে হয়।

Exam shortcut: Frequency বাড়লে একই geometry-তে Fresnel Zone-এর radius সাধারণত কমে।

## 4. Link Budget কী?

Link budget হলো transmitter থেকে receiver পর্যন্ত signal power-এর হিসাব। এতে transmit power, antenna gain, cable loss, propagation loss ও অন্যান্য loss বিবেচনা করা হয়।

### গুরুত্বপূর্ণ Formula

\\[ P_r=P_t+G_t+G_r-L\_{\text{total}} \\]

যেখানে:

- \\(P_r\\) = Received power, dBm
- \\(P_t\\) = Transmit power, dBm
- \\(G_t\\) = Transmit antenna gain, dBi
- \\(G_r\\) = Receive antenna gain, dBi
- \\(L\_{\text{total}}\\) = মোট loss, dB

### Free-Space Path Loss (FSPL)

\\[ \boxed{FSPL=92.45+20\log\_{10}(f)+20\log\_{10}(D)} \\]

এখানে frequency \\(f\\) হলো GHz-এ এবং distance \\(D\\) হলো km-এ।

### Numerical Example

ধরা যাক:

- Transmit power = \\(20\\) dBm
- Transmit antenna gain = \\(30\\) dBi
- Receive antenna gain = \\(30\\) dBi
- Frequency = \\(6\\) GHz
- Distance = \\(10\\) km
- অন্যান্য loss = \\(4\\) dB

প্রথমে FSPL:

\\[ FSPL=92.45+20\log\_{10}(6)+20\log\_{10}(10) \\]

\\[ FSPL\approx92.45+15.56+20 \\]

\\[ FSPL\approx128.01\text{ dB} \\]

এখন received power:

\\[ P_r=20+30+30-128.01-4 \\]

\\[ \boxed{P_r\approx-52.01\text{ dBm}} \\]

যদি receiver sensitivity \\(-70\\) dBm হয়, তাহলে আনুমানিক fade margin:

\\[ FM=P_r-P\_{\text{sensitivity}} \\]

\\[ FM=-52.01-(-70)=\boxed{17.99\text{ dB}} \\]

অর্থাৎ আনুমানিক fade margin 18 dB। বাস্তব link design-এ প্রয়োজনীয় availability ও fading margin radio equipment, frequency, climate এবং path condition অনুযায়ী নির্ধারিত হয়।

## 5. PDH ও SDH

PDH এবং SDH হলো digital transmission ও multiplexing technology, যেগুলো telecom network-এ একাধিক data stream বহন করতে ব্যবহৃত হয়েছে।

### PDH — Plesiochronous Digital Hierarchy

- পুরোনো digital transmission hierarchy।
- বিভিন্ন stream-এর clock পুরোপুরি একই না-ও হতে পারে; তাই justification/stuffing ব্যবস্থার প্রয়োজন হতে পারে।
- উচ্চ স্তরের stream থেকে নির্দিষ্ট নিম্ন স্তরের channel বের করতে demultiplexing-এর একাধিক ধাপ লাগতে পারে।
  ### SDH — Synchronous Digital Hierarchy
- Synchronized digital transmission hierarchy।
- Network management ও multiplexing structure তুলনামূলকভাবে সুবিধাজনক।
- STM-1-এর standard line rate হলো 155.52 Mbit/s।
- Higher-level STM rates সাধারণত STM-1-এর integer multiple।

### PDH বনাম SDH

| বিষয়                  | PDH                                        | SDH                             |
| --------------------- | ------------------------------------------ | ------------------------------- |
| Synchronization       | Plesiochronous                             | Synchronous hierarchy           |
| Multiplexing          | নিম্ন স্তরের channel access তুলনামূলক জটিল | Add/drop multiplexing সুবিধাজনক |
| Management            | তুলনামূলক সীমিত                            | উন্নত OAM ও network management  |
| Standard rate example | E1 = 2.048 Mbit/s                          | STM-1 = 155.52 Mbit/s           |

Exam facts:

- E1 rate = 2.048 Mbit/s
- STM-1 rate = 155.52 Mbit/s
- SDH-এর পূর্ণরূপ = Synchronous Digital Hierarchy
- PDH-এর পূর্ণরূপ = Plesiochronous Digital Hierarchy

## 6. Multiplexing: FDM, TDM ও WDM

Multiplexing হলো একই transmission medium বা system-এর capacity ব্যবহার করে একাধিক signal বহন করার কৌশল।

[PPT - Efficient Multiplexing Systems: FDM & TDM Overview PowerPoint Presentation - ID:9194691](https://images.openai.com/static-rsc-4/U75eeTOWxj8TRsgZOaKcZV9VS_ra-D0T1te3CcHq3uHeYAIiAZVT-Q8MWG_24hSKHvoizKftqjGoEJ7t4xnK6-oOwOySfpxNAgsqM8RaNNRQu3mi8gLBD-_gRXRGRYUgelGyjBfbIDEX4FM3dT9m0jcUmTPRcf5E0sPMiyknMD4?purpose=inline)

[Time Division Multiplexing: Working Principle, Diagram, Differences &  Applications](https://images.openai.com/static-rsc-4/rGNaHP2PtS0DR-3QoKExl6LVilqbfy8CANX8lfaHIgYaU6nF02csAE3CbVB-BYqtMX1JXOTs72c0a0vfu6l6vHL0Lu1Q3VkTpoMtjzY5JaEoO1c3iTgXTaEIt7VvMNgmkJB-JbmuLsccz6rn7GpixfcNXLlAixXtoOUnnm2u5eo?purpose=inline)

[Multiplexing Techniques: The Invisible Highway System of Your Data](https://images.openai.com/static-rsc-4/giGxo3LxPKMd3bhapM0U_kUO8BMRQrqTL_moKq6Y8SQh1a8kf31wzeTX_iBCWQJeNzk8gwvjAoe4j8X6NJtQkZ8CMX7s31YGtxTgRKp6GllQDv_on8ZfWohIGYOzl8TK9h_IVLi-HIM21gqAAbeM2vMlltrkTs5idZt5zJLPwyI?purpose=inline)

6

| Technology | কী ভাগ করা হয়?     | উদাহরণ                    |
| ---------- | ------------------ | ------------------------- |
| FDM        | Frequency band     | Radio broadcasting        |
| TDM        | Time slot          | Digital telecommunication |
| WDM        | Optical wavelength | Fiber-optic backbone      |

### WDM-এর ধরন

- CWDM: Coarse Wavelength Division Multiplexing।
- DWDM: Dense Wavelength Division Multiplexing।

WDM-এ বিভিন্ন wavelength-এর optical signal একই fiber-এ একসঙ্গে পাঠানো যায়। ফলে নতুন fiber বসানো ছাড়াই existing fiber-এর capacity বাড়ানো সম্ভব হতে পারে।

মনে রাখবে: FDM → Frequency, TDM → Time, WDM → Wavelength।

## 7. Network Synchronization

Telecom network-এ বিভিন্ন equipment-এর clock যথাযথভাবে synchronized রাখা জরুরি। Synchronization সমস্যা হলে timing error, packet delay variation বা service quality-তে প্রভাব পড়তে পারে।

| Technology | পূর্ণরূপ / কাজ                                                           |
| ---------- | ------------------------------------------------------------------------ |
| GPS/GNSS   | Satellite থেকে timing reference পাওয়া                                    |
| NTP        | Network-এর clock synchronize করা                                         |
| PTP        | Precision Time Protocol; নির্ভুল timing synchronization                  |
| SyncE      | Synchronous Ethernet; Ethernet link-এর মাধ্যমে frequency synchronization |

গুরুত্বপূর্ণ পার্থক্য:

- NTP: সাধারণ IP network-এ clock synchronization।
- PTP (IEEE 1588): উপযুক্ত hardware ও network design-এ বেশি নির্ভুল time synchronization সম্ভব।
- SyncE: Ethernet physical layer-এর মাধ্যমে frequency synchronization দেয়; একা absolute time-of-day সরবরাহ করে না।

## 8. Transmission Troubleshooting

Microwave বা transmission link down হলে সাধারণত নিচের বিষয়গুলো যাচাই করা হয়:

1. Equipment power ও alarm status।
2. Antenna alignment এবং LOS obstruction।
3. Received Signal Level (RSL) ও fade margin।
4. Frequency configuration ও interference।
5. Cable, connector এবং grounding।
6. Interface status, clock synchronization ও transmission error।
7. IP connectivity, routing এবং VLAN configuration।

### গুরুত্বপূর্ণ Term

| Term         | অর্থ                                                   |
| ------------ | ------------------------------------------------------ |
| RSL          | Received Signal Level                                  |
| SNR          | Signal-to-Noise Ratio                                  |
| BER          | Bit Error Rate                                         |
| Availability | নির্দিষ্ট সময়ে service সচল থাকার অনুপাত                |
| Fade Margin  | Received signal level ও প্রয়োজনীয় threshold-এর ব্যবধান |
| Latency      | Data পৌঁছাতে সময়                                       |
| Jitter       | Packet delay-এর পরিবর্তন                               |

## 9. Lesson 24 — Quick Revision

| প্রশ্ন                                    | উত্তর                                                     |
| ----------------------------------------- | --------------------------------------------------------- |
| LOS-এর পূর্ণরূপ কী?                       | Line of Sight                                             |
| Fresnel Zone কেন গুরুত্বপূর্ণ?            | Radio path-এর চারপাশে obstruction-এর প্রভাব বিবেচনার জন্য |
| Link budget-এর received power formula কী? | \\(P_r=P_t+G_t+G_r-L\_{\text{total}}\\)                   |
| FSPL-এর unit কী?                          | dB                                                        |
| E1-এর data rate কত?                       | 2.048 Mbit/s                                              |
| STM-1-এর rate কত?                         | 155.52 Mbit/s                                             |
| FDM-এ কী ভাগ করা হয়?                      | Frequency                                                 |
| TDM-এ কী ভাগ করা হয়?                      | Time slot                                                 |
| WDM-এ কী ভাগ করা হয়?                      | Optical wavelength                                        |
| PTP-এর standard number কী?                | IEEE 1588                                                 |
| SyncE কী দেয়?                             | Frequency synchronization                                 |
| BER-এর পূর্ণরূপ কী?                       | Bit Error Rate                                            |

## Lesson 24: MCQ Test

## Transmission MCQ

0/12 answered

1\. LOS-এর পূর্ণরূপ কী?

A. Level of Signal

B. Line of Sight

C. Link of Service

D. Loss of Spectrum

2\. First Fresnel Zone-এর প্রায় কত শতাংশ clearance একটি প্রচলিত planning guideline?

A. 10%

B. 30%

C. 60%

D. 100%

3\. Link budget-এ antenna gain সাধারণত কোন unit-এ প্রকাশ করা হয়?

A. dBi

B. dBm/km

C. Hz

D. Ohm

4\. E1 transmission rate কত?

A. 1.024 Mbit/s

B. 2.048 Mbit/s

C. 8.448 Mbit/s

D. 155.52 Mbit/s

5\. SDH-এর STM-1 rate কত?

A. 2.048 Mbit/s

B. 34.368 Mbit/s

C. 155.52 Mbit/s

D. 622.08 kbit/s

6\. WDM-এ multiplexing কীসের ভিত্তিতে হয়?

A. Time slot

B. Optical wavelength

C. IP address

D. Packet size

7\. TDM-এর পূর্ণরূপ কী?

A. Time Division Multiplexing

B. Transmission Data Method

C. Total Digital Modulation

D. Time Delay Measurement

8\. PDH-এর পূর্ণরূপ কী?

A. Packet Data Hierarchy

B. Plesiochronous Digital Hierarchy

C. Primary Digital Hub

D. Parallel Data Highway

9\. NTP-এর প্রধান কাজ কী?

A. Optical power মাপা

B. Clock synchronization

C. Fiber splice করা

D. Antenna gain বাড়ানো

10\. BER কী পরিমাপ করে?

A. Bit error-এর অনুপাত

B. Fiber length

C. Antenna height

D. IP subnet size

11\. 6 GHz frequency ও 10 km distance-এর FSPL আনুমানিক কত?

A. 68 dB

B. 92 dB

C. 128 dB

D. 155 dB

12\. SyncE প্রধানত কোন synchronization দেয়?

A. Frequency synchronization

B. Absolute location

C. IP address allocation

D. Optical wavelength conversion

Check Answers

পরবর্তী লেসন — Lesson 25: Mobile Network Optimization, KPI, RSRP, RSRQ, SINR, RSSI, Drive Test, Handover ও LTE Troubleshooting।
# Lesson 25: Mobile Network Optimization ও LTE Troubleshooting

আজকের লেসনে Teletalk-এর টেকনিক্যাল পরীক্ষার জন্য গুরুত্বপূর্ণ বিষয়গুলো শিখব: RSRP, RSRQ, SINR, RSSI, Drive Test, Handover, LTE KPI এবং Network Troubleshooting। প্রতিটি টপিকের সংজ্ঞা, ব্যবহারিক উদাহরণ ও পরীক্ষায় আসতে পারে এমন প্রশ্ন থাকবে।

## 1. Mobile Network Optimization কী?

Mobile Network Optimization হলো মোবাইল নেটওয়ার্কের পারফরম্যান্স উন্নত করার প্রক্রিয়া, যাতে ব্যবহারকারী ভালো সিগন্যাল, দ্রুত ডেটা, কম কল ড্রপ এবং নির্ভরযোগ্য সংযোগ পান।

প্রধান লক্ষ্য:

- Coverage উন্নত করা
- Signal quality বাড়ানো
- Download ও upload speed উন্নত করা
- Call drop ও handover failure কমানো
- Network congestion কমানো

উদাহরণ: কোনো এলাকায় LTE সিগন্যাল ভালো, কিন্তু ইন্টারনেট ধীর। কারণ হতে পারে বেশি ব্যবহারকারী, radio interference, backhaul bottleneck অথবা কম available bandwidth। তাই শুধু সিগন্যালের শক্তি বাড়ালেই সব সমস্যার সমাধান হয় না।

## 2. LTE Signal Parameters: RSRP, RSRQ, SINR ও RSSI

[What Is Signal Strength Measured In at Indiana Houlding blog](https://images.openai.com/static-rsc-4/bpIuPBw8NvG7ZxTCGKcKt1Z074bBCEy9wTwcJPxl8nC9h77w-ZZns1ZA1SeDTX3sJOzWvdkOsBmkoV4ZUARhrI8GlfwaeIJcDB4V7wCxyj9QLhdq-eDyy3APUqbDOi3w9lYsk87MsEBTXntcPOdkCFTVXyebXoRUbM6dAC_ByLE?purpose=inline)

RSRP — Reference Signal Received Power

LTE-এর reference signal থেকে পাওয়া শক্তির পরিমাপ। এটি মূলত signal coverage বোঝাতে ব্যবহৃত হয়।

একক: dBm

[Cellular Router External Antenna: A 2026 Install Guide                      – SwiftNet Wifi](https://images.openai.com/static-rsc-4/waCZQuKRL83qKc8Od5VAXkFTAEfi93sJoBgj1h_o0a_Qi3jmbuFCF64Urmk4Vd8rYxruystQpaoanAnxA4crfNlTp14IJLc5iFGSDBeAm1XTEpfVwmugHnOCSjvxzBmvmJL0bQyjGnLFZbX0lK_E0IhWjzl21aWNnLiKyMKAtsA?purpose=inline)

RSRQ — Reference Signal Received Quality

Signal quality বোঝায়; এটি RSRP এবং RSSI-এর সঙ্গে সম্পর্কিত। Interference ও load-এর প্রভাব এতে প্রতিফলিত হতে পারে।

একক: dB

[SNR vs SINR in Wireless Communications Explained | Sedqatullah Yaqoubi posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/q7ub8Ka7B3-erUqDvzMtjsLzU6uSm29pdMc0TshggB7aAQOEsXHr_MkxjeeZFv_zuVyUFgrI7EylO8COO76hfn1qKS7DSzc9j4ZEgv_z_gXCS1J33NrxJcXwLB--LtEXhQYgxszawhWnzrXkOTZ8uOFDKjzlreTsFXKO6le333c?purpose=inline)

SINR — Signal-to-Interference-plus-Noise Ratio

কাঙ্ক্ষিত signal-এর তুলনায় interference ও noise কতটা, তা বোঝায়। সাধারণত বেশি SINR ভালো radio condition নির্দেশ করে।

একক: dB

[MAX-BR1 units choosing the weaker band unless band is disabled - Pepwave MAX - Peplink Community](https://images.openai.com/static-rsc-4/BafNUuTWlYcHEaeDMCKQcQ6LMDECyXnydbFYn1MBP0kZOUr-JZJN_1B5zmc9Y1xbQ13RF-YcrTg9tC22a5lKuNQ17Qy3_Zj6_w6lOYtz5h36bkBannsOUHJSlIZLzqHyWJ99CHlkyezIU8MHWFpFnUtgyt1vsc5peHvrb-THHkA?purpose=inline)

RSSI — Received Signal Strength Indicator

নির্দিষ্ট bandwidth-এ মোট received power; এতে serving signal-এর পাশাপাশি interference ও noise-ও থাকতে পারে।

একক: dBm

### সাধারণ LTE signal interpretation

নিচের মানগুলো প্রচলিত আনুমানিক guideline; প্রকৃত classification network, device ও measurement setup অনুযায়ী বদলাতে পারে।

| Parameter | ভালো            | মাঝারি            | দুর্বল           |
| --------- | --------------- | ----------------- | ---------------- |
| RSRP      | −80 dBm বা বেশি | −80 থেকে −100 dBm | −100 dBm-এর নিচে |
| RSRQ      | −10 dB বা বেশি  | −10 থেকে −15 dB   | −15 dB-এর নিচে   |
| SINR      | 20 dB বা বেশি   | 0–20 dB           | 0 dB-এর নিচে     |

মনে রাখবে: RSRP যত কম negative হবে, সাধারণত signal তত শক্তিশালী। যেমন −75 dBm, −105 dBm-এর চেয়ে শক্তিশালী।

## 3. RSRQ-এর Formula ও Numerical Example

LTE-তে RSRQ-এর সম্পর্ক:

\\[ RSRQ=\frac{N\times RSRP}{RSSI} \\]

এখানে:

- \\(N\\) = measurement bandwidth-এ resource blocks-এর সংখ্যা
- RSRP = Reference Signal Received Power
- RSSI = Received Signal Strength Indicator

Logarithmic unit-এ:

\\[ RSRQ(dB)=RSRP(dBm)-RSSI(dBm)+10\log\_{10}(N) \\]

উদাহরণ: RSRP = −90 dBm, RSSI = −60 dBm এবং \\(N=50\\)।

\\[ RSRQ=-90-(-60)+10\log\_{10}(50) \\]

\\[ RSRQ\approx -13.01\ dB \\]

অর্থাৎ RSRQ প্রায় −13 dB।

পরীক্ষার জন্য গুরুত্বপূর্ণ: RSRP signal power নির্দেশ করে, আর RSRQ signal quality সম্পর্কে ধারণা দেয়।

## 4. Drive Test কী?

[The Importance of Drive Testing for Network Reliability](https://images.openai.com/static-rsc-4/7_JEKPkZgmLKGzPN7QS9dzoV5dnodCcJz0jhn7F4f2lvv9HJT6IbGX2X1v97kP_kXjIqglPJXTc_QiUjGZAmVqAnbMUmabpb-jx52NJJ2nG5GJv_JWp21NiQJD0RSIrFXYJXneanY1U_14a0QsF2CvlmkDWm50tyTbe4GX5A_hI?purpose=inline)

[Drive Test Evolves for 5G Network Validation | Dingli Communications posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/EZ6N6U9RjhvHmKZtO5p_hz2MA4bOO1iYZ2ge5HkiFYMlh8QMlcifK14DeLnB4ZV7fXTf65RGivT-ved0xriF4gq8_eOsw0uBYqgw15mvkhSWjEBlA5L-HLHRNDYBZ204p_J8bJ8RD7mqp9GiM0aivUXYkQekY6gUk9rm7IjxELM?purpose=inline)

[Serving Cell PCIs on Drive Route Troubleshooting Nemo Analyze !! Logfile analysis | Ankur Tomar](https://images.openai.com/static-rsc-4/h1j9bVsmPnaWyMCb2a61KjK5U8M8DLimFw7OvDFVOttbd7eQE77QwkEylzgk9HThBO2WOuYiXh4ZRJefzej6-34HLg_60qzR6s9c5Mvx-TIqmKSyOKfBKI2VpSej_I86YHGsvGEr0tQWs0V3x34J7fZHhwLNVPlML8KXREvreSw?purpose=inline)

11

Drive Test হলো নির্দিষ্ট এলাকায় চলমান গাড়ি বা অন্য কোনো measurement setup ব্যবহার করে মোবাইল নেটওয়ার্কের বাস্তব পারফরম্যান্স পরিমাপ করা।

Drive test-এ সাধারণত পরীক্ষা করা হয়:

- RSRP, RSRQ ও SINR
- Download/upload throughput
- Call setup success ও call drop
- Handover success/failure
- Coverage hole ও weak-signal area
- Latency এবং connectivity

উদাহরণ: একটি রাস্তার নির্দিষ্ট অংশে বারবার কল ড্রপ হচ্ছে। Drive test করলে দেখা যেতে পারে ওই অংশে RSRP দুর্বল, SINR কম, অথবা পাশের cell-এ handover ঠিকমতো হচ্ছে না।

### Drive Test বনাম Walk Test

| বিষয়          | Drive Test                | Walk Test                         |
| ------------- | ------------------------- | --------------------------------- |
| পদ্ধতি        | গাড়ি দিয়ে পরিমাপ          | হেঁটে পরিমাপ                      |
| ব্যবহার       | রাস্তা, highway, বড় এলাকা | ভবন, অফিস, indoor area            |
| প্রধান সুবিধা | দ্রুত বড় এলাকা পরীক্ষা    | নির্দিষ্ট জায়গা বিস্তারিত পরীক্ষা |

## 5. Handover কী?

Handover হলো চলমান মোবাইল সংযোগকে একটি cell বা base station থেকে অন্য cell বা base station-এ স্থানান্তর করা, যাতে চলার সময়ও সংযোগ বজায় থাকে।

[LTE Handover Events A1-A5 & B1-B2 Explained | Atif Zaman posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/1Vqnl9CHpQtKR7U_6scLv1Or3I0_XRLiyOM640qHvUrq7tm5ojdjKHaRnvS1f-dOsIAy767Ss0t_DCovAoCkO064BDnvULjUo9Qr1EiStIg-KLepMVW3Nk_NJe-0hfOCtktSMNsZ0qdYY1crYNXJ_WN66KyvtzIj99OBOBCbDYQ?purpose=inline)

[linkedin.com](https://www.linkedin.com/posts/atif-zaman-5a43aa24a_lte-handover-events-explanation-a1a5-activity-7431044213623902208-9TCT)

### Handover-এর ধরন

- Intra-frequency handover: একই frequency-তে অন্য cell-এ যাওয়া।
- Inter-frequency handover: অন্য frequency-তে যাওয়া।
- Inter-RAT handover: এক radio access technology থেকে অন্যটিতে যাওয়া, যেমন LTE থেকে 3G।

### Hard Handover বনাম Soft Handover

| Hard Handover                                  | Soft Handover                                 |
| ---------------------------------------------- | --------------------------------------------- |
| সাধারণত break-before-make                      | সাধারণত make-before-break                     |
| LTE-তে সাধারণ handover পদ্ধতি                  | CDMA/WCDMA-র কিছু ব্যবস্থায় ব্যবহৃত           |
| পুরোনো সংযোগ ছাড়ার পর নতুন সংযোগ প্রতিষ্ঠিত হয় | কিছু সময় একাধিক cell-এর সঙ্গে সংযোগ বজায় থাকে |

Exam point: LTE সাধারণত hard handover ব্যবহার করে। Soft handover LTE-এর সাধারণ handover পদ্ধতি নয়।

### Handover Failure-এর কারণ

1. Target cell-এর signal দুর্বল।
2. Neighbor-cell configuration ভুল বা অসম্পূর্ণ।
3. Radio interference বেশি।
4. Target cell congested।
5. Handover parameter বা timing সঠিক নয়।

## 6. LTE Network KPI

KPI-এর পূর্ণরূপ Key Performance Indicator। নেটওয়ার্কের কার্যকারিতা পরিমাপ করতে KPI ব্যবহার করা হয়।

| KPI                      | কী পরিমাপ করে?                         |
| ------------------------ | -------------------------------------- |
| RRC Setup Success Rate   | Radio connection স্থাপনের সফলতার হার   |
| E-RAB Setup Success Rate | LTE bearer establishment-এর সফলতার হার |
| Handover Success Rate    | Handover সফল হওয়ার হার                 |
| Call Drop Rate           | চলমান voice call বিচ্ছিন্ন হওয়ার হার   |
| Throughput               | প্রতি সেকেন্ডে কার্যকর data transfer   |
| Latency                  | ডেটা পৌঁছাতে বিলম্ব                    |
| Availability             | নেটওয়ার্ক কতটা সময় সচল থাকে            |

### KPI-এর Formula

\\[ \text{Success Rate}=\frac{\text{Successful Attempts}}{\text{Total Attempts}}\times100\\% \\]

Numerical example: মোট ১,০০০টি handover attempt-এর মধ্যে ৯৬০টি সফল হয়েছে।

\\[ \frac{960}{1000}\times100=96\\% \\]

Handover Success Rate = 96%।

মনে রাখবে, বাস্তব network KPI-এর numerator ও denominator নির্দিষ্ট 3GPP/operator counter definition অনুসারে নির্ধারিত হয়।

## 7. LTE Troubleshooting: সমস্যা ও সম্ভাব্য সমাধান

| সমস্যা                | সম্ভাব্য কারণ                                    | কী পরীক্ষা করবে?                              |
| --------------------- | ------------------------------------------------ | --------------------------------------------- |
| Signal দুর্বল         | দূরত্ব, building blockage, coverage gap          | RSRP, antenna ও coverage map                  |
| Signal ভালো, speed কম | Congestion, interference, backhaul bottleneck    | SINR, cell load, bandwidth ও backhaul         |
| Call drop             | Coverage gap, radio-link failure, handover issue | Drop counter, RSRP, SINR ও handover logs      |
| Handover failure      | Neighbor configuration, target-cell সমস্যা       | Neighbor list, handover counters              |
| High latency          | Congestion, routing বা transport delay           | Ping, traceroute, backhaul এবং core network   |
| LTE attach failure    | Authentication, SIM, configuration বা core issue | UE logs, MME/core logs, authentication status |

### Troubleshooting-এর সহজ Workflow

Step 1: Problem identify

কোন এলাকায়, কোন সময়ে এবং কোন service-এ সমস্যা?

Step 2: Measurements collect

RSRP, RSRQ, SINR, throughput ও KPI

Step 3: Root cause analysis

Coverage, interference, congestion, transport অথবা core issue

Step 4: Fix and verify

সমাধানের পর পুনরায় measurement ও KPI যাচাই

## 8. পরীক্ষার আগে Quick Revision

- RSRP: LTE reference signal-এর received power।
- RSRQ: LTE reference signal quality।
- SINR: Signal বনাম interference ও noise।
- RSSI: মোট received power-এর পরিমাপ।
- Drive Test: বাস্তব এলাকায় network performance measurement।
- Handover: এক cell থেকে অন্য cell-এ সংযোগ স্থানান্তর।
- KPI: নেটওয়ার্কের performance পরিমাপের indicator।
- Throughput: কার্যকর data transfer rate।
- Latency: ডেটা পৌঁছানোর delay।
- LTE handover: সাধারণত hard handover।

## 9. Interactive MCQ Quiz

## Lesson 25 Quiz

0/12 answered

প্রতিটি প্রশ্নের একটি সঠিক উত্তর নির্বাচন করো। শেষে Check Answers চাপো।

1\. LTE-তে coverage বোঝার জন্য কোন parameter সবচেয়ে সরাসরি ব্যবহৃত হয়?

A. RSRP

B. RSRQ

C. SINR

D. Latency

2\. Signal quality ও interference-এর প্রভাব বোঝার জন্য কোনটি গুরুত্বপূর্ণ?

A. IMEI

B. RSRQ

C. MSISDN

D. DHCP

3\. SINR-এর পূর্ণরূপ কী?

A. Signal Internet Network Rate

B. Signal-to-Interference-plus-Noise Ratio

C. System Input Noise Range

D. Signal Integrated Network Response

4\. কোনটি received power-এর একক?

A. dBm

B. dB/s

C. Hz/s

D. Byte

5\. Drive Test-এর প্রধান উদ্দেশ্য কী?

A. Database তৈরি করা

B. বাস্তব এলাকায় mobile network performance পরিমাপ করা

C. Software compile করা

D. SIM তৈরি করা

6\. LTE-তে সাধারণ handover পদ্ধতি কোনটি?

A. Soft handover

B. Hard handover

C. Store-and-forward

D. Circuit switching

7\. ১,০০০টি handover attempt-এর ৯৬০টি সফল হলে success rate কত?

A. 90%

B. 94%

C. 96%

D. 98%

8\. Signal ভালো, কিন্তু speed কম—সম্ভাব্য কারণ কী?

A. শুধু দুর্বল RSRP

B. Congestion বা interference

C. সব সময় SIM নষ্ট

D. শুধু GPS বন্ধ

9\. Latency কী বোঝায়?

A. ডেটা পৌঁছাতে বিলম্ব

B. Antenna height

C. SIM-এর নম্বর

D. Optical fiber-এর ব্যাস

10\. Handover failure বিশ্লেষণে কোনটি সবচেয়ে প্রাসঙ্গিক?

A. Neighbor-cell configuration

B. Keyboard layout

C. Monitor resolution

D. File extension

11\. RSSI সাধারণত কী নির্দেশ করে?

A. শুধু LTE reference signal power

B. নির্দিষ্ট bandwidth-এ মোট received power

C. শুধু upload speed

D. শুধু latency

12\. KPI-এর পূর্ণরূপ কী?

A. Key Performance Indicator

B. Known Protocol Interface

C. Kernel Processing Input

D. Key Program Installation

Check Answers

পরবর্তী ক্লাস হবে Lesson 26: 2G, 3G, 4G ও 5G-এর তুলনা, LTE call flow, attach procedure এবং গুরুত্বপূর্ণ telecom interview questions।

# Lesson 26: 2G, 3G, 4G ও 5G — Call Flow, LTE Attach Procedure এবং Telecom Interview Questions

এই লেসনটি Teletalk Bangladesh Limited-এর টেকনিক্যাল পরীক্ষার প্রস্তুতির জন্য সাজানো হয়েছে। আজ আমরা মোবাইল নেটওয়ার্কের প্রজন্মগুলোর পার্থক্য, LTE-তে ফোন কীভাবে নেটওয়ার্কে যুক্ত হয়, voice call কীভাবে কাজ করে এবং গুরুত্বপূর্ণ টেকনিক্যাল প্রশ্ন শিখব।

## 1. 2G, 3G, 4G ও 5G-এর তুলনা

[Chapter 7 Wireless and Mobile Networks -  ppt download](https://images.openai.com/static-rsc-4/1hE3SLlME1w6PshVeKxj2FTrCkDB5InrMxtmoErahxR52ROAlVcvvtfbMotzDV59tlC-SovQSsrdTNgMJDJrHtf5GYD_BeCR3wrynhbXkHmjq-BDa2jK_eRs7-3HIvXt1r7spaLsrkZ01rrM7AHlNEyJL3OcXYcMqRcrydCoSyk?purpose=inline)

2G — GSM

প্রধান প্রযুক্তি: GSM, GPRS, EDGE

ডিজিটাল voice call, SMS এবং GPRS/EDGE-এর মাধ্যমে data service।

[PPT - 3 rd Generation WCDMA / UMTS Wireless Network PowerPoint Presentation - ID:6746158](https://images.openai.com/static-rsc-4/sSgVAwUkktWVR7jDVz4byMFzpwGithkwadygvt5Wom5NXyJqukQ0TT9tIS2qaP13lvklG_b8BAhODGYEr07LM3NCjgARM8d4XAPjUAokhYQezrGjNuKGTp26B1jdQG22jhs3j3dJJ097luChWbR1VGXODoGvF0qs8DJ4nnFXP9I?purpose=inline)

3G — UMTS/WCDMA

প্রধান প্রযুক্তি: UMTS, WCDMA, HSPA

উন্নত mobile data, video calling এবং তুলনামূলক দ্রুত internet access।

[4G RAN Architecture Simplifies Radio Access with eNodeB | Sedqatullah Yaqoubi posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/nX43d8El-HDZ4E1meD7O8yJ9QizS3M40GH5-ztq7JNNhjbzWkxFtGPgpx5cM7nL-Wa7tE5ei6F8gy2OeT1awq_dl2OjsWny57E715Y5EYpz58bB3gvkRMfK77Zp1oOU7KshvIOkgnq537bJOCPCev7eqYBtJDUnjrs5AleaS_7s?purpose=inline)

4G — LTE

প্রধান প্রযুক্তি: LTE, LTE-Advanced

উচ্চগতির IP-based data service; VoLTE ব্যবহার করলে LTE network-এর মাধ্যমে voice call।

[Using Massive MIMO in 2026: The Technology Powering Future Wireless Networks](https://images.openai.com/static-rsc-4/kqhn6qr5FmsybdDxd07doegWeZxw3CeBu9XOq2Wpz5pb02z4QtULQT-rMGSaT0PlFq7C3zFrLCTfcFaCStA6SBy02yk07hydfD4C7RtVwij28n2zIsr1LmXOhIccYt934-P-TBMxT-G7i_znj7vAUyWgb2q9ig9QDXDXqHktW1M?purpose=inline)

5G — NR

প্রধান প্রযুক্তি: 5G NR, 5G Core

বেশি capacity, উচ্চ data rate, কম latency-এর সম্ভাবনা এবং massive IoT-সহ বিভিন্ন use case।

### গুরুত্বপূর্ণ পার্থক্য

| বৈশিষ্ট্য                   | 2G                     | 3G                       | 4G                  | 5G                                     |
| --------------------------- | ---------------------- | ------------------------ | ------------------- | -------------------------------------- |
| Radio technology            | GSM                    | WCDMA/UMTS               | LTE                 | NR                                     |
| প্রধান service              | Voice, SMS             | Voice, data              | Broadband, VoLTE    | Enhanced broadband, IoT                |
| Radio equipment             | BTS                    | NodeB                    | eNodeB              | gNodeB                                 |
| প্রধান network architecture | Circuit-switched voice | Circuit + packet domains | Packet-switched EPC | 5G Core-এ service-based architecture   |
| Voice service               | GSM voice              | Circuit-switched voice   | VoLTE অথবা fallback | VoNR অথবা fallback, deployment অনুযায়ী |

পরীক্ষায় মনে রাখবে: BTS → 2G, NodeB → 3G, eNodeB → 4G LTE, gNodeB → 5G NR।

সব 4G network-এ VoLTE থাকা বাধ্যতামূলক নয়। একইভাবে, 5G-তে VoNR ব্যবহারের জন্য উপযুক্ত 5G deployment ও voice-service configuration প্রয়োজন।

## 2. LTE Network Architecture

LTE-এর মূল network architecture-কে সাধারণত দুই ভাগে দেখা হয়:

UE (User Equipment)

মোবাইল ফোন / LTE device

E-UTRAN

eNodeB — Radio Access Network

EPC (Evolved Packet Core)

MME

Control plane

HSS

Subscriber data

S-GW

User-plane routing

P-GW

External data network

Internet / IMS

Data service / VoLTE service

### প্রতিটি component-এর কাজ

- UE: ব্যবহারকারীর ফোন বা LTE device।
- eNodeB: Radio communication, scheduling এবং handover-সংক্রান্ত radio কাজ।
- MME: Attach, mobility management ও control-plane signalling।
- HSS: Subscriber profile এবং authentication-সংক্রান্ত তথ্য।
- S-GW: LTE user-plane packet forwarding ও mobility-সংক্রান্ত ভূমিকা।
- P-GW: External packet data network-এ সংযোগ এবং IP connectivity-সংক্রান্ত ভূমিকা।
- IMS: VoLTE-সহ IP Multimedia Service পরিচালনার architecture।

একটি সহজ নিয়ম: MME = control plane; S-GW/P-GW = user-plane packet path-এর গুরুত্বপূর্ণ অংশ।

## 3. LTE Attach Procedure কী?

LTE Attach Procedure হলো এমন একটি signalling process, যার মাধ্যমে মোবাইল ডিভাইস LTE network-এ নিবন্ধিত হয় এবং প্রয়োজনীয় শর্ত পূরণ হলে data service ব্যবহারের ব্যবস্থা পায়।

1\. UE → eNodeB

Attach Request পাঠায়

2\. eNodeB → MME

NAS signalling MME-তে পৌঁছে দেয়

3\. MME ↔ HSS / Authentication

Subscriber identity, authentication ও subscription যাচাই

4\. Bearer Establishment

প্রয়োজনীয় control ও user-plane configuration

5\. Attach Accept

সফল হলে UE Attach Complete পাঠাতে পারে; data service ব্যবহারের সুযোগ তৈরি হয়

এটি একটি simplified flow। বাস্তবে authentication, security setup, bearer establishment এবং অন্যান্য message-এর সুনির্দিষ্ট ক্রম পরিস্থিতি ও configuration অনুযায়ী কিছুটা ভিন্ন হতে পারে।

### Attach Procedure-এর পরীক্ষার গুরুত্বপূর্ণ শব্দ

| Term           | অর্থ                                                                         |
| -------------- | ---------------------------------------------------------------------------- |
| NAS            | Non-Access Stratum; UE ও core-এর মধ্যে signalling                            |
| Authentication | Subscriber-এর পরিচয় যাচাই                                                    |
| HSS            | Subscriber profile ও authentication data-এর কেন্দ্রীয় database               |
| Default bearer | UE-এর packet data connectivity-এর জন্য প্রাথমিক bearer                       |
| APN            | Access Point Name; কোন packet data network-এ সংযোগ হবে তা নির্ধারণে ব্যবহৃত  |
| GUTI           | Globally Unique Temporary UE Identity; অস্থায়ী পরিচয় হিসেবে ব্যবহৃত হতে পারে |

প্রশ্ন: LTE Attach Request কে পাঠায়?

উত্তর: UE বা মোবাইল ডিভাইস। eNodeB সেটিকে MME-এর দিকে বহন করে।

## 4. LTE-তে Data Packet কীভাবে যায়?

ধরা যাক, তুমি ফোনে একটি website খুলছ।

1. ফোন LTE radio link দিয়ে eNodeB-তে packet পাঠায়।
2. eNodeB packet-কে S-GW-এর দিকে পাঠায়।
3. S-GW থেকে packet P-GW-এর দিকে যায়।
4. P-GW external data network বা internet-এর সঙ্গে যোগাযোগ করায়।
5. Response packet বিপরীত পথে ফিরে আসে।

এটিকে সাধারণভাবে বলা যায়:

UE → eNodeB → S-GW → P-GW → Internet

এটি user-plane-এর সরলীকৃত path। MME signalling ও connection management-এ ভূমিকা রাখে, কিন্তু সাধারণ user data packet-এর মূল forwarding path-এর অংশ নয়।

### LTE Interface মনে রাখার কৌশল

| Interface | সংযোগ                               |
| --------- | ----------------------------------- |
| S1-MME    | eNodeB ↔ MME                        |
| S1-U      | eNodeB ↔ S-GW                       |
| S5/S8     | S-GW ↔ P-GW                         |
| S6a       | MME ↔ HSS                           |
| SGi       | P-GW ↔ External packet data network |

## 5. Voice Call Flow: 2G বনাম VoLTE

### 2G GSM Voice Call

2G-এর circuit-switched voice network-এ সাধারণত:

Mobile → BTS → BSC → MSC → Destination network/mobile

- BTS radio interface পরিচালনা করে।
- BSC একাধিক BTS-এর radio resources পরিচালনায় ভূমিকা রাখে।
- MSC call setup ও switching পরিচালনা করে।

### VoLTE Call

VoLTE হলো LTE network-এর ওপর IP-based voice service। এতে IMS গুরুত্বপূর্ণ ভূমিকা পালন করে এবং SIP signalling ব্যবহৃত হয়।

Mobile A

eNodeB + EPC

LTE connectivity ও packet transport

IMS / SIP

Call signalling ও session control

Mobile B / Destination network

### SIP-এর গুরুত্বপূর্ণ message

- INVITE: Session শুরু করার অনুরোধ।
- 100 Trying: Request processing চলছে।
- 180 Ringing: অপর প্রান্তে ফোন ring করছে।
- 200 OK: Request সফলভাবে গ্রহণ করা হয়েছে।
- ACK: সফল session response নিশ্চিত করে।
- BYE: Session শেষ করার জন্য ব্যবহৃত হয়।

মনে রাখবে, SIP call signalling পরিচালনা করে; voice media সাধারণত RTP/RTCP-ভিত্তিক transport ব্যবহার করে। বাস্তব call flow-তে অতিরিক্ত message-ও থাকতে পারে।

## 6. 5G Core: গুরুত্বপূর্ণ Component

| Component | প্রধান কাজ                   |
| --------- | ---------------------------- |
| AMF       | Access ও mobility management |
| SMF       | Session management           |
| UPF       | User-plane packet forwarding |
| UDM       | Subscriber data management   |
| AUSF      | Authentication service       |
| PCF       | Policy control               |
| NRF       | Network function discovery   |
| NSSF      | Network slice selection      |

সহজে মনে রাখবে: AMF = mobility, SMF = session, UPF = user data।

LTE-এর EPC-এর সঙ্গে 5G Core-এর পার্থক্য হলো 5G Core-এ service-based architecture এবং আরও modular network functions ব্যবহৃত হয়।

## 7. Teletalk Technical Exam: Quick Interview Questions

| প্রশ্ন                                           | সংক্ষিপ্ত উত্তর                                    |
| ------------------------------------------------ | -------------------------------------------------- |
| GSM কোন generation-এর প্রযুক্তি?                 | 2G                                                 |
| NodeB কোন generation-এ ব্যবহৃত হয়?               | 3G                                                 |
| eNodeB কী?                                       | LTE base station                                   |
| gNodeB কী?                                       | 5G NR base station                                 |
| LTE-এর core network কী নামে পরিচিত?              | EPC                                                |
| MME-এর কাজ কী?                                   | Control-plane signalling ও mobility management     |
| HSS কী সংরক্ষণ করে?                              | Subscriber profile ও authentication-সংক্রান্ত তথ্য |
| LTE user-plane-এর গুরুত্বপূর্ণ gateway কোনগুলো?  | S-GW ও P-GW                                        |
| VoLTE-এর পূর্ণরূপ কী?                            | Voice over LTE                                     |
| IMS-এর একটি গুরুত্বপূর্ণ signalling protocol কী? | SIP                                                |
| SIP-এর INVITE কী করে?                            | Session শুরু করার অনুরোধ পাঠায়                     |
| 5G-তে user-plane packet forwarding কে করে?       | UPF                                                |
| 5G-তে session management কে করে?                 | SMF                                                |
| NAS-এর পূর্ণরূপ কী?                              | Non-Access Stratum                                 |
| APN-এর পূর্ণরূপ কী?                              | Access Point Name                                  |

## 8. Interactive MCQ Quiz

## Lesson 26 Quiz

0/15 answered

প্রতিটি প্রশ্নের একটি উত্তর নির্বাচন করে শেষে Check Answers চাপো।

1\. GSM সাধারণত কোন generation-এর প্রযুক্তি?

A. 2G

B. 3G

C. 4G

D. 5G

2\. LTE-এর base station কোনটি?

A. BTS

B. NodeB

C. eNodeB

D. gNodeB

3\. 5G NR-এর base station কী?

A. BSC

B. MSC

C. eNodeB

D. gNodeB

4\. LTE core network-এর নাম কী?

A. EPC

B. IMS

C. BSC

D. UTRAN

5\. LTE-তে control-plane signalling ও mobility management-এর দায়িত্ব প্রধানত কার?

A. UPF

B. MME

C. P-GW

D. RTP

6\. LTE-তে subscriber profile ও authentication-সংক্রান্ত তথ্যের জন্য কোন component গুরুত্বপূর্ণ?

A. HSS

B. eNodeB

C. S-GW

D. Nginx

7\. LTE-এর user-plane packet path-এর একটি সাধারণ ক্রম কোনটি?

A. UE → eNodeB → S-GW → P-GW

B. UE → HSS → MME → BTS

C. UE → IMS → BSC → HSS

D. UE → PCF → AMF → BSC

8\. VoLTE-এর পূর্ণরূপ কী?

A. Video over Long Ethernet

B. Voice over LTE

C. Voice on Local Exchange

D. Virtual Operator LTE

9\. SIP-এর INVITE message-এর উদ্দেশ্য কী?

A. Session শুরু করার অনুরোধ

B. IP address বরাদ্দ

C. Subscriber database মুছে ফেলা

D. Handover সম্পন্ন করা

10\. 5G Core-এ user-plane packet forwarding কে পরিচালনা করে?

A. AMF

B. AUSF

C. UPF

D. UDM

11\. 5G Core-এ session management-এর দায়িত্ব কার?

A. SMF

B. NRF

C. NSSF

D. HSS

12\. LTE Attach Request সাধারণত কে শুরু করে?

A. HSS

B. UE

C. P-GW

D. IMS

13\. LTE-তে eNodeB থেকে MME-এর control-plane interface কোনটি?

A. S1-U

B. SGi

C. S1-MME

D. S6a

14\. External packet data network-এর সঙ্গে P-GW-এর interface কোনটি?

A. S1-MME

B. S6a

C. S1-U

D. SGi

15\. LTE-এর তুলনায় 5G Core-এর একটি বৈশিষ্ট্য কী?

A. শুধু circuit switching

B. Service-based architecture

C. শুধু analog voice

D. কোনো user-plane নেই

Check Answers

পরবর্তী লেসন: Lesson 27 — Telecom Numerical Problems ও Exam Practice। সেখানে dB/dBm, link budget, optical power loss, subnetting, bandwidth, throughput এবং গুরুত্বপূর্ণ numerical MCQ অনুশীলন করব।

---
# Lesson 27: Telecom Numerical Problems ও Exam Practice

এই লেসনে Teletalk Bangladesh Limited-এর টেকনিক্যাল পরীক্ষার জন্য গুরুত্বপূর্ণ numerical problems অনুশীলন করব। প্রতিটি অঙ্কের formula, step-by-step solution এবং shortcut থাকবে।

আজকের বিষয়:

1. dB ও dBm calculation
2. Optical Fiber Power Budget
3. Microwave Link Budget ও FSPL
4. IP Subnetting
5. Bandwidth, Throughput ও Data Transfer Time
6. Telecom Numerical MCQ

## 1. dB ও dBm — সবচেয়ে গুরুত্বপূর্ণ

### dB কী?

dB (decibel) হলো দুটি power level-এর অনুপাত প্রকাশ করার logarithmic একক।

\\[ G\_{dB}=10\log\_{10}\left(\frac{P_2}{P_1}\right) \\]

এখানে \\(P_1\\) হলো reference power এবং \\(P_2\\) হলো measured power।

### dBm কী?

dBm হলো 1 milliwatt-এর তুলনায় absolute power level।

\\[ P\_{dBm}=10\log\_{10}(P\_{mW}) \\]

উল্টোভাবে,

\\[ P\_{mW}=10^{P\_{dBm}/10} \\]

### গুরুত্বপূর্ণ conversion table

| Power         | dBm         |
| ------------- | ----------- |
| 1 mW          | 0 dBm       |
| 2 mW          | প্রায় 3 dBm |
| 10 mW         | 10 dBm      |
| 100 mW        | 20 dBm      |
| 1 W = 1000 mW | 30 dBm      |
| 0.1 mW        | −10 dBm     |

Shortcut: Power 10 গুণ হলে dBm-এ 10 যোগ হবে; power 2 গুণ হলে প্রায় 3 dB যোগ হবে।

### Example 1: 100 mW-কে dBm-এ রূপান্তর

\\[ P\_{dBm}=10\log\_{10}(100) \\]

\\[ =10\times2=\boxed{20\ dBm} \\]

### Example 2: 30 dBm কত Watt?

\\[ P\_{mW}=10^{30/10}=1000\ mW \\]

অর্থাৎ,

\\[ \boxed{30\ dBm=1\ W} \\]

### Example 3: Power ratio 100 হলে gain কত?

\\[ G=10\log\_{10}(100) =\boxed{20\ dB} \\]

মনে রাখবে: dB ও dBm এক নয়। dB হলো ratio; dBm হলো নির্দিষ্ট reference-এর তুলনায় power।

## 2. Optical Fiber Power Budget

Optical fiber-এ transmitter থেকে receiver পর্যন্ত signal যাওয়ার সময় fiber, connector ও splice-এর কারণে power loss হয়।

মূল formula:

\\[ P_r=P_t-L\_{total} \\]

এখানে সব power dBm-এ এবং loss dB-এ প্রকাশিত।

মোট loss:

\\[ L\_{total}=\alpha D+L_c+L_s+L\_{other} \\]

- \\(\alpha\\) = fiber attenuation, dB/km
- \\(D\\) = fiber length, km
- \\(L_c\\) = connector loss
- \\(L_s\\) = splice loss

### Numerical Example

ধরা যাক:

- Transmitter power = \\(+3\\) dBm
- Fiber length = 10 km
- Attenuation = 0.2 dB/km
- Connector loss = 2 dB
- Splice loss = 1 dB

Step 1: Fiber loss

\\[ L_f=0.2\times10=2\ dB \\]

Step 2: Total loss

\\[ L\_{total}=2+2+1=5\ dB \\]

Step 3: Receiver power

\\[ P_r=3-5=\boxed{-2\ dBm} \\]

অর্থাৎ receiver-এ আনুমানিক −2 dBm power পাওয়া যাবে।

যদি receiver sensitivity −10 dBm হয়, তাহলে এই সরল হিসাব অনুযায়ী power sensitivity-এর চেয়ে বেশি। তবে বাস্তবে connector variation, aging এবং engineering margin-ও বিবেচনা করতে হবে।

## 3. Microwave Link Budget ও FSPL

Microwave link-এ দুটি tower-এর মধ্যে radio signal পাঠানো হয়। দূরত্ব বাড়লে এবং frequency পরিবর্তিত হলে free-space path loss পরিবর্তিত হয়।

### FSPL Formula

\\[ FSPL(dB)=92.45+20\log\_{10}(f)+20\log\_{10}(D) \\]

এখানে:

- \\(f\\) = frequency in GHz
- \\(D\\) = distance in km

### Numerical Example

ধরা যাক frequency = 6 GHz এবং distance = 10 km।

\\[ FSPL=92.45+20\log\_{10}(6)+20\log\_{10}(10) \\]

যেহেতু \\(\log\_{10}(6)\approx0.778\\) এবং \\(\log\_{10}(10)=1\\),

\\[ FSPL=92.45+15.56+20 \\]

\\[ \boxed{FSPL\approx128.01\ dB} \\]

### Link Budget Formula

\\[ P_r=P_t+G_t+G_r-L\_{total} \\]

ধরা যাক:

- Transmit power \\(P_t=20\\) dBm
- Transmit antenna gain \\(G_t=30\\) dBi
- Receive antenna gain \\(G_r=30\\) dBi
- FSPL = 128.01 dB
- অন্যান্য loss = 4 dB

তাহলে,

\\[ P_r=20+30+30-128.01-4 \\]

\\[ \boxed{P_r=-52.01\ dBm} \\]

যদি receiver sensitivity −70 dBm হয়:

\\[ Fade\ Margin=P_r-P\_{sensitivity} \\]

\\[ =-52.01-(-70)=\boxed{17.99\ dB} \\]

পরীক্ষার কৌশল: Link budget-এ gain যোগ করতে হবে এবং loss বিয়োগ করতে হবে। Sensitivity-এর তুলনায় received signal কত dB শক্তিশালী, সেটিই এই উদাহরণে fade margin।

## 4. IP Subnetting Numerical Problems

Subnetting হলো একটি IP network-কে ছোট ছোট network-এ ভাগ করা।

IPv4 address হলো 32 bit। CIDR notation-এ `/24`, `/26`, `/28` ইত্যাদি network prefix নির্দেশ করে।

### গুরুত্বপূর্ণ Formula

\\[ \text{Total addresses}=2^{(32-n)} \\]

এখানে \\(n\\) হলো prefix length।

সাধারণ IPv4 subnet-এ:

\\[ \text{Usable hosts}=2^{(32-n)}-2 \\]

এই usable-host formula সাধারণত প্রচলিত subnet-এ প্রযোজ্য; `/31` ও `/32`-এর ক্ষেত্রে বিশেষ নিয়ম আছে।

### Example 1: `/24` subnet-এ usable host কত?

\\[ 2^{32-24}-2=2^8-2 \\]

\\[ =256-2=\boxed{254} \\]

### Example 2: `/26` subnet-এ usable host কত?

\\[ 2^{32-26}-2=2^6-2 \\]

\\[ =64-2=\boxed{62} \\]

### Common Subnet Table

| CIDR | Subnet mask     | Total addresses | সাধারণ usable hosts |
| ---- | --------------- | --------------- | ------------------- |
| /24  | 255.255.255.0   | 256             | 254                 |
| /25  | 255.255.255.128 | 128             | 126                 |
| /26  | 255.255.255.192 | 64              | 62                  |
| /27  | 255.255.255.224 | 32              | 30                  |
| /28  | 255.255.255.240 | 16              | 14                  |
| /29  | 255.255.255.248 | 8               | 6                   |
| /30  | 255.255.255.252 | 4               | 2                   |

### Example 3: `192.168.1.0/26`

একটি `/26` subnet-এ block size হলো 64। তাই subnet range হবে:

- `192.168.1.0/26`
- `192.168.1.64/26`
- `192.168.1.128/26`
- `192.168.1.192/26`

প্রথম subnet-এর জন্য:

| বিষয়              | Address        |
| ----------------- | -------------- |
| Network address   | `192.168.1.0`  |
| First usable host | `192.168.1.1`  |
| Last usable host  | `192.168.1.62` |
| Broadcast address | `192.168.1.63` |

Shortcut: `/26` হলে block size 64; `/27` হলে 32; `/28` হলে 16।

## 5. Bandwidth, Throughput ও Data Transfer Time

Bandwidth হলো কোনো channel-এর capacity বা frequency range-এর পরিমাপ—প্রসঙ্গ অনুযায়ী অর্থ আলাদা হতে পারে। Digital networking-এ bandwidth শব্দটি প্রায়ই সর্বোচ্চ data-carrying capacity বোঝাতে ব্যবহৃত হয়।

Throughput হলো বাস্তবে প্রতি সেকেন্ডে যত data transfer হয়।

### Numerical Example 1: Data transfer time

একটি 100 MB file, 20 Mbps speed-এ download করতে কত সময় লাগবে?

ধরি, 1 byte = 8 bits এবং protocol overhead উপেক্ষা করছি।

\\[ 100\ MB=100\times8=800\ Mb \\]

\\[ Time=\frac{Data}{Rate} \\]

\\[ Time=\frac{800\ Mb}{20\ Mbps} =\boxed{40\ seconds} \\]

এটি theoretical estimate। বাস্তবে protocol overhead, network congestion এবং speed variation-এর কারণে সময় বেশি হতে পারে।

### Numerical Example 2: Throughput efficiency

একটি connection-এর theoretical rate 100 Mbps, কিন্তু measured throughput 80 Mbps।

\\[ Efficiency=\frac{80}{100}\times100 \\]

\\[ \boxed{80\\%} \\]

এখানে throughput efficiency 80%।

### Numerical Example 3: Frequency bandwidth

কোনো radio channel-এর upper frequency 1850 MHz এবং lower frequency 1800 MHz।

\\[ Bandwidth=f\_{upper}-f\_{lower} \\]

\\[ =1850-1800=\boxed{50\ MHz} \\]

## 6. গুরুত্বপূর্ণ Telecom Numerical Formula Sheet

| বিষয়                  | Formula                                                  |
| --------------------- | -------------------------------------------------------- |
| dBm থেকে mW           | \\(P\_{mW}=10^{P\_{dBm}/10}\\)                           |
| mW থেকে dBm           | \\(P\_{dBm}=10\log\_{10}(P\_{mW})\\)                     |
| Power gain            | \\(G\_{dB}=10\log\_{10}(P_2/P_1)\\)                      |
| Fiber receiver power  | \\(P_r=P_t-L\_{total}\\)                                 |
| Microwave link budget | \\(P_r=P_t+G_t+G_r-L\_{total}\\)                         |
| FSPL                  | \\(92.45+20\log\_{10}(f\_{GHz})+20\log\_{10}(D\_{km})\\) |
| IPv4 total addresses  | \\(2^{32-n}\\)                                           |
| সাধারণ usable hosts   | \\(2^{32-n}-2\\)                                         |
| Data transfer time    | Data size in bits ÷ rate in bits/s                       |
| Bandwidth             | \\(f\_{upper}-f\_{lower}\\)                              |
| Success rate          | Successful attempts ÷ total attempts × 100%              |

## 7. Teletalk Technical Exam — Numerical MCQ Quiz

নিজে হিসাব করে উত্তর দাও। শেষে Check Answers চাপলে সঠিক উত্তর ও ব্যাখ্যা দেখতে পাবে।

## Lesson 27 Quiz

0/15 answered

1\. 100 mW কত dBm?

A. 10 dBm

B. 20 dBm

C. 30 dBm

D. 40 dBm

2\. 30 dBm কত Watt?

A. 0.1 W

B. 0.5 W

C. 1 W

D. 10 W

3\. 10 km fiber-এর attenuation 0.2 dB/km হলে fiber loss কত?

A. 0.2 dB

B. 1 dB

C. 2 dB

D. 20 dB

4\. Transmitter power +3 dBm এবং total loss 5 dB হলে receiver power কত?

A. +8 dBm

B. +2 dBm

C. −2 dBm

D. −8 dBm

5\. 6 GHz ও 10 km দূরত্বে FSPL প্রায় কত?

A. 98 dB

B. 108 dB

C. 118 dB

D. 128 dB

6\. Received power −50 dBm এবং sensitivity −70 dBm হলে fade margin কত?

A. 10 dB

B. 20 dB

C. −20 dB

D. 120 dB

7\. /24 IPv4 subnet-এ সাধারণত usable host কত?

A. 128

B. 254

C. 256

D. 512

8\. /27 subnet-এ সাধারণত usable host কত?

A. 14

B. 30

C. 32

D. 62

9\. /26 subnet-এর block size কত?

A. 16

B. 32

C. 64

D. 128

10\. 100 MB file 20 Mbps-এ download করতে theoretical সময় কত?

A. 4 seconds

B. 20 seconds

C. 40 seconds

D. 80 seconds

11\. 100 Mbps theoretical rate-এ 80 Mbps throughput হলে efficiency কত?

A. 20%

B. 50%

C. 80%

D. 125%

12\. Upper frequency 1850 MHz এবং lower frequency 1800 MHz হলে bandwidth কত?

A. 25 MHz

B. 50 MHz

C. 100 MHz

D. 3650 MHz

13\. Power 10 গুণ হলে power gain কত?

A. 1 dB

B. 3 dB

C. 10 dB

D. 20 dB

14\. 192.168.1.0/26 subnet-এর broadcast address কোনটি?

A. 192.168.1.1

B. 192.168.1.62

C. 192.168.1.63

D. 192.168.1.64

15\. Link budget-এ antenna gain-এর সঙ্গে কী করা হয়?

A. বিয়োগ করা হয়

B. যোগ করা হয়

C. সব সময় শূন্য ধরা হয়

D. শুধু ভাগ করা হয়

Check Answers

পরবর্তী ক্লাস — Lesson 28: Teletalk Technical Exam-এর জন্য Full Model Test: Telecom, Networking, Optical Fiber, Linux, DBMS, Operating Systems, Programming এবং Numerical MCQ—সব মিলিয়ে একটি পূর্ণাঙ্গ অনুশীলনী পরীক্ষা।

# Lesson 28: Teletalk Technical Exam — Full Model Test

আজকের ক্লাসে আগের ২৭টি লেসনের গুরুত্বপূর্ণ বিষয় থেকে একটি পূর্ণাঙ্গ মডেল টেস্ট দিচ্ছি। এতে Telecom, Networking, Optical Fiber, Linux, DBMS, Operating Systems, Programming এবং Numerical Problems থাকবে।

পরীক্ষার নিয়ম

- মোট প্রশ্ন: ৪০টি MCQ
- প্রতিটি প্রশ্ন: ১ নম্বর
- মোট নম্বর: ৪০
- প্রস্তাবিত সময়: ৩৫ মিনিট
- প্রথমে উত্তর দেবে, তারপর Check Answers চাপবে।
- এটি অনুশীলনী পরীক্ষা; Teletalk-এর অফিসিয়াল প্রশ্নপত্র নয়।

## Part A — Telecom & Mobile Networks (১০ নম্বর)

## Full Model Test — 40 MCQ

0/40 answered

প্রস্তাবিত সময়: ৩৫ মিনিট

1\. GSM সাধারণত কোন generation-এর প্রযুক্তি?

A. 2G

B. 3G

C. 4G

D. 5G

2\. LTE network-এর base station কোনটি?

A. BTS

B. NodeB

C. eNodeB

D. gNodeB

3\. 5G Core-এ user-plane packet forwarding-এর দায়িত্ব কার?

A. AMF

B. UPF

C. AUSF

D. UDM

4\. VoLTE-এর পূর্ণরূপ কী?

A. Voice over LTE

B. Video on Long Ethernet

C. Voice on Local Exchange

D. Virtual Operator LTE

5\. LTE-তে RSRP কী পরিমাপ করে?

A. শুধু latency

B. Reference signal-এর received power

C. Download speed

D. Packet loss

6\. 1000টি handover attempt-এর 950টি সফল হলে success rate কত?

A. 90%

B. 92%

C. 95%

D. 98%

7\. Optical fiber-এ আলো চলার প্রধান নীতি কোনটি?

A. Electromagnetic induction

B. Total internal reflection

C. Photoelectric effect

D. Nuclear fusion

8\. GPON-এ OLT-এর কাজ কী?

A. শুধু Wi-Fi password তৈরি

B. Optical access network-এর central-side equipment হিসেবে কাজ

C. Mobile SIM authenticate করা

D. DNS resolve করা

9\. OTDR প্রধানত কী কাজে লাগে?

A. Fiber link-এর fault ও distance নির্ণয়ে

B. CPU temperature মাপতে

C. IP address দিতে

D. Database backup করতে

10\. E1-এর nominal data rate কত?

A. 1.024 Mbit/s

B. 2.048 Mbit/s

C. 8.192 Mbit/s

D. 155.52 Mbit/s

11\. TCP কোন ধরনের protocol?

A. Connection-oriented transport protocol

B. Connectionless network-layer protocol

C. Optical signalling standard

D. Database query language

12\. DNS-এর প্রধান কাজ কী?

A. Domain name-কে IP address-এর সঙ্গে resolve করা

B. IP packet encrypt করা

C. CPU schedule করা

D. RAM allocate করা

13\. HTTPS-এর default port কোনটি?

A. 21

B. 25

C. 80

D. 443

14\. IPv4 address কত bit-এর?

A. 16 bit

B. 32 bit

C. 64 bit

D. 128 bit

15\. Router প্রধানত কী করে?

A. ভিন্ন IP network-এর মধ্যে packet forward করে

B. শুধু file edit করে

C. Database normalize করে

D. শুধু optical power মাপে

16\. VLAN-এর প্রধান উদ্দেশ্য কী?

A. Logical network segmentation

B. CPU clock বাড়ানো

C. Fiber attenuation কমানো

D. Password hash করা

17\. Linux-এ বর্তমান directory-এর path দেখানোর command কোনটি?

A. pwd

B. mkdir

C. grep

D. chmod

18\. Linux-এ file permission পরিবর্তনের command কোনটি?

A. ps

B. chmod

C. ping

D. cat

19\. Linux-এ systemd service-এর status দেখতে কোন command ব্যবহৃত হয়?

A. systemctl status

B. ipconfig status

C. sql status

D. python status

20\. Linux-এ সাধারণত system log দেখতে কোন command ব্যবহার করা যায়?

A. journalctl

B. touch

C. rmdir

D. whoami

21\. DBMS-এর পূর্ণরূপ কী?

A. Database Management System

B. Data Binary Machine Service

C. Digital Base Memory Structure

D. Database Monitoring Syntax

22\. Table-এর প্রতিটি row-কে uniquely identify করতে কোন key ব্যবহৃত হয়?

A. Foreign key

B. Primary key

C. Non-unique index

D. Wildcard

23\. SQL-এ data query করার জন্য সাধারণত কোন command ব্যবহৃত হয়?

A. SELECT

B. COMMIT

C. GRANT

D. DROP

24\. ACID-এর A কী বোঝায়?

A. Availability

B. Atomicity

C. Authorization

D. Addressing

25\. Foreign key-এর প্রধান কাজ কী?

A. Table-এর মধ্যে referential relationship বজায় রাখা

B. CPU register তৈরি

C. Internet speed দ্বিগুণ করা

D. File permission দেওয়া

26\. Operating System-এর প্রধান কাজ কোনটি?

A. Hardware ও software resource পরিচালনা

B. শুধু presentation তৈরি

C. শুধু webpage design

D. শুধু email পাঠানো

27\. একই process-এর মধ্যে lightweight execution unit কোনটি?

A. Thread

B. Table

C. Router

D. Packet

28\. কোন scheduling algorithm-এ সাধারণত fixed time quantum ব্যবহৃত হয়?

A. FCFS

B. Round Robin

C. Non-preemptive SJF

D. FIFO page replacement

29\. Deadlock-এর চারটি necessary condition-এর একটি কোনটি?

A. Circular wait

B. Data compression

C. DNS resolution

D. Optical reflection

30\. CPU-এর arithmetic ও logical operation সম্পাদনের unit কোনটি?

A. ALU

B. CU

C. RAM

D. NIC

31\. Python-এ list-এর বৈশিষ্ট্য কোনটি?

A. Ordered এবং mutable

B. সবসময় immutable

C. শুধু integer রাখে

D. Key-value pair ছাড়া অন্য কিছু নয়

32\. OOP-এ inheritance কী?

A. এক class-এর অন্য class-এর বৈশিষ্ট্য/আচরণ উত্তরাধিকারসূত্রে নেওয়া

B. Variable মুছে ফেলা

C. IP address assign করা

D. SQL query optimize করা

33\. Binary 1010-এর decimal মান কত?

A. 8

B. 9

C. 10

D. 12

34\. 30 dBm কত Watt?

A. 0.01 W

B. 0.1 W

C. 1 W

D. 10 W

35\. 10 km fiber-এর attenuation 0.2 dB/km হলে fiber loss কত?

A. 0.2 dB

B. 2 dB

C. 5 dB

D. 20 dB

36\. /26 IPv4 subnet-এ সাধারণত usable host কত?

A. 30

B. 32

C. 62

D. 126

37\. 100 MB file 20 Mbps-এ স্থানান্তর করতে theoretical সময় কত?

A. 4 s

B. 20 s

C. 40 s

D. 80 s

38\. 1850 MHz থেকে 1800 MHz পর্যন্ত frequency range-এর bandwidth কত?

A. 25 MHz

B. 50 MHz

C. 100 MHz

D. 3650 MHz

39\. Power ratio 100 হলে gain কত dB?

A. 10 dB

B. 20 dB

C. 30 dB

D. 100 dB

40\. 100 Mbps link-এ measured throughput 75 Mbps হলে efficiency কত?

A. 25%

B. 50%

C. 75%

D. 125%

Submit & Check Answers

## পরীক্ষার ফল অনুযায়ী পরবর্তী প্রস্তুতি

তোমার স্কোর দেখার পর এইভাবে এগোবে:

- ৩৬–৪০: কঠিন numerical ও interview question অনুশীলন করো।
- ৩০–৩৫: Telecom architecture, networking ও subnetting রিভিশন করো।
- ২০–২৯: যেসব বিষয়ে ভুল হয়েছে, সেগুলোর আগের লেসন আবার পড়ো।
- ২০-এর নিচে: প্রতিদিন ২টি topic পড়ো, তারপর MCQ দিয়ে নিজেকে যাচাই করো।

পরামর্শ: Teletalk-এর পরীক্ষার প্রস্তুতিতে শুধু telecom নয়, networking, DBMS, operating systems, programming, সাধারণ গণিত ও ইংরেজিও গুরুত্ব দিয়ে পড়বে। নিয়োগ বিজ্ঞপ্তিতে যে syllabus দেওয়া আছে, সেটিই চূড়ান্ত অগ্রাধিকার পাবে।