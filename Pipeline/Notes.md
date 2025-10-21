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


## Parser output schema

```json
{
  "Patient": {
    "full_name": "Jon Peck",
    "dob": "1991-02-14",
    "gender": "Male",
    "telecom": {
      "phone": "UNKNOWN",
      "email": "UNKNOWN"
    },
    "address": "9502 Claymont Ct, Louisville, KY 40241",
    "responsible_party": "Jon Peck",
    "identifiers": [
      { "system": "MRN", "value": "UNKNOWN" }
    ]
  },
  "Coverage": {
    "payer_name": "HealthGuard Assurance",
    "payer_code": "SPHSC",
    "subscriber_id": "JJAYG3MVQW99",
    "group_number": "UNKNOWN",
    "plan_name": "UNKNOWN",
    "eligibility_status": "Eligible",
    "eligibility_date": "2023-06-15",
    "deductible_remaining": "No",
    "coinsurance_percent": "15%",
    "copay_amount": "UNKNOWN",
    "out_of_pocket_remaining": "Yes"
  },
  "Payer": {
    "name": "HealthGuard Assurance",
    "identifier": "UNKNOWN",
    "address": "UNKNOWN",
    "telecom": {
      "phone": "UNKNOWN"
    }
  },
  "Provider": {
    "practice_name": "Horizon Medical Clinic",
    "physician_name": "Bernard Hudson",
    "billing_account_number": "938460822",
    "npi": "UNKNOWN",
    "address": "UNKNOWN",
    "telecom": {
      "phone": "UNKNOWN"
    }
  },
  "Service": {
    "date_of_service": "2023-06-15",
    "place_of_service": "UNKNOWN",
    "tests_ordered": [
      { "code": "005009", "code_system": "UNKNOWN", "description": "UNKNOWN" },
      { "code": "322000", "code_system": "UNKNOWN", "description": "UNKNOWN" },
      { "code": "001503", "code_system": "UNKNOWN", "description": "UNKNOWN" },
      { "code": "998085", "code_system": "UNKNOWN", "description": "UNKNOWN" },
      { "code": "004598", "code_system": "UNKNOWN", "description": "UNKNOWN" }
    ]
  },
  "Bill": {
    "statement_type": "ESTIMATE",
    "currency": "USD",
    "totals": {
      "health_plan_allowed_amount": "184.69",
      "estimated_amount_paid_by_health_plan": "41.04",
      "patient_out_of_pocket": "143.64",
      "amount_due": "143.64"
    },
    "line_items": [
      {
        "code": "85025",
        "code_system": "CPT",
        "description": "CBC W/DIFF",
        "allowed_amount": "18.25",
        "estimated_plan_paid": "1.85",
        "deductible": "0.00",
        "coinsurance": "16.41",
        "copay": "0.00"
      },
      {
        "code": "80053",
        "code_system": "CPT",
        "description": "CMP",
        "allowed_amount": "15.21",
        "estimated_plan_paid": "0.22",
        "deductible": "0.00",
        "coinsurance": "14.99",
        "copay": "0.00"
      },
      {
        "code": "82607",
        "code_system": "CPT",
        "description": "VITAMIN BH",
        "allowed_amount": "20.10",
        "estimated_plan_paid": "2.34",
        "deductible": "0.00",
        "coinsurance": "17.76",
        "copay": "0.00"
      },
      {
        "code": "36415",
        "code_system": "CPT",
        "description": "BLOOD DRAWING",
        "allowed_amount": "18.32",
        "estimated_plan_paid": "5.62",
        "deductible": "0.00",
        "coinsurance": "12.70",
        "copay": "0.00"
      },
      {
        "code": "82728",
        "code_system": "CPT",
        "description": "FERRITIN",
        "allowed_amount": "15.64",
        "estimated_plan_paid": "2.44",
        "deductible": "0.00",
        "coinsurance": "13.20",
        "copay": "0.00"
      },
      {
        "code": "83550",
        "code_system": "CPT",
        "description": "IRON BIND CAPACITY",
        "allowed_amount": "16.41",
        "estimated_plan_paid": "5.94",
        "deductible": "0.00",
        "coinsurance": "10.46",
        "copay": "0.00"
      },
      {
        "code": "83540",
        "code_system": "CPT",
        "description": "IRON",
        "allowed_amount": "15.96",
        "estimated_plan_paid": "2.93",
        "deductible": "0.00",
        "coinsurance": "13.03",
        "copay": "0.00"
      },
      {
        "code": "80061",
        "code_system": "CPT",
        "description": "LIPID PANEL",
        "allowed_amount": "18.31",
        "estimated_plan_paid": "0.81",
        "deductible": "0.00",
        "coinsurance": "17.50",
        "copay": "0.00"
      },
      {
        "code": "83036",
        "code_system": "CPT",
        "description": "HGB; GLYCATED",
        "allowed_amount": "9.29",
        "estimated_plan_paid": "10.04",
        "deductible": "0.00",
        "coinsurance": "-0.75",
        "copay": "0.00"
      },
      {
        "code": "86803",
        "code_system": "CPT",
        "description": "HEPATITIS C AB",
        "allowed_amount": "8.04",
        "estimated_plan_paid": "3.36",
        "deductible": "0.00",
        "coinsurance": "4.68",
        "copay": "0.00"
      },
      {
        "code": "Additional",
        "code_system": "UNKNOWN",
        "description": "Additional billing codes",
        "allowed_amount": "20.57",
        "estimated_plan_paid": "2.84",
        "deductible": "0.00",
        "coinsurance": "17.73",
        "copay": "0.00"
      }
    ]
  }
}
```
https://mermaid.live/edit#pako:eNqlWf1uo8oVfxXEVaNWilmGb1ypku1kE-9NHNdJd5VuVojAxBktBsRHWt_VSn2W-2j3SXpmgAEGcCo1f8H5mt9v5sw5B-eHHCQhlufybDZ7ioMkfiH7-VMsSZF_TMpiLuHo-1PMlC9R8q_g1c8K6eECLPLyeZ_56St9uKIP6tcneUmiSIlIjD1S4EMu_dnPMv_4lyf5G40pSSHJcFCQJJYelpWE_t1Q119U6Y___C5ROHPJMVXN5O9efswh3FxabR-YMMR5AG_LlfTlw8X640cev4rm-RAPOYpmioqUKhRnIA9BriqqKsoDam8pBhoo0lEPRImgLhFVNfV3idxuhTAVA1PRkKio1tU0UT7OAFUMDMV1B4pxBhploHUZaJZqv8fg8_phcbveSMtrIRojoqkKEpdhRDRFN0T5OBGtImIrtjVQjBPRKRG9Q0S3DPRuTi1v7u4upIvd4st6cyUEbNJK10QFRWAq1kA-zkWvuGiKPVSMczEoF6N3KLbmvMfl4-Vut35Yb4RYTW5ZhqiojsQYyMdpGBUNXdGGinEaJqVhdmnopqm-R2O9u4PEWm8upNViu1itHx6FqBWh4S0163NxDVE-TsisCKmKYQ0U44QsSsjqEzL-J0JCnOZMXEtUVGfi6qJ8nILVnIk6cJigYFMKdr9iWeg9Cjfr7fpC2i42lzdCOH5JkKio1ncG8nEmdnPhzaFinIlDmTi9w1B16z0m11fLv0pXN4-rxcPlhRCQcXEVzRXlaZUnqiEqxrk4jMtMVWxzoBjn4lIubpeL5ajv9pHry-3iAW78vbSSFkshIiPjDDC7jIyu6JYoH-fiMi6GYjkD-URLZM0ddbv7IgwJHQL8aMjoH5tfN3dfNh1WHetnGC9IvGceubhM02pMe6CpLpFjDBQTXVPl3UYfagSaOA4rg-XXD9UA9CR_-CbNZlJe-EAJx4VXHFMMkr9JSy8vwL2vmUuX9w_rW0hAvtiS-gdlluE4ONaeQXAE10YIO3V_0bcvksKP8tq6eqGQHtgTBVXbetxQesV-VLx6aeTHnh_BgIdDzz8kZVw0YRC7znDe7SXoBsB5QQ5ApnHzUp-E3vPR60RuQtHRwkDdDOxGSv2C0B2BqdNLXrw0Cb5jjkJnU4ze7Vld33rtsGx2uTBGHBhhv9qgLd2ZbbVkuzVbavJSRpEX-4cq1pY9QrRPMLRucfCdx2PGYfJcm8ETXdN10UzVZsjo2-0hTXBWm1YvYH3rR7hv54dhhvMao0ffaAmCaVhawUR-SOBgVsW5dJOUJH-DXMPn0q-PkqFqnebHAkGUNIlz8hxhOJOsONYhqXySTYEjHCSH2hTe6C7Vws4uUQ07stckbnaJPUPg-v62cRtjfPBJVBuz5zFjakhCOBPyQnDWbAMJWSJ3FF-lb108YMBNablZc0vpF7UDBbTsYrJa03rQ4kNPY7cZ2r75UYk7pvA-ApzlVpnjHErTG878feWyuvtMga9qWQsZFFXOH3HW5hpIvTSG8Nfs8lyVfhZKizwvMz8O2kTpOdNS2DrTsnW_vb5ficbwkZYHGXkGDxJy-5zQAvjp0-LxSr_9_Pcvna-E2m-fJWXqxeXhuc5e6rbP0pE9aGDRWtKnBJJpexyRPYHCToqjR-timXNHqgLHS2YR4VOeIdSgjl9YsF6g6TPVmiFT9AxxWMJnKL0bGc3FmDaVxhuU9NJtEtErSEhcn4WX4izAdZWkTkzHZrg_Dd3gpLpVtbIH4fSm9IrgCMYkoSfw2GmCLANpf8QhNIIqYRePVZWDPBmkHqMCZ0ryxpZfQUU6YHreH9qkkZRq4dpm8UhDtDVy8dhUydOZWzu2F5m7s0QclIPKvFcTwbauihPWvRoG1pNVrNIJdawSTlYztssvGYRPs-SN8JK-qy76thZ2VtnVtyLzIeEgcdpN2_E9SzLyG9TjWxySAKacFcw4JGh5NSFejzkJSPd2QYwwoXd-ibOYbvl1GeZJPHCt5ybPDwLWKDv3GUKAlF4XV3cMS3U6Py007nFKOOSUjG19bdg7qd3kQdXWvZPaTR_UbuScdtMNh0VXGOec5S3P7WWV-EFUwvjI4tx_XtE173H2RoJOfQY5qxNQVeg9zCt94wKbno_Xl9oPKl4w6pgyRxHyDes0I_MX_Smra9JOW6zK0lmrsUu7dm19a9RhV90pZI0-6OuhOHFNExlNgUQcJDoJEnm9UCJIxEGiUZCIg0QCSNSC1KZAahykdhKk5vVCiSA1DlIbBalxkJoAUmtB6lMgdQ5SPwlS93qhRJA6B6mPgtQ5SF0AqbcgjSmQBgdpnARpeL1QIkiDgzRGQRocpCGANFqQ5hRIk4M0T4I0vV4oEaTJQZqjIE0O0hRAmi1IawqkxUFaJ0FaXi-UCNLiIK1RkBYHaQkgrRakPQXS5iDtkyBtrxdKBGlzkPYoSJuDtAWQdgvSmQLpcJDOSZCO1wslgnQ4SGcUpMNBOgJIpwXpToF0OUj3JEjX64USQbocpDsK0uUgXQGk2ynmky0HtT0HnW46qO06aLTtoLbvoPHGg9rOg8TWg9rewz_d6b-WJNJ8vEG3OqPd4IxW2zNazc5otTijt_GMZvsZzaYzelpndDeosdpr1EkG01r-oQCOeTMZ_D-h5XN5n5FQnr_4UY7P5QPOYHSHd_kHXRemm1d8gDljDo8hfvHLqHiSn-Kf4Jf68T-T5CDPi6wET_ju2r_yOGVKR5EL4u8zvzVhPyOs6NHJc8NkIeT5D_nf8nxmGAgpGnIsZOmmrVruuXwEI0dBmmbqtq7ahq452s9z-Te2KNLOZRg_iyS7rf4fyP4t-PO_8FwOoA

## High-Level Pipeline

```
OCR'd Bill Texts  →  bill_parser.py
                        ↓? CoreNLP
          Structured JSON (with placeholders) 
                        ↓?? CoreNLP
    Ontology Mapper (map to billing ontology schema) →  node_edges.py
                        ↓
            Graph Builder (Memgraph) → graph_builder.py
                        ↓
  GraphRAG Query Layer (LLM reasoning?) → graphrag_engine.py
```
