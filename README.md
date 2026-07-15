# Frame-Semantic Annotation of EU Reporting Requirements

Supplementary material for our NXDG 2026 submission, *"Frame Semantics for EU Reporting Requirements: An Annotated Benchmark, Guidelines, and a Path Towards RRMV Population."*

This repository contains a frame-semantic annotation layer over a corpus of EU reporting requests, legislative provisions that require an EU institution, agency, or Member State to supply a report, technical standard, opinion, or similar artifact to another EU body. Each reporting request is annotated with six FrameNet frames (`Telling`, `Intentionally_create`, `Conditional_scenario`, `Time_vector`, `Frequency`, `Artifact`) capturing who must report what, to whom, under which conditions, by when, and how often.

## Contents

```
guidelines/
  annotation_guidelinesV5.md      Full annotation guidelines: frame definitions,
                                 decision rules, and worked examples

corpus/
  RR ENG Gold_standard_format.zip     Full INCEpTION project export: 91 annotated
                                 reporting requests, source texts, tagsets,
                                 and layer definitions

rrmv_mapping/
  frame_rrmv_mapping.json       Frame/Frame-Element to RRMV mapping (structured)
  frame_rrmv_mapping.csv        Same mapping, flat format
  rr_0002_rrmv_example.ttl      Worked example: one reporting request instantiated
                                 as RDF, aligned to RRMV Release 1.0.0
