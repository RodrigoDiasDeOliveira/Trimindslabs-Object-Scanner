# ObjectScanner V1 README/ADR/code evidence review — 2026-10-11

## Scope and boundary

This is a source/documentation inspection of the default branch, comparing the README and selected ADRs with the tracked tree, Android source and CI workflow. No Gradle build, Android test, Python test, provider call, database connection, deployment, or live API check was run. Online status is not verified.

This repository is treated as a separate historical/implementation branch from ObjectScanner V2. Version labels alone do not establish direct succession, replacement, or greater completeness.

## Executive findings

1. **The tracked repository tree does not contain the PythonBackend or OracleDatabase directories described in the README.** The inspected tree contains the Android application, ADRs, architecture document path, workflow, and tracked Gradle/build artifacts. Therefore the README's Flask/Yolo/Azure/Oracle architecture is not evidenced as a complete implementation in this repository snapshot.
2. **The Android client does implement camera capture and multipart REST upload.** MainActivity uses CameraHelper and ObjectScanService; ObjectScanApi posts an image to /detect. RetrofitClient hardcodes the emulator address http://10.0.2.2:5000/ and comments that a physical device requires a different URL.
3. **The backend workflow targets a missing directory.** The Python job sets working-directory to ./PythonBackend, but that directory is absent from the inspected tree. The Android job also contains a malformed-looking checkout step where the uses value is written as a nested mapping rather than an action string. These are static workflow observations; no CI run was executed.
4. **The documented Azure fallback, YOLO inference, Oracle persistence, synchronization and audit trail are not evidenced by the tracked source.** The Android client handles the /detect response but the Python inference service, Azure adapter, Oracle schema and persistence layer are absent from this repository snapshot.
5. **Offline-ready claims are not supported by the inspected Android flow.** ObjectScanService posts the image to the remote API and returns null to the callback on request failure; no local image/result queue or retry/synchronization mechanism was identified in the inspected Android source.
6. **The README's clone path and repository slug may be stale.** The README points to RodrigoDiasDeOliveira/Object-Scanner, while the current repository is Trimindslabs-Object-Scanner. Align the canonical URL and clearly label this repository's current scope.
7. **Build artifacts and local Gradle state are tracked.** The repository tree contains Android/.gradle and Android/build paths, plus Android/local.properties. These should be reviewed for repository hygiene; no cleanup or file removal was performed.
8. **The ADR set has a numbering gap.** ADR-001 through ADR-007 and ADR-009 through ADR-012 are present; ADR-008 was not found in the inspected docs tree. The missing number should be explained or the index/numbering corrected without rewriting decision history.

## ADR evidence matrix

| ADR | Decision / capability | Evidence in inspected source | Assessment |
|---|---|---|---|
| ADR-001 | Overall system architecture | Android app and Retrofit client exist; PythonBackend and OracleDatabase directories described in README are absent from the tracked tree. | **Partial.** Mobile/API client path exists; the documented full-stack architecture is not present in this repository snapshot. |
| ADR-002 | Mobile framework | Android project uses Java, Android SDK, CameraX, Retrofit and Gson. | **Source evidence present.** Build/test status not verified. |
| ADR-003 | YOLO object-detection model | No YOLO model/backend files were found in the inspected tree; Android client only submits images to /detect and parses ObjectCountResponse. | **Not evidenced in this repository snapshot.** The server-side model path must be linked from a real separate repository or marked not present. |
| ADR-004 | Dataset management / Roboflow | No Python training scripts, dataset directory or Roboflow integration were found in the inspected tree. | **Not evidenced in this repository snapshot.** |
| ADR-005 | Flask backend | README and ADR choose Flask, and CI attempts to run in PythonBackend, but that directory and app.py/requirements.txt are absent from the inspected tree. | **Not present in this repository snapshot.** CI backend job is inconsistent with tracked contents. |
| ADR-006 | Oracle persistence | README/ADR describe Oracle storage, but no OracleDatabase schema or Python database adapter is present in the inspected tree. | **Not evidenced in this repository snapshot.** |
| ADR-007 | Azure Vision fallback / barcode fallback | Android client calls only the /detect endpoint. No Azure client or fallback orchestration is present in the inspected Android source. | **Not evidenced in this repository snapshot.** |
| ADR-009 | Large dataset management | ADR exists, but the corresponding dataset management/backend implementation is not present in the inspected tree. | **Decision documented; implementation not evidenced here.** |
| ADR-010 | Model export strategy | ADR exists, but no model export/training code or model artifact was identified in the inspected tree. | **Decision documented; implementation not evidenced here.** |
| ADR-011 | Image processing and data flow | Android captures a bitmap, compresses it as JPEG and sends it as multipart form data. Server-side processing stages are not included in the inspected tree. | **Mobile upload path evidenced; end-to-end processing not evidenced.** |
| ADR-012 | Integration and deployment | Client has a hardcoded emulator URL; workflow expects a missing Python backend; no Dockerfile/deployment manifest was identified in the inspected tree. | **Partial / inconsistent.** Deployment and TLP/cloud synchronization are not evidenced in this repository snapshot. |

## Specific implementation and documentation mismatches

- README's project structure includes PythonBackend, its model/training/services files, and OracleDatabase/schema, but none of these paths appears in the inspected default-branch tree.
- CI's Python job uses a working directory that is absent from the repository snapshot. The Android workflow step for checkout uses a nested mapping under uses rather than a plain action reference. Current workflow status remains unverified.
- RetrofitClient uses the Android emulator's special loopback address; this is not a general server URL for physical devices or cloud deployment.
- ObjectScanService has no offline queue: it uploads immediately and invokes the callback with null on network failure.
- README claims an Azure fallback below a confidence threshold, but the inspected client has no Azure fallback path and no backend implementation is tracked here.
- README documents unit, integration and performance tests, but the inspected repository tree does not show the described Python test suite or broad Android tests. No test execution was performed.
- Tracked Gradle cache/build output and local.properties may be environment-specific. Their content and cleanup impact should be reviewed separately before removal.
- The absence of the Python backend from this repository does not prove it is absent from all repositories or deployments; this report is limited to this repository's tracked default-branch tree.

## Recommended follow-up

1. Decide whether this repository is intended to be Android-only, or whether the Python backend and Oracle schema should be restored or linked as explicit separate repositories.
2. Update README structure, setup instructions, technology badges, and ADR evidence to match that decision.
3. Repair the CI workflow only after confirming the intended backend source location; correct the Android checkout step and make required tests fail the job rather than silently passing when no tests exist.
4. Mark YOLO, Azure fallback, Oracle persistence, offline queue and TLP synchronization as planned/not evidenced until source and end-to-end tests demonstrate them.
5. Document supported base URLs for emulator, physical device and deployment environments; do not imply the emulator URL works outside the emulator.
6. Review tracked Gradle/build/local configuration artifacts in a separate hygiene change; this documentation PR removes nothing.
7. Reconcile the missing ADR-008 number with the intended historical decision sequence.

## Explicit non-claims

This review does not claim that the Android app currently builds, that the workflow currently fails, that the service is offline, or that the backend cannot exist elsewhere. No source, build artifacts, secrets, cloud resources or deployments were changed.
