# che
Ecplise Che Devfiles

devfile.yaml Explanation
Here is exactly why this specific configuration works when everything else failed. Save this context for your future self:

The Identity Fix (echo ... >> /etc/passwd):

Problem: Che forces UID 1234. The Red Hat image doesn't know User 1234 exists.

Fix: We force the container to write its own name tag into the system registry on startup.

The Zombie Killer (fuser -k):

Problem: When a workspace restarts, sometimes the old process holds onto Port 3100, causing the new one to crash with EADDRINUSE.

Fix: We nuke anything on port 3100 before starting.

The Localhost Bypass (sed ... 0.0.0.0):

Problem: VS Code defaults to listening only on 127.0.0.1. This blocks external connections (like the Ingress controller).

Fix: We patch the startup script on the fly to listen on All Interfaces (0.0.0.0), allowing traffic from the outside world.
