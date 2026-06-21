Sprint 2 (June 15–28)
Goal: Bug Fixes + Core Experiment Wired to Cloud Storage

Fix ConvertImagesToBinary — use parameters with env var fallback, not the other way around
Fix the index mismatch between spatial files and imageData array
Fix hardcoded dev machine fallback paths in ImageSpatial.cs and Program.cs
Implement DownloadInputFile — pull training images from blob storage
Implement UploadResultFile — push result images back to blob
Implement UploadExperimentResult — write ExperimentResult record to table storage
Set up logging concept: define LogInfo, LogError, LogDebug, Log

Deliverable: Bugs fixed, experiment runs locally end-to-end — reads from queue, downloads, trains, uploads

Sprint 3 (June 29 – July 12)
Goal: Wrap Pipeline into IExperiment + Complete MCP Integration

Wrap the full Program.cs pipeline inside IExperiment — binarize → vectorize → spatial pool → train → reconstruct → similarity → Excel
Connect IExperiment to queue trigger — message received starts the experiment
Complete and test MCP server (already partially integrated via ModelContextProtocol package)
Test MCP agent triggering the experiment locally via STDIO and HTTP
Write Experiment Specification - Firstname Lastname.md

Deliverable: Full pipeline runs through IExperiment, triggered by queue message, MCP server operational
