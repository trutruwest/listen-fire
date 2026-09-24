# Deploying to the mini

Verified 2026-09-24.

## The loop

1. Commit and push to `origin` (https://github.com/trutruwest/listen-fire).
2. `ssh mini`
3. `cd ~/Documents/Claude/listen-fire`
4. `git pull`
5. `cd deploy && docker compose pull && docker compose up -d`

## Notes that cost time to work out

**The path is the same relative to `$HOME`, not the same absolute path.**
The MacBook checkout is `/Users/trudywestby/Documents/Claude/listen-fire`;
the mini's is `/Users/nphard-mini/Documents/Claude/listen-fire`. The remote
user is `nphard-mini`.

**The pull needs no credentials.** The fork is public and `origin` is an HTTPS
URL, so `git pull` on the mini authenticates to nothing. SSH agent forwarding
is not required, and adding it would not help.

**`mini` is a Tailscale host** (`np-hards-mac-mini.tail8b9038.ts.net`) already
configured in `~/.ssh/config` on the MacBook. When it is asleep, `ssh` times
out and `tailscale status` shows the peer with `rx 0` or a bare `-`. That is a
sleeping machine, not a network or key fault.

**Deployment needs Docker, not pnpm.** Per `deploy/SELF_HOSTING.md` the
production path "needs no build and no toolchain — just Docker". `pnpm` is for
the development loop on the MacBook.

## Not yet satisfied

Docker is not installed on the mini, so step 5 cannot run there yet. Steps 1-4
are verified working.
