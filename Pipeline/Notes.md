# Ontology

## Background Research

### Using the following prompt:

```
Goal
I need to determine whether it’s feasible to build a holistic, implementation-ready ontology for patient hospital bills that generalizes across bill types (inpatient, outpatient, professional, facility, pharmacy, etc.). I’m not asking you to invent an ontology. Instead, I want you to research and compile authoritative resources that define the structure of bills and related artifacts.

What to do (ordered):

Conclusion (first): In 3–6 sentences, state whether a holistic, implementation-ready ontology is feasible, with the main reasons.

Resources only (no original design): Find and list authoritative standards, specs, forms, data models, and code systems that define or constrain hospital bills and explanation-of-benefit (EOB) structures.

Explain relevance: For each resource, briefly explain how it maps to bill structure (e.g., header fields, line items, adjudication, coverage, codes).

Crosswalk summary: Describe at a high level how these resources relate to each other (e.g., which define paper/EDI fields, which define API schemas, which define code sets).

Gaps & risks: Note any licensing or access constraints (e.g., paywalled specs), regional differences, or ambiguities that could affect implementation.

Actionable next steps: Propose a short, prioritized plan for building the ontology using only the sourced materials (no new fields invented).

Output format

Start with the Conclusion section.

Then provide a Resources section as a table with columns: Name | Type (standard/form/model/code set) | Scope | Why it matters | Official link.

Follow with Crosswalk Summary, Gaps & Risks, and Actionable Next Steps.

Include direct citations/links for every resource you mention. Do not propose your own ontology or field list. Constraints

Do not generate or infer any new schema fields.

Do not include any speculative design.

Focus on official or widely adopted sources (standards bodies, government/industry groups, major frameworks).

Clarity and concision over length.

Audience & tone Audience: engineers/designers building data models for healthcare billing. Tone: precise, neutral, implementation-oriented.

Acceptance criteria

Conclusion appears first and directly answers feasibility.

All items in Resources have working official links and a one-line relevance explanation.

Crosswalk accurately distinguishes standards vs. forms vs. code sets vs. data models.

No invented fields or ontologies are prese
```

### Result: https://chatgpt.com/share/68f74151-30dc-800f-b42c-61faa933d65a

## High-Level Pipeline

```
OCR'd Bill Texts  →  bill_parser.py
                        ↓
        Structured JSON (with placeholders)
                        ↓
? CoreNLP (https://stanfordnlp.github.io/CoreNLP/) corenlp_extractor.py
                        ↓
    Ontology Mapper (map to billing ontology schema)
                        ↓
        Graph Builder (Memgraph) graph_builder.py
                        ↓
  GraphRAG Query Layer (LLM reasoning?) graphrag_engine.py
```

## Parser output schema

```json
{
  "Source": {
    "source_path": "data/bill_3.txt",
    "parser_version": "x.x.x",
    "extracted_at": "2025-10-19T23:10:00Z",
    "confidence": CL
  },

  "Patient": {
    "full_name": "Jon Peck",
    "dob": "1991-02-14",
    "telecom": { "phone": "UNKNOWN" },
    "address": "9502 Claymont Ct, Louisville, KY 40241",
    "identifiers": [
      { "system": "MRN", "value": "UNKNOWN" }
    ]
  },

  "Coverage": {
    "plan_name": "HealthGuard Assurance",
    "subscriber_id": "JJAYG3MVQW99",
    "group_number": "UNKNOWN",
    "coverage_type": "UNKNOWN",
    "effective_period": { "start": "06/15/2023" },
    "deductible_remaining": "UNKNOWN",
    "out_of_pocket_remaining": "YES",
    "coinsurance": "15%",
    "payer": { "name": "HealthGuard Assurance", "payer_id": "UNKNOWN" }
  },

  "ProviderOrganization": {
    "name": "Horizon Medical Clinic",
    "npi": "UNKNOWN",
    "taxonomy_code": "UNKNOWN",
    "address": "UNKNOWN"
  },

  "Claim": {
    "claim_id": "UNKNOWN",
    "claim_type": "UNKNOWN",
    "service_period": { "start": "UNKNOWN", "end": "UNKNOWN" },
    "drg": null
  },

  "Bill": {
    "bill_id": "UNKNOWN",
    "account_number": "938460822",
    "statement_date": "UNKNOWN",
    "due_date": "UNKNOWN",
    "total_balance": 184.69,
    "paid": 41.04
    "owns": 143.64
    "currency": "USD",
    "status": "UNKNOWN"
  },

  "ChargeItems": [
    {
      "code": { "system": "CPT", "value": "85025" },
      "description": "CBC W/DIFF",
      "revenue_code": null,
      "place_of_service": "UNKNOWN",
      "modifiers": [],
      "quantity": 1,
      "unit_price": 18.25,
      "charge_amount": 18.25,
      "service_date": "2023-06-15",
      "adjudication": [
        { "type": "allowed", "amount": 18.25 },
        { "type": "paid", "amount": 1.85 },
        { "type": "deductible", "amount": 0.00 },
        { "type": "coinsurance", "amount": 16.41 }
        { "type": "copay", "amount": 00.00 }
      ]
    }
    // more
  ],

  "Payments": [
    {
      "payment_date": "UNKNOWN",
      "payment_amount": 41.04,
      "payment_method": "insurerance",
      "payer_entity": "HealthGuard Assurance",
      "reference_id": "UNKNOWN",
      "applied_to": "Bill"
    }
    {
      "payment_date": "UNKNOWN",
      "payment_amount": 143.64,
      "payment_method": "outofpocket",
      "payer_entity": "Patient",
      "reference_id": "UNKNOWN",
      "applied_to": "Bill"
    }
  ],

  "AdjudicationDetails": [
    {"type": "allowed", "amount": 184.69},
    {"type": "paid", "amount": 41.04},
    {"type": "out_of_pocket", "amount": 143.64}
  ],

  "PaymentPlan": null,
  "FinancialAssistance": null,
  "CollectionActivity": null
}
```
