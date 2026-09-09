# CoD2 / x87sidecar issue #23 — x87 block trace capture (PR #35 build)

- sidecar: `4af191b8a783d16980bab66ae60fc7fc93d84343` (PR #35), built locally, codesign ok
- host: macOS 26.5.1 (Darwin 25.5.0), MacBook Air M2; WineCX 24.0.7 wow64 (Sikarugir); libRosettaRuntime md5 3fd28585277ad4600e6c830c10a66446
- env: X87_STOCK_HASH_LIST=0x1 X87_TRACE_BLOCK=0x129250d0f7976b3f X87_TRACE_OUTPUT=/tmp/cod2-x87 X87_TRACE_STOP_NEGATIVE=1 X87_NO_PREAUTH=1 WINEDEBUG=+seh,+tid,+timestamp (otherwise unchanged)
- trigger: rapid weapon switching in combat (same as all previous runs)
- result: #DE at mss32+0x3d457, mixer thread 0124, **61.4 s** after CoD2SP_s.exe start; eax=ff130000 (−237 → 65536·(2^x−1) family)
- sidecar: `[x87trace] wrote /tmp/cod2-x87.56941.x87trace: events=142278 retained=65536 dropped=0 frozen=0`
- note: a first run with tracing enabled went 417 s without a crash, but the trigger was not exercised in it (player away) — not evidence either way

Files:
- `cod2-x87.56941.x87trace.gz` — the retained window (16,777,472 bytes raw, magic X87TRC1); sha256 of the raw file: ee2471aededbc43a9c29df6c2cb294f76b091a23de3937056290de2efc75eadd
- `wine.err.gz` — full Wine log of the run (+seh,+tid,+timestamp)
