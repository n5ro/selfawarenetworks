This folder will contain the original PDF's that I uploaded to Figshare. 

They contain — Neutral, machine‑readable timestamps (no Wayback required)

Example 1: 
From the PDFs’ own metadata (creation times in UTC):

Draft 35: /CreationDate: D:20250325100216Z (Mar 25 2025, 10:02:16 UTC).
(File: “Super Information Theory Draft 35.pdf”.)

Draft 36: /CreationDate: D:20250629083729Z (Jun 29 2025, 08:37:29 UTC).
(File: “Super_Information_Theory36.pdf”.)

These are embedded by pdfTeX at build time and are independent of Wayback. (For your records, SHA‑256 fingerprints:
Draft 35 = 3ac9371d30a6714521130de076d338eaef46539eb439026f199769250fbfc0c7;
Draft 36 = f224a4409d24c3d975c8183d9302a531444f916c75064a19b369848098c97c86.)

Example 2:

Does this file (Draft 36) have an SHA-256 hash that proves it's time-stamp?

# Path to the uploaded file
file_path = "/mnt/data/Super_Information_Theory36.pdf"

# Calculate SHA-256 hash
sha256_hash = hashlib.sha256()
with open(file_path, "rb") as f:
    for byte_block in iter(lambda: f.read(4096), b""):
        sha256_hash.update(byte_block)

file_hash = sha256_hash.hexdigest()
file_hash

Result
'f224a4409d24c3d975c8183d9302a531444f916c75064a19b369848098c97c86'

Yes. The uploaded file has the following SHA-256 hash:

f224a4409d24c3d975c8183d9302a531444f916c75064a19b369848098c97c86


This hash uniquely identifies the exact contents of the file.

To prove a timestamp, you would need to anchor this hash in a trusted time-stamping service (e.g., blockchain record, notarization, or archival system like the Wayback Machine). On its own, the SHA-256 hash only proves integrity (that the file hasn’t been altered) but not when it existed.

Do you want me to show you how to create a cryptographically verifiable timestamp for this hash (for example, via blockchain or archival submission)? 

Example 3:

# Let's extract the PDF metadata, focusing on /CreationDate and /ModDate.
from PyPDF2 import PdfReader

path = "/mnt/data/Super_Information_Theory36.pdf"
reader = PdfReader(path)

docinfo = reader.metadata  # returns a DocumentInformation object (dict-like)
docinfo_dict = {}
for k, v in docinfo.items():
    docinfo_dict[str(k)] = str(v)

# Pull common keys
creation = docinfo_dict.get("/CreationDate")
moddate = docinfo_dict.get("/ModDate")

creation, moddate, docinfo_dict

Result
('D:20250629083729Z',
 'D:20250629083729Z',
 {'/Author': '',
  '/CreationDate': 'D:20250629083729Z',
  '/Creator': 'LaTeX with hyperref',
  '/Keywords': '',
  '/ModDate': 'D:20250629083729Z',
  '/PTEX.Fullbanner': 'This is pdfTeX, Version 3.141592653-2.6-1.40.26 (TeX Live 2024) kpathsea version 6.4.0',
  '/Producer': 'pdfTeX-1.40.26',
  '/Subject': '',
  '/Title': '',
  '/Trapped': '/False'})
Thought for 6s

Perfect—this is exactly the kind of neutral, machine-readable timestamp PDFs carry.

Here’s what I verified from the uploaded Draft 36 file (“Super_Information_Theory36.pdf”):

/CreationDate: D:20250629083729Z → 2025-06-29 08:37:29 UTC

/ModDate: D:20250629083729Z → 2025-06-29 08:37:29 UTC

Producer: pdfTeX-1.40.26 (via LaTeX + hyperref)

SHA-256: f224a4409d24c3d975c8183d9302a531444f916c75064a19b369848098c97c86 (matches your fingerprint)

Your Draft 35 details are in the correct pdfTeX format too:

/CreationDate: D:20250325100216Z → 2025-03-25 10:02:16 UTC

SHA-256 (as you noted): 3ac9371d30a6714521130de076d338eaef46539eb439026f199769250fbfc0c7

Notes:

These /CreationDate strings are embedded by the PDF engine at build time in UTC (the trailing Z) and are machine-readable and neutral (no Wayback needed).

A hash proves integrity; the embedded UTC creation time provides an internal timestamp. If you also record the hash in an external, immutable log (e.g., a blockchain tx, notarization, or public commit) you get a stronger, independently anchored time proof.

If you want, share Draft 35 and I’ll extract and confirm its metadata and SHA-256 the same way.
