# Procurement Data Automation
An end-to-end intelligent data pipeline built on the Databricks Lakehouse Platform (Unity Catalog) that **automates procurement document processing, matching, and validation** using advanced AI and LLM foundation models.

# Business Need Overview

## PO, Invoice & Goods Receipt Matching

### 2-Way Match — PO vs Invoice

* Match **PO Number, Vendor Name, and Material Name**.
* Validate invoice amount:
  `PO Quantity × PO Unit Price = Invoice Amount`

### 3-Way Match — PO vs Invoice vs Goods Receipt (GR)

* Perform all **2-way match checks**.
* Validate invoiced quantity:
  `Invoice Quantity = GR Received Quantity`
* Validate **delivery dates** against the PO and goods receipt records.


# Project Architecture 

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/473c67d2-40c6-4169-ae53-d1e76075764b" />



---

## 🏗️ Architecture Overview

The pipeline implements a modern Medallion Architecture combined with AI-driven extraction and validation:

* **Source Data (Staging Volume):** Ingests raw procurement documents (**Purchase Order PDF**, **Good Receive PDF**, and **Invoice PDF**) into Unity Catalog volumes.
* **Bronze Layer (Delta Lake):** Uses **Delta Live Tables (DLT)** to capture and store unstructured PDF text reliably.
* **Silver Layer (Delta Lake & LLM Foundation Model):** Leverages **AI Plus LLM Foundation Models** to extract, parse, and structure raw text into standardized formats, generating rich embeddings.
* **Validation & Processing Layer:** Processes structured data through specialized indexing modules (*Purchase Order VS Index*, *Good Receive VS Index*, and *Invoice VS Index*) before passing them to a central LLM validation engine.
* **Gold Layer & Alerting:** 
  * **Matching Success:** Automatically promotes validated, matching records to Gold **Delta Lake** tables feeding an executive **Dashboard**.
  * **Discrepancies:** Triggers automated notifications via **Gmail** for any non-matching purchase orders requiring manual review.

---

## 🚀 Key Technologies

* **Platform:** Databricks, Unity Catalog (Catalog, Schema, Tables, Volumes)
* **Storage & Processing:** Delta Lake, Delta Live Tables (DLT)
* **AI / ML:** AI Plus LLM Foundation Models, Embeddings
* **Visualization & Action:** Databricks Dashboards, Automated Email Alerts
