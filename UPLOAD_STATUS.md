# wake-audio upload status (executor handoff)

## Goal
Publish morning.mp3.b64 (507740) + ambient.mp3.b64 (1176196) on joshhair/wake-audio main

## Plan B — ACTIVE staging+append (2026-09-19 ~16:35 PT)

### Proven pipeline
1. create_or_update_file → staging/chunk.txt (4000 chars)
2. Verify commit-pinned raw md5 before append
3. actions_run_trigger method=run_workflow workflow_id=append-staging-chunk.yml
   inputs: target_path, expected_size, expected_md5
4. Sequential only; wait for success; never parallel creates (409)

### Progress on main
- morning **000–025**: md5-good
- morning **026**: in progress via staging append
- Ambient: **0/148**
- Remaining ≈ morning_027–063 (37) + ambient_000–147 (148) = **185**
- Local queue: /workspace/wake-voices/upload_queue.txt

### Do NOT assemble until 64 morning + 148 ambient parts exist and md5-ok
