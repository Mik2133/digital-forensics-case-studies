# Digital Forensics Case Studies

English case studies from my digital-forensics practice with competition evidence. I focus on the question, the specific artifact that supports an answer, and the limits of what the evidence establishes.

## Cases

| Event | Focus | Status |
|---|---|---|
| [2025 Shuzheng Cup preliminary](shuzheng-cup-2025/README.md) | Linux logs, disk hashes, Docker, Kubernetes, and application configuration | Selected server-forensics questions documented; one reference answer remains unverified |

## Method

1. Identify the relevant evidence image and preserve the original data.
2. Record the artifact path and the exact observation behind each answer.
3. Separate original evidence from changes introduced by booting a forensic copy.
4. Mark answers that come from a reference write-up until they can be independently reproduced.

This repository contains written analysis only. It does not publish disk images, credentials, or raw application configuration.

For challenge-based CTF write-ups, see my [CTF writeups](https://github.com/Mik2133/ctf-writeups).
