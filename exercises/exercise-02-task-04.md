# Exercise 2 — Exfiltrate a Sensitive File

## Task 4 — Simulated File Exfiltration with Steganography

**Environment:** Authorized Practice Labs training environment  
**Data:** Lab-provided placeholder text  
**Evidence status:** Workflow and expected results documented from supplied instructions; transfer and extraction screenshots have not been supplied.

## Objective

Demonstrate how a lab text file can be embedded in an image, transferred between lab machines, and recovered. The exercise uses placeholder content to simulate sensitive data.

## Workflow

### 1. Prepare the Image on PLABWIN10

In OpenStego, **Hide data** is used with the following inputs:

| Field | Lab value |
| --- | --- |
| Message file | `CEO_Eyes_Only` in `\\PLABDC01\Practicelabs-Sharedrive\Operations` |
| Cover image | `TowerBridge.jpg` in Pablo's Documents folder |
| Output image | `TowerBridge.png` |
| Password | Lab-specified steganography password; omitted from public documentation |

The instructed success message indicates that OpenStego has created an image containing the embedded file.

### 2. Transfer the Output Image to PLABKALI

The lab describes using SMB access to PLABWIN10's administrative share at `192.168.0.4`, navigating to Pablo's Documents folder, and retrieving `TowerBridge.png`.

This is a transfer between machines inside the lab. The instructions use a subsequent download outside the lab interface to simulate receipt at an external destination. The internal SMB transfer alone does not establish that data left the domain.

### 3. Recover the Embedded Text

OpenStego's **Extract data** function on Kali is configured with `TowerBridge.png` as the input image and `/home/plabadmin` as the output directory. The same lab-specified password is supplied to extract the message.

The stated final result is `CEO_Eyes_Only.txt`, containing Lorem Ipsum placeholder text.

## Expected Validation

| Stage | Evidence needed |
| --- | --- |
| Image creation | OpenStego success message and output image |
| Transfer | Successful retrieval of `TowerBridge.png` on Kali |
| Extraction | OpenStego extraction success message |
| Recovery | Extracted `CEO_Eyes_Only.txt` and its placeholder contents |

The named screenshots in the instructions are evidence targets, not attachments verified in this repository.

## Portfolio Evidence Labels

- **Lab Text File Selected for Steganography**
- **Cover Image and Output File Configured**
- **Embedded Image Created Successfully**
- **Stego Image Transferred to Kali**
- **Embedded Text Extracted Successfully**
- **Recovered Placeholder File Verified**

## Findings and Interpretation

The workflow illustrates that a viewable image can carry additional embedded data. Visual inspection of the picture alone is not a reliable test for hidden content. A complete demonstration requires both successful transfer and recovery of the embedded file.

This section records a simulated exfiltration exercise, not the movement of actual sensitive business information. Execution results will be added when supporting screenshots are available.

## Skills Covered

- Configuring steganography inputs and outputs.
- Distinguishing image creation, file transfer, and data recovery.
- Separating internal transfer from simulated external receipt.
- Validating results with evidence at each stage.

[Previous: Task 3](exercise-02-task-03.md) | [Project overview](../README.md)
