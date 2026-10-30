# BELL Redteam Plan (think-research-design-plan-act)

## Think
- 8-char hex PSK, reduced 13-char keyspace (12345679ACDEF) ~8.16e8.
- Capture needs root/monitor; no root available, no handshakes yet.
- Only CPU OpenCL (PoCL) available; 20,936 H/s at -O -w 3 (device 1).
- config device_ids "1,2" invalid (only 1 device).

## Research
- Use -1 12345679ACDEF -a 3 ?1x8, --markov-disable.
- -O -w 3, temp-abort 85, pin device 1.
- Prefer PMKID capture (single frame), mode 22000.
- Resumable sessions with --potfile-path and --restore.

## Design
1. Capture scoped PMKID via hcxdumptool (requires sudo).
2. Convert with hcxpcapngtool -> all.22000.
3. Filter to BELL SSIDs -> bell.22000.
4. Benchmark + candidate generation (hcxeiutool/hcxpsktool/rules).
5. Attack GPU/CPU with wordlist then mask, resumable.
6. Report cracked + summary, secure outputs.

## Act
- Fixed device_ids to 1, cores 8, speed 20936 in config (blocked: root-owned file; apply manually).
- Created this plan. Next: obtain sudo/root to capture; then run pipeline.
