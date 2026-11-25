# 2026 Digital Forensics Cup Preliminary

This write-up reconstructs selected preliminary-round questions from our competition notes. The notes record 26 answers as verified during the investigation. Four questions were left open, and one answer was provisional. The original images were unavailable for a fresh verification of this write-up. The server notes preserve the answers but give only partial artifact locations.

## Mobile and computer forensics

| Question | Recorded answer | Evidence and verification |
| --- | --- | --- |
| 65 | Device serial omitted | Read the `Serial Number` field in `Info.plist` from the Apple device backup on the computer. |
| 66 | `39.894585` | In the decrypted backup, find `IMG_0017.JPG` in the `ZASSET` table of `Photos.sqlite`. Round its `ZLATITUDE` value, `39.89458494672165`, to six decimal places. |
| 67 | Conversation identifier omitted | Locate the original question about recovering deleted WeChat chats in the Doubao database's `MessageTable`. Read `conversation_id` from that row. |
| 68 | `26.10.232860` | Read `CFBundleVersion` for the main WPS app in `Manifest.plist`. The separate `iTunesMetadata.bundleVersion` field contains `26.10.0232860`. |
| 69 | `2333` | Find the browser `History` entry titled “iPhone - 文件闪传” and extract the port from its HTTP URL. |
| 70 | `d97af6f22cf196a5d37d5e4c200b7657acb9af67462aa41d969d13527dee1612` | Match the asset UUID in the browser's download URL to the original JPEG in the phone's photo library. The extracted original was 526,119 bytes, matching the browser's recorded download size. Compute SHA-256 over that original. |
| 71 | `/storage/Users/currentUser/Download/com.xiaolifaa.fastfiletransfer/0001.docx` | Find `0001.docx` in the `file_record` table of Huawei File Transfer's `FSend.db` and read the saved destination path. |
| 72 | `HZ02-2026-1147` | Open the computer's downloaded copy of `0001.docx` as an archive. Read the project number from the embedded approval image at `_rels/0001.jpeg`. |
| 74 | Wallet address omitted | Read `_rels/address.txt` from the same document archive. |
| 75 | Card suffix omitted | Read the cloned WeChat account's payment exchange in order. One message names the card suffix, and a later message confirms receipt of 100,000 yuan. |
| 76 | Bangkok (`曼谷`) | The Apple backup's WeChat conversation records an instruction to book a one-way ticket to Bangkok on the 19th of that month. |
| 77 | Account identifier omitted | Match the number supplied in the question against the contact BLOB in the `Friend` table of `WCDB_Contact.sqlite`. Read `userName` from the matching row. |

| Question | Status | Remaining evidence |
| --- | --- | --- |
| 73 | Open | Recover the original file from the USB evidence. |
| 78 | Open | Obtain the hidden-volume ledger and deduplicate its entries. |
| 79 | Open | Recover the target ZIP archive. |
| 80 | Provisional | Chat records suggest a balance of 350,000 yuan (450,000 minus 100,000). Verify against the hidden-volume ledger and transfer receipts. |
| 81 | Open | Verify the RAR password against the recovered archive. |

## Program analysis

| Question | Recorded answer | Evidence and verification |
| --- | --- | --- |
| 99 | `3` | Inspect the PE import table of `launcher.exe`. It imports `KERNEL32.dll`, `msvcrt.dll`, and `USER32.dll`. |
| 100 | `0x33` and `0x5a` | In the input-validation routine, `0x33` decodes the reference string. The program XORs the input with `0x5a` before Base64 encoding and comparison. |
| 101 | `flag{V1ctory_bel0ngs_to_th3_most_t3naC1ous--Ro1and_Garr0s}` | Decode the embedded target flag bytes with XOR `0x5a`. The requested answer uses the `flag{...}` format. |
| 102 | `2f1a6e2d5b` | Reproduce the `PACK1` extraction to recover the 1,098,752-byte worker PE. Reproduce the two 3DES-CBC rounds with padding. The first round takes the first 24 bytes and last 8 bytes of the original launcher as its key and IV. The second round takes the last 24 bytes and first 8 bytes. The recorded BCrypt and independent implementations agreed on a 1,098,768-byte output. |

The regenerated Q102 output had SHA-256 `4bfa124c9b4c04e8dfe295aac71511415d5658afd91185aece0e022f1a6e2d5b`. The submitted value is its final ten hexadecimal characters.

## Server forensics

| Question | Recorded answer | Evidence or scope of the saved notes |
| --- | --- | --- |
| 109 | `export_7318.mp4` | Match the complete export to the clue clip by visuals, on-screen text, and narration. |
| 110 | Account identifier omitted | The answer identifies the local workbench login associated with the matching export job. |
| 111 | Share URL omitted | The saved URL uses HTTP on port `8392`. The resource path contains the workbench's share identifier. |
| 112 | `2026-11-14 23:43:52` | The saved notes record the timestamp. Its source field and timezone are unavailable. |
| 113 | `LIC-218-4705` | The notes reference a recovered Q-218 authorization image, `license_Q-218.png`. |
| 114 | `WH-0314` | The saved notes record the value. Its source artifact is unavailable. |
| 115 | `vsynth-data` | The saved notes record the value. Its source artifact is unavailable. |
| 116 | `wh-promo.example.com` | The saved notes record the domain. Its source artifact is unavailable. |
| 117 | `38` | The count covers outbound orders whose fulfillment changed from `3PL-HX` to `SELF`. |
| 118 | `7` | The count uses UTC, the timezone recorded in the server logs. The saved notes do not specify the complete filter. |
