# Project State Process Steps

This document captures the standard step-by-step process for keeping the HiveFabric project state current.

1. **Ingest Objectives:** Read `meta_parameters.yaml`, OKRs from governance, and current telemetry thresholds to understand what the fabric must deliver this cycle.
2. **Plan Work:** Use the engineering playbook to translate objectives into gitflow branches (`feature/`, `bugfix/`, etc.). Document each step in `process_steps.md` whenever a new sprint or focus area begins.
3. **Execute & Monitor:** Deploy tasks, run tests, and collect telemetry (QA, scheduler, billing metrics). Record major updates or blockers in `status_log.md`.
4. **Review & Adjust:** When metrics deviate, consult human legislators per the Immutable Rules, revise plans, and update the `status_log.md` with the outcome.
5. **Close Loop:** Once work passes QA and review, merge via gitflow, capture lessons (failures, successes) in this folder, and update the `status_log.md` to say where we are.
